---
title: Personalização híbrida usando o SDK da Web e a API do servidor do Edge Network
description: Este artigo demonstra como você pode usar o SDK da Web em conjunto com a API do servidor para implantar personalização híbrida em suas propriedades da Web.
keywords: personalização; híbrido; api do servidor; lado do servidor; implementação híbrida;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 3%

---

# Personalização híbrida usando o SDK da Web e a API do servidor do Edge Network

## Visão geral {#overview}

A personalização híbrida descreve o processo de recuperação de conteúdo de personalização no lado do servidor, usando a [API do Edge Network Server](../../server-api/overview.md), e de renderização no lado do cliente, usando o [SDK da Web](../home.md).

Você pode usar personalização híbrida com soluções de personalização como Adobe Target, Adobe Journey Optimizer ou Offer Decisioning, sendo que a diferença é o conteúdo da carga da [!UICONTROL API do servidor].

## Pré-requisitos {#prerequisites}

Antes de implementar a personalização híbrida em suas propriedades da Web, verifique se você atende às seguintes condições:

* Você decidiu qual solução de personalização deseja usar. Isso terá um impacto no conteúdo da carga da [!UICONTROL API do servidor].
* Você tem acesso a um servidor de aplicativos que pode ser usado para fazer as chamadas da [!UICONTROL API do Servidor].
* Você tem acesso à [API do Edge Network Server](../../server-api/authentication.md).
* Você [configurou](/help/web-sdk/commands/configure/overview.md) corretamente e implantou o SDK da Web nas páginas que deseja personalizar.

## Diagrama de Fluxo {#flow-diagram}

O diagrama de fluxo abaixo descreve a ordem das etapas executadas para fornecer personalização híbrida.

![Diagrama de fluxo visual mostrando a ordem das etapas executadas para fornecer personalização híbrida.](assets/hybrid-personalization-diagram.png)

1. Todos os cookies existentes armazenados anteriormente pelo navegador, com o prefixo `kndctr_`, são incluídos na solicitação do navegador.
1. O navegador da Web do cliente solicita a página da Web do servidor de aplicativos.
1. Quando o servidor de aplicativos recebe a solicitação de página, ele faz uma solicitação `POST` ao [ponto de extremidade de coleta de dados interativa da API do servidor](../../server-api/interactive-data-collection.md) para buscar conteúdo de personalização. A solicitação `POST` contém um `event` e um `query`. Os cookies da etapa anterior, se disponíveis, estão incluídos na matriz `meta>state>entries`.
1. A API do servidor retorna o conteúdo de personalização ao seu servidor de aplicativos.
1. O servidor de aplicativos retorna uma resposta HTML para o navegador cliente, contendo os [cookies de identidade e de cluster](#cookies).
1. Na página do cliente, o comando [!DNL Web SDK] `applyResponse` é chamado, transmitindo os cabeçalhos e o corpo da resposta da [!UICONTROL API do Servidor] da etapa anterior.
1. O [!DNL Web SDK] renderiza ofertas do Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) e itens do Canal da Web do Journey Optimizer automaticamente, porque o sinalizador `renderDecisions` está definido como `true`.
1. As ofertas [!DNL HTML]/[!DNL JSON] baseadas em formulário de destino e as experiências baseadas em código Journey Optimizer são aplicadas manualmente por meio do método `applyProposition`, para atualizar o [!DNL DOM] com base no conteúdo de personalização da proposta.
1. Para ofertas [!DNL HTML]/[!DNL JSON] baseadas em formulário do Target e experiências baseadas em código Journey Optimizer, os eventos de exibição devem ser enviados manualmente para indicar quando o conteúdo retornado foi exibido. Isso é feito por meio do comando `sendEvent`.

## Cookies {#cookies}

Os cookies são usados para manter a identidade do usuário e as informações do cluster.  Ao usar uma implementação híbrida, o servidor de aplicações web manipula o armazenamento e o envio desses cookies durante o ciclo de vida da solicitação.

| Cookie | Finalidade | Armazenado por | Enviado por |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contém detalhes da identidade do usuário. | Servidor de aplicativos | Servidor de aplicativos |
| `kndctr_AdobeOrg_cluster` | Indica qual cluster de Edge Network deve ser usado para atender às solicitações. | Servidor de aplicativos | Servidor de aplicativos |

## Solicitar posicionamento {#request-placement}

As solicitações de API do servidor são necessárias para obter apresentações e enviar uma notificação de exibição. Ao usar uma implementação híbrida, o servidor do aplicativo faz essas solicitações à API do servidor.

| Solicitação | Feito por |
|---|---|
| Solicitação do Interact para recuperar apresentações | Servidor de aplicativos |
| Solicitação do Interact para enviar notificações de exibição | Servidor de aplicativos |

## Implicações do Analytics {#analytics}

Ao implementar a personalização híbrida, você deve prestar atenção especial para que as ocorrências de página não sejam contadas várias vezes no Analytics.

Quando você [configura uma sequência de dados](../../datastreams/overview.md) para o Analytics, os eventos são automaticamente encaminhados para que as ocorrências da página sejam capturadas.

A amostra dessa implementação usa dois fluxos de dados diferentes:

* Uma sequência de dados configurada para o Analytics. Essa sequência de dados é usada para interações do SDK da Web.
* Uma segunda sequência de dados sem uma configuração do Analytics. Essa sequência de dados é usada para solicitações de API do servidor. Você deve configurar essa sequência de dados com a mesma configuração de destino da sequência de dados configurada para o Analytics.

Dessa forma, a solicitação do lado do servidor não registra eventos do Analytics, mas as solicitações do lado do cliente registram. Isso faz com que as solicitações do Analytics sejam contadas com precisão.


## Solicitação do lado do servidor {#server-side-request}

O exemplo de solicitação abaixo ilustra uma solicitação da API do servidor que o servidor de aplicativos poderia usar para recuperar o conteúdo de personalização.

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
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sim. | A ID do fluxo de dados que você usa para transmitir as interações para o Edge Network. Consulte a [visão geral das sequências de dados](../../datastreams/overview.md) para saber como configurar uma sequência de dados. |
| `requestId` | `String` | Não | Uma ID aleatória para correlacionar solicitações internas do servidor. Se nenhum for fornecido, o Edge Network gera um e o retorna na resposta. |

### Resposta do lado do servidor {#server-response}

O exemplo de resposta abaixo mostra como pode ser a resposta da API do servidor.


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
