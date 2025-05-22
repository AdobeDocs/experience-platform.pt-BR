---
title: Personalização híbrida usando o Web SDK e a API do Edge Network
description: Este artigo demonstra como usar o Web SDK em conjunto com a API do Edge Network para implantar personalização híbrida em suas propriedades da Web.
keywords: personalização; híbrido; api do servidor; lado do servidor; implementação híbrida;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 7b91f4f486db67d4673877477a6be8287693533a
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 2%

---

# Personalização híbrida usando o Web SDK e a API do Edge Network

## Visão geral {#overview}

A personalização híbrida descreve o processo de recuperação de conteúdo de personalização no lado do servidor, usando a [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/), e de renderização no lado do cliente, usando a [Web SDK](../home.md).

Você pode usar personalização híbrida com soluções de personalização como Adobe Target, Adobe Journey Optimizer ou Offer Decisioning, sendo que a diferença é o conteúdo da carga da [!UICONTROL API do Edge Network].

## Pré-requisitos {#prerequisites}

Antes de implementar a personalização híbrida em suas propriedades da Web, verifique se você atende às seguintes condições:

* Você decidiu qual solução de personalização deseja usar. Isso terá um impacto no conteúdo da [!UICONTROL API do Edge Network].
* Você tem acesso a um servidor de aplicativos que pode usar para fazer as chamadas da [!UICONTROL API do Edge Network].
* Você tem acesso à [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/).
* Você [configurou](/help/web-sdk/commands/configure/overview.md) corretamente e implantou o Web SDK nas páginas que deseja personalizar.

## Diagrama de Fluxo {#flow-diagram}

O diagrama de fluxo abaixo descreve a ordem das etapas executadas para fornecer personalização híbrida.

![Diagrama de fluxo visual mostrando a ordem das etapas executadas para fornecer personalização híbrida.](assets/hybrid-personalization-diagram.png)

1. Todos os cookies existentes armazenados anteriormente pelo navegador, com o prefixo `kndctr_`, são incluídos na solicitação do navegador.
1. O navegador da Web do cliente solicita a página da Web do servidor de aplicativos.
1. Quando o servidor de aplicativos recebe a solicitação de página, ele faz uma solicitação `POST` ao [ponto de extremidade de coleta de dados interativa da API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) para buscar conteúdo de personalização. A solicitação `POST` contém um `event` e um `query`. Os cookies da etapa anterior, se disponíveis, estão incluídos na matriz `meta>state>entries`.
1. A API do Edge Network retorna o conteúdo de personalização ao servidor de aplicativos.
1. O servidor de aplicativos retorna uma resposta do HTML para o navegador cliente, contendo os [cookies de identidade e de cluster](#cookies).
1. Na página do cliente, o comando [!DNL Web SDK] `applyResponse` é chamado, transmitindo os cabeçalhos e o corpo da resposta da [!UICONTROL API do Edge Network] da etapa anterior.
1. O [!DNL Web SDK] renderiza ofertas do Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=pt-BR) e itens do Canal da Web do Journey Optimizer automaticamente, porque o sinalizador `renderDecisions` está definido como `true`.
1. As ofertas [!DNL HTML]/[!DNL JSON] baseadas em formulário de destino e as experiências baseadas em código Journey Optimizer são aplicadas manualmente por meio do método `applyProposition`, para atualizar o [!DNL DOM] com base no conteúdo de personalização da proposta.
1. Para ofertas [!DNL HTML]/[!DNL JSON] baseadas em formulário do Target e experiências baseadas em código Journey Optimizer, os eventos de exibição devem ser enviados manualmente para indicar quando o conteúdo retornado foi exibido. Isso é feito por meio do comando `sendEvent`.

## Cookies {#cookies}

Os cookies são usados para manter a identidade do usuário e as informações do cluster.  Ao usar uma implementação híbrida, o servidor de aplicações web manipula o armazenamento e o envio desses cookies durante o ciclo de vida da solicitação.

| Cookie | Finalidade | Armazenado por | Enviado por |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contém detalhes da identidade do usuário. | Servidor de aplicativos | Servidor de aplicativos |
| `kndctr_AdobeOrg_cluster` | Indica qual cluster do Edge Network deve ser usado para atender às solicitações. | Servidor de aplicativos | Servidor de aplicativos |

## Solicitar posicionamento {#request-placement}

As solicitações de API do Edge Network são necessárias para obter apresentações e enviar uma notificação de exibição. Ao usar uma implementação híbrida, o servidor de aplicativos faz essas solicitações à API do Edge Network.

| Solicitação | Feito por |
|---|---|
| Solicitação do Interact para recuperar apresentações | Servidor de aplicativos |
| Solicitação do Interact para enviar notificações de exibição | Servidor de aplicativos |


## Estabelecer o host regional da Edge Network {#regional-host}

Para estabelecer o host regional do Edge Network, primeiro leia a dica de localização do cookie `kndctr_<orgId>_AdobeOrg_cluster`, que pode ter os seguintes valores:

* `va6`
* `or2`
* `irl1`
* `ind1`
* `sgp3`
* `jpn3`
* `aus3`

Exemplo: `kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster: va6`

O host regional Edge Network usa o seguinte formato:`<location_hint>.server.adobedc.net` e pode ter os seguintes valores:

* `va6.server.adobedc.net`
* `or2.server.adobedc.net`
* `irl1.server.adobedc.net`
* `ind1.server.adobedc.net`
* `sgp3.server.adobedc.net`
* `jpn3.server.adobedc.net`
* `aus3.server.adobedc.net`

Ao usar esses hosts específicos, as solicitações serão direcionadas para o mesmo local do Edge Network que o usuário visitou antes e o sistema poderá fornecer a melhor experiência, pois os dados do usuário estão presentes nele.

Se nenhuma dica de localização (ou seja, nenhum cookie) estiver presente, use o host padrão: `server.adobedc.net`.

>[!TIP]
>
>Como prática recomendada, você deve usar uma lista de locais permitidos. Isso impede que a dica de localização seja temperada com, pois é fornecida por meio de cookies do lado do cliente.

## Implicações do Analytics {#analytics}

Ao implementar a personalização híbrida, você deve prestar atenção especial para que as ocorrências de página não sejam contadas várias vezes no Analytics.

Quando você [configura uma sequência de dados](../../datastreams/overview.md) para o Analytics, os eventos são automaticamente encaminhados para que as ocorrências da página sejam capturadas.

A amostra dessa implementação usa dois fluxos de dados diferentes:

* Uma sequência de dados configurada para o Analytics. Essa sequência de dados é usada para interações do Web SDK.
* Uma segunda sequência de dados sem uma configuração do Analytics. Essa sequência de dados é usada para solicitações de API do Edge Network. Você deve configurar essa sequência de dados com a mesma configuração de destino da sequência de dados configurada para o Analytics.

Dessa forma, a solicitação do lado do servidor não registra eventos do Analytics, mas as solicitações do lado do cliente registram. Isso faz com que as solicitações do Analytics sejam contadas com precisão.

## Criar a solicitação do lado do servidor {#server-side-request}

O exemplo de solicitação abaixo ilustra uma solicitação da API do Edge Network que o servidor de aplicativos poderia usar para recuperar o conteúdo de personalização.

>[!IMPORTANT]
>
>Este exemplo de solicitação usa o Adobe Target como uma solução de personalização. Sua solicitação pode variar de acordo com a solução de personalização escolhida.


**Formato da API**

```http
POST /ee/v2/interact
```

### Solicitação {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries": [{
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
           "value":"CiY0NzE0NzkwMTUyMzYzMzI4NDAxMjc3NDcwNzA2NTcxMjI3OTI1NVIRCJ_S-uCRMRABGAEqBElSTDHwAZ_S-uCRMQ=="
         }, {
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
           "value": "general=in"
         }, {
            "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster",
            "value": "va6"
         }]
      }
   }
}'
```

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sim. | A ID da sequência de dados usada para transmitir as interações para a Edge Network. Consulte a [visão geral das sequências de dados](../../datastreams/overview.md) para saber como configurar uma sequência de dados. |
| `requestId` | `String` | Não | Uma ID aleatória para correlacionar solicitações internas do servidor. Se nenhum for fornecido, o Edge Network gerará um e o retornará na resposta. |

### Cabeçalhos de proxy {#proxy-headers}

Os seguintes cabeçalhos são necessários para processar a solicitação corretamente.

* `Referer`
* `X-Forwarded-For`
* `X-Forwarded-Proto`
* `X-Forwarded-Host`

Defina-os corretamente para apontar para as informações reais do cliente. Por exemplo, o cabeçalho `X-Forwarded-For` deve conter o IP do cliente para que a geolocalização adequada ocorra.

### Cabeçalhos do usuário-agente {#user-agent-headers}

Use os seguintes cabeçalhos user-agent para processar a solicitação corretamente.

**Padrão**

* `User-Agent`

**Baixa entropia (obrigatório):**

* `Sec-CH-UA`
* `Sec-CH-UA-Mobile`
* `Sec-CH-UA-Platform`

**Alta entropia (opcional):**

* `Sec-CH-UA-Platform-Version`
* `Sec-CH-UA-Arch`
* `Sec-CH-UA-Model`
* `Sec-CH-UA-Bitness`
* `Sec-CH-UA-WoW64`

A solicitação deve ser enviada conforme mostrado na [especificação da API Edge Network](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/). Consulte a [documentação de personalização](https://developer.adobe.com/data-collection-apis/docs/getting-started/personalization/), se necessário.

### Resposta do lado do servidor {#server-response}

A resposta do Edge Network conterá `state:store` instruções, que devem ser transformadas em `Set-Cookie` cabeçalhos. Eles serão salvos no navegador e a implementação do Web SDK poderá usá-los.

Os cookies devem ser definidos no domínio de nível superior, para que sejam enviados junto com solicitações para a implementação do servidor e do cliente. (Ou pelo menos um subdomínio comum usado por ambas as implementações)

Exemplo:

* Chamadas do lado do servidor usam `api.example.com`
* As chamadas do lado do cliente usam `adobe.example.com`

Os cookies devem ser definidos em `.example.com` para que sejam compartilhados em ambos os casos.

A resposta do lado do servidor é organizada em fragmentos chamados `Handles`, que são gerados dependendo da configuração da sequência de dados. Por exemplo, os mecanismos de personalização em tempo real retornam `personalization:decisions` identificadores enquanto o mecanismo de ativação em tempo real produz `activation:pull` identificadores.

O exemplo de resposta abaixo mostra como pode ser a resposta da API do Edge Network.

```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```



## Solicitação do lado do cliente {#client-request}

Na página do cliente, o comando [!DNL Web SDK] `applyResponse` é chamado, transmitindo os cabeçalhos e o corpo da resposta do lado do servidor.

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

As ofertas [!DNL JSON] baseadas em formulário são aplicadas manualmente por meio do método `applyPersonalization`, para atualizar o [!DNL DOM] com base na oferta de personalização. Para atividades baseadas em formulário, os eventos de exibição devem ser enviados manualmente para indicar quando a oferta foi exibida. Isso é feito por meio do comando `sendEvent`.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## Aplicativo de amostra {#sample-app}

Para ajudá-lo a experimentar e saber mais sobre esse tipo de personalização, fornecemos um aplicativo de amostra que você pode baixar e usar para testes. Você pode baixar o aplicativo, juntamente com instruções detalhadas sobre como usá-lo, neste [repositório do GitHub](https://github.com/adobe/alloy-samples).
