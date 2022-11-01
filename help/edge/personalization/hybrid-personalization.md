---
title: Personalização híbrida usando o SDK da Web e a API do servidor de rede de borda
description: Este artigo demonstra como você pode usar o SDK da Web em conjunto com a API do servidor para implantar personalização híbrida em suas propriedades da Web.
keywords: personalização; híbrido; api do servidor; lado do servidor; aplicação híbrida;
source-git-commit: f280d4cbcde434ccf36df37e95f1902cfd02c96c
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---


# Personalização híbrida usando o SDK da Web e a API do servidor de rede de borda

## Visão geral {#overview}

A personalização Hybdrid descreve o processo de recuperação do conteúdo de personalização no lado do servidor, usando o [API do Servidor de Rede de Borda](../..//server-api/overview.md)e renderizando no lado do cliente, usando o [Web SDK](../home.md).

Você pode usar a personalização híbrida com soluções de personalização como o Adobe Target ou o Offer Decisioning, sendo a diferença o conteúdo da variável [!UICONTROL API do servidor] carga.

## Pré-requisitos {#prerequisites}

Antes de implementar a personalização híbrida em suas propriedades da Web, verifique se você atende às seguintes condições:

* Você decidiu qual solução de personalização deseja usar. Isso terá impacto no conteúdo da variável [!UICONTROL API do servidor] carga.
* Você tem acesso a um servidor de aplicativos que pode ser usado para fazer o [!UICONTROL API do servidor] chamadas .
* Você tem acesso ao [API do Servidor de Rede de Borda](../../server-api/authentication.md).
* Você possui corretamente [configurado e implantado](../fundamentals/configuring-the-sdk.md) SDK da Web nas páginas que você deseja personalizar.

## Diagrama de fluxo {#flow-diagram}

O diagrama de fluxo abaixo descreve a ordem das etapas tomadas para fornecer personalização híbrida.

![O diagrama do fluxo visual mostrando a ordem das etapas tomadas para fornecer personalização híbrida.](assets/hybrid-personalization-diagram.png)

1. Todos os cookies existentes armazenados anteriormente pelo navegador, com o prefixo `kndctr_`, estão incluídos na solicitação do navegador.
1. O navegador da Web cliente solicita a página da Web do servidor de aplicativos.
1. Quando o servidor de aplicativos recebe a solicitação de página, ele faz uma `POST` à [Ponto de extremidade da coleta de dados interativa da API do servidor](../../server-api/interactive-data-collection.md) para buscar conteúdo de personalização. O `POST` a solicitação contém um `event` e `query`. Os cookies da etapa anterior, se disponíveis, são incluídos na variável `meta>state>entries` matriz.
1. A API do servidor retorna o conteúdo de personalização para o servidor de aplicativos.
1. O servidor de aplicativos retorna uma resposta de HTML para o navegador cliente, contendo a variável [cookies de identidade e cluster](#cookies).
1. Na página do cliente, a variável [!DNL Web SDK] `applyResponse` é chamado, transmitindo os cabeçalhos e o corpo do [!UICONTROL API do servidor] da etapa anterior.
1. O [!DNL Web SDK] renderiza o carregamento da página [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) O oferece automaticamente, pois a variável `renderDecisions` sinalizador está definido como `true`.
1. Baseado em formulário [!DNL JSON] as ofertas são aplicadas manualmente por meio da variável `applyPersonalization` , para atualizar a [!DNL DOM] com base na oferta de personalização.
1. Para atividades baseadas em formulário, os eventos de exibição devem ser enviados manualmente para indicar quando a oferta foi exibida. Isso é feito por meio da variável `sendEvent` comando.

## Cookies {#cookies}

Os cookies são usados para persistir a identidade do usuário e as informações do cluster.  Ao usar uma implementação híbrida, o servidor de aplicativos Web manipula o armazenamento e o envio desses cookies durante o ciclo de vida da solicitação.

| Cookie | Propósito | Armazenado por | Enviado por |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contém detalhes de identidade do usuário. | Servidor de aplicativos | Servidor de aplicativos |
| `kndctr_AdobeOrg_cluster` | Indica qual cluster de Rede de Borda deve ser usado para atender às solicitações. | Servidor de aplicativos | Servidor de aplicativos |

## Solicitar posicionamento {#request-placement}

As solicitações da API do servidor são necessárias para obter apresentações e enviar uma notificação de exibição. Ao usar uma implementação híbrida, o servidor de aplicativos faz essas solicitações à API do Servidor.

| Solicitação | Feito por |
|---|---|
| Solicitação de interação para recuperar apresentações | Servidor de aplicativos |
| Solicitação de interação para enviar notificações de exibição | Servidor de aplicativos |

## Implicações do Analytics {#analytics}

Ao implementar a personalização híbrida, você deve prestar atenção especial para que as ocorrências de página não sejam contadas várias vezes no Analytics.

Quando você [configurar um conjunto de dados](../datastreams/overview.md) para o Analytics, os eventos são encaminhados automaticamente para que as ocorrências de página sejam capturadas.

O exemplo dessa implementação usa dois conjuntos de dados diferentes:

* Um conjunto de dados configurado para o Analytics. Esse armazenamento de dados é usado para interações com o SDK da Web.
* Um segundo armazenamento de dados sem uma configuração do Analytics. Esse armazenamento de dados é usado para solicitações de API do servidor.

Dessa forma, a solicitação do lado do servidor não registra nenhum evento do Analytics, mas as solicitações do lado do cliente registram. Isso faz com que as solicitações do Analytics sejam contadas com precisão.


## Solicitação do lado do servidor {#server-side-request}

A solicitação de exemplo abaixo ilustra uma solicitação de API de servidor que o servidor de aplicativos pode usar para recuperar o conteúdo de personalização.

>[!IMPORTANT]
>
>Essa solicitação de exemplo usa o Adobe Target como uma solução de personalização. Sua solicitação pode variar de acordo com a solução de personalização escolhida.


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
| `dataStreamId` | `String` | Sim. | A ID do armazenamento de dados que você usa para transmitir as interações para a Rede de borda. Consulte a [visão geral dos datastreams](../datastreams/overview.md) para saber como configurar um armazenamento de dados. |
| `requestId` | `String` | Não | Uma ID aleatória para correlacionar solicitações internas do servidor. Se nenhum for fornecido, a Edge Network gerará um e o retornará na resposta. |

### Resposta do lado do servidor {#server-response}

O exemplo de resposta abaixo mostra como a resposta da API do servidor pode ser.


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

Baseado em formulário [!DNL JSON] as ofertas são aplicadas manualmente por meio da variável `applyPersonalization` , para atualizar a [!DNL DOM] com base na oferta de personalização. Para atividades baseadas em formulário, os eventos de exibição devem ser enviados manualmente para indicar quando a oferta foi exibida. Isso é feito por meio da variável `sendEvent` comando.

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

## Exemplo de aplicativo {#sample-app}

Para ajudar você a testar e saber mais sobre esse tipo de personalização, fornecemos um aplicativo de amostra que pode ser baixado e usado para testes. Você pode baixar o aplicativo, juntamente com instruções detalhadas sobre como usá-lo, a partir desta [Repositório GitHub](https://github.com/adobe/alloy-samples).






