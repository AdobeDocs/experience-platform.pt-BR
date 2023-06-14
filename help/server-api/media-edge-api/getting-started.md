---
keywords: Experience Platform;borda da mídia;tópicos populares;intervalo de datas
solution: Experience Platform
title: Introdução às APIs do Media Edge
description: Introdução às APIs do Media Edge
source-git-commit: b4687fa7f1a2eb8f206ad41eae0af759b0801b83
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 7%

---


# Introdução à API do Media Edge

Este guia fornece instruções para fazer interações iniciais bem-sucedidas com o serviço de API do Media Edge. Isso inclui iniciar uma sessão de mídia e rastrear eventos enviados para uma solução da Adobe Experience Platform (AEP), como o Customer Journey Analytics (CJA). O serviço da API de borda de mídia é iniciado com o ponto de extremidade de início de sessão. Depois que a sessão for iniciada, um ou mais dos seguintes eventos poderão ser rastreados:

* play
* ping
* bitrateChange
* bufferStart
* pauseStart
* adBreakStart
* adStart
* adComplete
* adSkip
* adBreakComplete
* chapterStart
* chapterComplete
* chapterSkip
* error
* sessionEnd
* sessionComplete
* statesUpdate

Cada evento tem seu próprio terminal. Todos os pontos de extremidade da API Media Edge são métodos POST, com corpos de solicitação JSON para dados de evento. Para obter mais informações sobre endpoints, parâmetros e exemplos da API do Media Edge, consulte o arquivo Media Edge Swagger.

Este guia mostra como rastrear os seguintes eventos após iniciar a sessão:

* Início do buffer
* Reproduzir
* Sessão concluída

## Implementar a API

Além de pequenas diferenças no modelo e nos caminhos chamados, a API Media Edge é a mesma da API Media Collection. Os detalhes de implementação do Media Collection permanecem válidos para a API Media Edge, conforme descrito na documentação a seguir:

* [Definição do tipo de solicitação HTTP no seu reprodutor](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Enviar eventos de ping](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Condições de tempo limite](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [Controlar a ordem dos eventos](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Autorização

Atualmente, as APIs do Media Edge não exigem cabeçalhos de autorização em suas solicitações.


## Início da sessão

Para iniciar a sessão de mídia no servidor, use o endpoint de Início de sessão. Uma resposta bem-sucedida inclui uma `sessionId`, que é um parâmetro obrigatório para solicitações de eventos subsequentes.

Antes de fazer a solicitação de início de sessão, você precisará do seguinte:

* A variável `datastreamId` é um parâmetro obrigatório para a solicitação POST Session Start. Para recuperar um `datastreamId`, consulte [Configurar um fluxo de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=pt-BR).

* Um objeto JSON para a carga da solicitação que contém os dados mínimos necessários (como mostrado no exemplo de solicitação abaixo).

Depois de obter essas informações, forneça a `datastreamId` na chamada a seguir:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Exemplo de solicitação

O exemplo a seguir mostra uma solicitação de cURL de início de sessão:

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

No exemplo de solicitação acima, a variável `eventType` o valor contém o prefixo `media` de acordo com a [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR) para especificar domínios.

Além disso, o mapeamento de tipos de dados para `eventType` no exemplo acima, estão como se segue:

| eventType | tipos de dados |
| -------- | ------ |
| mediaSessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): Matriz[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): Matriz[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| all | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### Exemplo de resposta

O exemplo a seguir mostra uma resposta bem-sucedida para a solicitação de início de sessão:

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

No exemplo de resposta acima, a variável `sessionId` é exibido como `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. Você usará essa ID em solicitações de evento subsequentes como um parâmetro obrigatório.

Para obter mais informações sobre parâmetros de ponto de extremidade de Início de sessão e exemplos, consulte o arquivo do Media Edge Swagger.

Para obter mais informações sobre parâmetros de dados de mídia XDM, consulte [Esquema de Informações de Detalhes de Mídia](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Solicitação de evento de início de buffer

O evento Início do buffer é sinalizado quando o buffering é iniciado no reprodutor de mídia. A retomada do buffer não é um evento no serviço de API; em vez disso, ela é inferida quando um evento de reprodução é enviado após o início do buffer. Para fazer uma solicitação de evento de Início do buffer, use `sessionId` na carga de uma chamada para o seguinte endpoint:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Exemplo de solicitação

O exemplo a seguir mostra uma solicitação de cURL de início de buffer:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

No exemplo de solicitação acima, o mesmo `sessionId` que é retornado na chamada anterior é usado como o parâmetro obrigatório na solicitação de Início do buffer.

Para obter mais informações sobre os parâmetros de ponto final de Início do buffer e exemplos, consulte o arquivo Media Edge Swagger.

A resposta bem-sucedida indica um status 200 e não inclui conteúdo.

## Reproduzir solicitação de evento

O evento Reproduzir é enviado quando o reprodutor de mídia altera seu estado para &quot;reproduzindo&quot; a partir de outro estado, como &quot;buffering&quot;, &quot;pausado&quot; ou &quot;erro&quot;. Para fazer uma solicitação de evento Play, use `sessionId` na carga de uma chamada para o seguinte endpoint:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Exemplo de solicitação

O exemplo a seguir mostra uma solicitação Play cURL:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

A resposta bem-sucedida indica um status 200 e não inclui conteúdo.

Para obter mais informações sobre parâmetros de endpoint de reprodução e exemplos, consulte o arquivo Media Edge Swagger.

## Solicitação de evento de conclusão de sessão

O evento Sessão concluída é enviado quando o fim do conteúdo principal é atingido. Para fazer uma solicitação de evento de Sessão Concluída, use `sessionId` na carga de uma chamada para o seguinte endpoint:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Exemplo de solicitação

O exemplo a seguir mostra uma solicitação de cURL de Sessão Concluída:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

A resposta bem-sucedida indica um status 200 e não inclui conteúdo.

## Códigos de resposta

A tabela a seguir mostra os possíveis códigos de resposta resultantes das solicitações da API do Media Edge:

| Status | Descrição |
| ---------- | --------- |
| 200 | A sessão foi criada com sucesso |
| 207 | Problema com um dos serviços que se conectam à Experience Edge Network (consulte mais no guia de solução de problemas) |
| nível 400 | Solicitação inválida |
| nível 500 | Erro do servidor |

Para obter mais informações sobre como manipular erros e códigos de resposta malsucedidos, consulte o Guia de solução de problemas do Media Edge.


