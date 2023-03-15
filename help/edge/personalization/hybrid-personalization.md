---
title: Personalização híbrida usando o SDK da Web e a API do servidor de rede de borda
description: Este artigo demonstra como você pode usar o SDK da Web em conjunto com a API do servidor para implantar personalização híbrida em suas propriedades da Web.
keywords: personalização; híbrido; api do servidor; lado do servidor; implementação híbrida;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---

# Personalização híbrida usando o SDK da Web e a API do servidor de rede de borda

## Visão geral {#overview}

A personalização híbrida descreve o processo de recuperação de conteúdo de personalização no lado do servidor, usando o [API do servidor de rede de borda](../..//server-api/overview.md)e renderizá-lo no lado do cliente, usando o [SDK da Web](../home.md).

Você pode usar a personalização híbrida com soluções de personalização como o Adobe Target ou o Offer Decisioning, sendo a diferença o conteúdo da [!UICONTROL API do servidor] carga útil.

## Pré-requisitos {#prerequisites}

Antes de implementar a personalização híbrida em suas propriedades da Web, verifique se você atende às seguintes condições:

* Você decidiu qual solução de personalização deseja usar. Tal terá um impacto sobre o conteúdo da [!UICONTROL API do servidor] carga útil.
* Você tem acesso a um servidor de aplicativos que pode usar para fazer com que [!UICONTROL API do servidor] chamadas.
* Você tem acesso ao [API do servidor de rede de borda](../../server-api/authentication.md).
* Você fez corretamente [configurado e implantado](../fundamentals/configuring-the-sdk.md) SDK da Web nas páginas que você deseja personalizar.

## Diagrama de Fluxo {#flow-diagram}

O diagrama de fluxo abaixo descreve a ordem das etapas executadas para fornecer personalização híbrida.

![Diagrama de fluxo visual mostrando a ordem das etapas executadas para fornecer personalização híbrida.](assets/hybrid-personalization-diagram.png)

1. Todos os cookies existentes armazenados anteriormente pelo navegador, com o prefixo `kndctr_`, estão incluídos na solicitação do navegador.
1. O navegador da Web do cliente solicita a página da Web do servidor de aplicativos.
1. Quando o servidor de aplicativos recebe a solicitação de página, ele faz uma `POST` solicitação à [Ponto de extremidade de coleção de dados interativos da API do servidor](../../server-api/interactive-data-collection.md) para buscar conteúdo de personalização. A variável `POST` contém um `event` e uma `query`. Os cookies da etapa anterior, se disponíveis, estão incluídos na variável `meta>state>entries` matriz.
1. A API do servidor retorna o conteúdo de personalização ao seu servidor de aplicativos.
1. O servidor de aplicativos retorna uma resposta de HTML para o navegador do cliente, contendo o [identidade e cookies de cluster](#cookies).
1. Na página do cliente, a variável [!DNL Web SDK] `applyResponse` é chamado, transmitindo os cabeçalhos e o corpo da variável [!UICONTROL API do servidor] resposta da etapa anterior.
1. A variável [!DNL Web SDK] renderiza o carregamento da página [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) O oferece automaticamente, pois a variável `renderDecisions` o sinalizador está definido como `true`.
1. Baseado em formulário [!DNL JSON] as ofertas são aplicadas manualmente por meio do `applyPersonalization` para atualizar o [!DNL DOM] com base na oferta de personalização.
1. Para atividades baseadas em formulário, os eventos de exibição devem ser enviados manualmente para indicar quando a oferta foi exibida. Isso é feito por meio da `sendEvent` comando.

## Cookies {#cookies}

Os cookies são usados para manter a identidade do usuário e as informações do cluster.  Ao usar uma implementação híbrida, o servidor de aplicações web manipula o armazenamento e o envio desses cookies durante o ciclo de vida da solicitação.

| Cookie | Propósito | Armazenado por | Enviado por |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contém detalhes da identidade do usuário. | Servidor de aplicativos | Servidor de aplicativos |
| `kndctr_AdobeOrg_cluster` | Indica qual cluster da Rede de Borda deve ser usado para atender às solicitações. | Servidor de aplicativos | Servidor de aplicativos |

## Solicitar posicionamento {#request-placement}

As solicitações de API do servidor são necessárias para obter apresentações e enviar uma notificação de exibição. Ao usar uma implementação híbrida, o servidor do aplicativo faz essas solicitações à API do servidor.

| Solicitação | Feito por |
|---|---|
| Solicitação do Interact para recuperar apresentações | Servidor de aplicativos |
| Solicitação do Interact para enviar notificações de exibição | Servidor de aplicativos |

## Implicações do Analytics {#analytics}

Ao implementar a personalização híbrida, você deve prestar atenção especial para que as ocorrências de página não sejam contadas várias vezes no Analytics.

Quando você [configurar um fluxo de dados](../datastreams/overview.md) no Analytics, os eventos são encaminhados automaticamente para que as ocorrências de página sejam capturadas.

A amostra dessa implementação usa dois fluxos de dados diferentes:

* Uma sequência de dados configurada para o Analytics. Essa sequência de dados é usada para interações do SDK da Web.
* Uma segunda sequência de dados sem uma configuração do Analytics. Essa sequência de dados é usada para solicitações de API do servidor.

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
| `dataStreamId` | `String` | Sim. | A ID do fluxo de dados que você usa para transmitir as interações para a Rede de borda. Consulte a [visão geral dos fluxos de dados](../datastreams/overview.md) para saber como configurar um fluxo de dados. |
| `requestId` | `String` | Não | Uma ID aleatória para correlacionar solicitações internas do servidor. Se nenhum for fornecido, a rede de borda gerará um e o retornará na resposta. |

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

Na página do cliente, a variável [!DNL Web SDK] `applyResponse` é chamado, transmitindo os cabeçalhos e o corpo da resposta do lado do servidor.

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

Baseado em formulário [!DNL JSON] as ofertas são aplicadas manualmente por meio do `applyPersonalization` para atualizar o [!DNL DOM] com base na oferta de personalização. Para atividades baseadas em formulário, os eventos de exibição devem ser enviados manualmente para indicar quando a oferta foi exibida. Isso é feito por meio da `sendEvent` comando.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## Aplicativo de amostra {#sample-app}

Para ajudá-lo a experimentar e saber mais sobre esse tipo de personalização, fornecemos um aplicativo de amostra que você pode baixar e usar para testes. Você pode baixar o aplicativo e fornecer instruções detalhadas sobre como usá-lo a partir deste [Repositório do GitHub](https://github.com/adobe/alloy-samples).
