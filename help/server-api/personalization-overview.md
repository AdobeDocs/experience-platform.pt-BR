---
title: Visão geral da personalização
description: Saiba como usar a API do servidor de rede de borda da Adobe Experience Platform para recuperar conteúdo personalizado de soluções de personalização Adobe.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 10%

---

# Visão geral da personalização

Com o [!DNL Server API], você poderá recuperar o conteúdo personalizado nas soluções de personalização do Adobe, incluindo [Adobe Target](https://business.adobe.com/br/products/target/adobe-target.html) e [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=pt-BR).

Além disso, a [!DNL Server API] O capacita recursos de personalização de mesma página e próxima página por meio de destinos de personalização do Adobe Experience Platform, como [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) e a variável [conexão de personalização personalizada](../destinations/catalog/personalization/custom-personalization.md). Para saber como configurar o Experience Platform para personalização de mesma página e próxima página, consulte o [guia dedicado](../destinations/ui/activate-edge-personalization-destinations.md).

Ao usar a API do servidor, você deve integrar a resposta fornecida pelo mecanismo de personalização com a lógica usada para renderizar o conteúdo em seu site. Ao contrário do [SDK da Web](../web-sdk/home.md), o [!DNL Server API] não tem um mecanismo para aplicar automaticamente o conteúdo retornado por [!DNL Adobe Target] e [!DNL Offer Decisioning].

## Terminologia {#terminology}

Antes de trabalhar com as soluções de personalização de Adobe, compreenda os seguintes conceitos:

* **Oferta**: uma oferta é uma mensagem de marketing que pode ter regras associadas que especificam quem está qualificado para ver a oferta.
* **Decisão**: uma decisão (anteriormente conhecida como atividade de oferta) informa a seleção de uma oferta.
* **Esquema**: o schema de uma decisão informa o tipo de oferta retornada.
* **Escopo**: O escopo da decisão.
   * No Adobe Target, essa é a variável [!DNL mbox]. A variável [!DNL global mbox] é o `__view__` escopo
   * Para [!DNL Offer Decisioning], essas são as sequências de caracteres codificadas na Base64 do JSON que contêm as IDs de atividade e posicionamento que você deseja que o serviço do offer decisioning use para propor ofertas.

## A variável `query` objeto {#query-object}

A recuperação de conteúdo personalizado requer um objeto de consulta de solicitação explícita para um exemplo de solicitação. O objeto de consulta tem o seguinte formato:

```json
{
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "alloyStore",
            "siteWide",
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}
```

| Atributo | Tipo | Obrigatório / Opcional | Descrição |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Obrigatório para personalização do Target. Opcional para o Offer Decisioning. | Lista de schemas usados na decisão para selecionar o tipo de ofertas retornadas. |
| `scopes` | `String[]` | Opcional | Lista de escopos de decisão. Máximo de 30 por solicitação. |

## O objeto handle {#handle}

O conteúdo personalizado recuperado das soluções de personalização é apresentado em uma `personalization:decisions` que tem o seguinte formato para sua carga:

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| Atributo | Tipo | Descrição |
| --- | --- | --- |
| `payload.id` | String | A ID da decisão. |
| `payload.scope` | String | O escopo de decisão que resultou nas ofertas propostas. |
| `payload.scopeDetails.decisionProvider` | String | Defina como `TGT` ao usar o Adobe Target. |
| `payload.scopeDetails.activity.id` | String | O identificador exclusivo da atividade de oferta. |
| `payload.scopeDetails.experience.id` | String | O identificador exclusivo do posicionamento da oferta. |
| `items[].id` | String | O identificador exclusivo do posicionamento da oferta. |
| `items[].data.id` | String | A ID da oferta proposta. |
| `items[].data.schema` | String | O schema do conteúdo associado à oferta proposta. |
| `items[].data.format` | String | O formato do conteúdo associado à oferta proposta. |
| `items[].data.language` | String | Uma matriz de idiomas associados ao conteúdo da oferta proposta. |
| `items[].data.content` | String | Conteúdo associado à oferta proposta no formato de uma cadeia de caracteres. |
| `items[].data.selector` | String | Seletor de HTML usado para identificar o elemento DOM de destino para uma oferta de ação DOM. |
| `items[].data.prehidingSelector` | String | Seletor de HTML usado para identificar o elemento DOM a ser ocultado ao manipular uma oferta de ação DOM. |
| `items[].data.deliveryUrl` | String | Conteúdo de imagem associado à oferta proposta no formato de um URL. |
| `items[].data.characteristics` | String | Características associadas à oferta proposta no formato de um objeto JSON. |

## Exemplo de chamada de API {#sample-call}

**Formato da API**

```http
POST /ee/v2/interact
```

### Solicitação {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `configId` | String | Sim | A ID do fluxo de dados. |
| `requestId` | String | Não | Forneça uma ID de rastreamento de solicitação externa. Se nenhum for fornecido, a rede de borda gerará um para você e o retornará no corpo/cabeçalhos de resposta. |

### Resposta {#response}

Retorna um `200 OK` e um ou mais `Handle` objetos, dependendo dos serviços de borda ativados na configuração da sequência de dados.

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## Notificações {#notifications}

As notificações devem ser disparadas quando um conteúdo ou uma exibição previamente buscada for visitada ou renderizada para o usuário final. Para que as notificações sejam desativadas para o escopo correto, certifique-se de rastrear os respectivos `id` para cada escopo.

Notificações com a direita `id` para que os escopos correspondentes sejam refletidos corretamente, é necessário acionar.

**Formato da API**

```http
POST /ee/v2/collect
```

### Solicitação {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sim | A ID da sequência de dados usada pelo ponto de extremidade de coleta de dados. |
| `requestId` | `String` | Não | ID de rastreamento de solicitação externa externa. Se nenhum for fornecido, a rede de borda gerará um para você e o retornará no corpo/cabeçalhos de resposta. |
| `silent` | `Boolean` | Não | Parâmetro booliano opcional que indica se a Rede de borda deve retornar um `204 No Content` resposta com uma carga vazia. Erros críticos são relatados usando o código de status HTTP e a carga correspondentes. |

### Resposta {#notifications-response}

Uma resposta bem-sucedida retorna um dos seguintes status, e uma `requestID` se nenhum foi fornecido na solicitação.

* `202 Accepted` quando o pedido foi processado com êxito;
* `204 No Content` quando a solicitação foi processada com êxito e a variável `silent` O parâmetro foi definido como `true`;
* `400 Bad Request` quando a solicitação não foi formada corretamente (por exemplo, a identidade primária obrigatória não foi encontrada).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
