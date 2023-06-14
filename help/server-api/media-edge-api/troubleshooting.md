---
keywords: Experience Platform;borda da mídia;tópicos populares;intervalo de datas
solution: Experience Platform
title: Introdução às APIs do Media Edge
description: Guia de solução de problemas de APIs do Media Edge
source-git-commit: f723114eebc9eb6bfa2512b927c5055daf97188b
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# Guia de solução de problemas da API do Media Edge

Este guia fornece instruções para a solução de problemas relacionados a erros e para a obtenção de respostas bem-sucedidas.

## Uso de ajudas de resposta a erros

Para ajudar a solucionar problemas de respostas malsucedidas, os erros são acompanhados por um corpo de resposta contendo um objeto de erro. Nesse caso, o corpo da resposta contém detalhes do problema, conforme definido por [RFC 7807 Detalhes do problema para APIs HTTP](https://datatracker.ietf.org/doc/html/rfc7807). Para melhorar a experiência do usuário da API, os detalhes do problema são descritivos (os detalhes das chaves da matriz são exibidos usando JsonPath para o campo ausente ou inválido). Eles também são cumulativos (todos os campos inválidos serão relatados na mesma solicitação).


## Validação de inícios de sessão

A maioria dos problemas ao criar solicitações de Início de sessão resulta em uma resposta de 207 Vários status.
A carga é semelhante aos erros não fatais da API do servidor da rede de borda da Experience. Todos os erros do Media Analytics têm o seguinte tipo:  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. Os números exibidos na resposta correspondem ao status do erro.

O exemplo a seguir mostra um corpo de resposta para uma solicitação de Início de sessão que não tem um campo obrigatório e tem um campo inválido.

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

No exemplo acima, ambos os problemas são observados por `name` e `reason` em `details`: o primeiro motivo é exibido `missing required field` e o segundo descreve a não-conformidade com a norma ISO 8601.


>[!NOTE]
>
> Para erros causados de forma ascendente pelo Media Analytics, o Adobe recomenda que você continue a processar a sessão de mídia gerada.

## Validação de eventos

A maioria das solicitações de evento inválidas resulta em uma resposta 400 de Solicitação incorreta. Nesses casos, a carga é semelhante aos erros fatais da API do servidor da rede de borda da Experience.

Para solicitações de evento, o serviço de API de borda de mídia inclui verificações adicionais que não são capturadas no próprio modelo XDM. Isso inclui a verificação de que o caminho `eventType` corresponde à carga da solicitação `eventType`.


O exemplo a seguir mostra uma `eventType` incompatibilidade com um `adBreakStart` carga enviada para `ee/va/v1/chapterStart`:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

O exemplo a seguir mostra uma verificação adicional da API do Media Edge que encontra um `chapterStart` chamada ausente `chapterDetails` informações:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## Lidar com erros de nível 400 e 500

A tabela a seguir fornece instruções para tratar erros de resposta de status:


| Código de erro | Descrição |
| ---------- | --------- |
| 4xx Solicitação incorreta | A maioria dos erros 4xx (por exemplo, `400`, `403`, `404`) não deve ser repetido pelo usuário. Tentar novamente a solicitação não resultará em uma resposta bem-sucedida. O usuário deve corrigir o erro antes de tentar novamente a solicitação. Eventos que resultam em códigos de status 4xx não são rastreados, o que pode afetar a precisão dos dados em sessões que receberam respostas 4xx. |
| 410 Não existe mais | Indica que a sessão destinada ao rastreamento não está mais sendo calculada no lado do servidor. O motivo mais comum para isso é que a sessão tem mais de 24 horas. Depois de receber um `410`, tente iniciar uma nova sessão e rastreie-a. |
| 429 Muitas solicitações | Esse código de resposta indica que a taxa do servidor está limitando as solicitações. Siga as **Repetir-após** instruções no cabeçalho de resposta com cuidado. Qualquer resposta que flua de volta deve ter o código de resposta HTTP com um código de erro específico de domínio. |
| Erro interno de servidor 500 | `500` os erros são genéricos, erros &quot;catch-all&quot;. `500` os erros não devem ser repetidos, exceto por `502`, `503` e `504`. |
| 502 Gateway incorreto | Este código de erro indica que o servidor, ao atuar como um gateway, recebeu uma resposta inválida dos servidores upstream. Isso pode ocorrer devido a problemas de rede entre servidores. O problema temporário da rede pode se resolver sozinho, portanto, tentar novamente a solicitação pode resolver o problema. |
| 503 Serviço indisponível | Este código de erro indica que o serviço está temporariamente indisponível. Isso pode ocorrer durante os períodos de manutenção. Destinatários de `503` erros podem repetir a solicitação, mas também devem seguir a variável **Repetir-após** instruções do cabeçalho. |


## Enfileirar eventos quando as respostas da sessão forem lentas

Após iniciar uma sessão de rastreamento de mídia, o reprodutor de mídia pode ser acionado antes que a resposta do Início da sessão retorne (com o parâmetro da ID de sessão) do back-end. Se isso ocorrer, o aplicativo deve colocar em fila todos os eventos de rastreamento que chegam entre a solicitação de início de sessão e a resposta. Quando a resposta das sessões for recebida, primeiro você deve processar todos os eventos na fila, e depois começar a processar os eventos em tempo real.

Para obter melhores resultados, verifique o reprodutor de referência na distribuição para obter instruções sobre como processar eventos antes de receber uma ID de sessão.

O exemplo a seguir mostra um método para processar eventos antes de receber uma ID de sessão:


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


