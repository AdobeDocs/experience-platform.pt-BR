---
title: Personalização via Offer Decisioning
description: Saiba como usar a API do servidor para fornecer e renderizar experiências personalizadas por meio do Offer Decisioning.
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# Personalização via Offer Decisioning

## Visão geral {#overview}

A API do servidor de rede de borda pode fornecer experiências personalizadas gerenciadas no [Offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) ao canal da web.

[!DNL Offer Decisioning] O é compatível com uma interface não visual para criar, ativar e fornecer suas atividades e experiências de personalização.

## Configurar o fluxo de dados {#configure-your-datastream}

Antes de usar a API do servidor em conjunto com o Offer Decisioning, é necessário habilitar a personalização do Adobe Experience Platform na configuração do fluxo de dados e habilitar a **[!UICONTROL Offer decisioning]** opção.

Consulte a [guia sobre como adicionar serviços a um fluxo de dados](../edge/datastreams/overview.md#adobe-experience-platform-settings), para obter informações detalhadas sobre como ativar o Offer Decisioning.

![Imagem da interface do usuário mostrando a tela de configuração do serviço de sequência de dados, com o Offer Decisioning selecionado](assets/aep-od-datastream.png)

## Criação de público {#audience-creation}

[!DNL Offer Decisioning] O depende do Serviço de segmentação da Adobe Experience Platform para a criação de públicos-alvo. Você pode encontrar a documentação para o [!DNL Segmentation Service] [aqui](../segmentation/home.md).

## Definição de escopos de decisão {#creating-decision-scopes}

A variável [!DNL Offer Decision Engine] usa dados do Adobe Experience Platform e [Perfis de clientes em tempo real](../profile/home.md), juntamente com o [!DNL Offer Library], para fornecer ofertas aos clientes e canais certos na hora certa.

Para saber mais sobre o [!DNL Offer Decisioning Engine], consulte a seção dedicada [documentação](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=pt-BR).

Depois [configuração do seu fluxo de dados](#configure-your-datastream), você deve definir os escopos de decisão que serão usados na campanha de personalização.

[Escopos de decisão](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes) são as cadeias de caracteres JSON codificadas na Base64 que contêm as IDs de atividade e posicionamento que você deseja que o [!DNL Offer Decisioning Service] para usar ao propor ofertas.

**Escopo de decisão JSON**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**String codificada na Base64 do escopo de decisão**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

Após criar as ofertas e coleções, é necessário definir um [escopo da decisão](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes).

Copie o escopo de decisão codificado na Base64. Você o usará no `query` objeto da solicitação de API do servidor.

![Imagem da interface do usuário mostrando a interface do usuário do Offer Decisioning, destacando o escopo da decisão.](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## Exemplo de chamada de API {#api-example}

**Formato da API**

```http
POST /ee/v2/interact
```

### Solicitação {#request}

Uma solicitação completa que inclui um objeto XDM completo, um objeto de dados e uma consulta de Offer decisioning é descrita abaixo.

>[!NOTE]
>
>A variável `xdm` e `data` objetos são opcionais e só são necessários para o Offer Decisioning se você tiver criado segmentos com condições que usam campos em qualquer um desses objetos.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
            "web": {
                "webPageDetails": {
                    "URL": "https://alloystore.dev",
                    "name": "Home Page"
                },
                "webReferrer": {
                    "URL": ""
                }
            },
            "device": {
                "screenHeight": 1440,
                "screenWidth": 3440,
                "screenOrientation": "landscape"
            },
            "environment": {
                "type": "browser",
                "browserDetails": {
                    "viewportWidth": 3440,
                    "viewportHeight": 1440
                }
            },
            "placeContext": {
                "localTime": "2022-03-22T22:45:21.193-06:00",
                "localTimezoneOffset": 360
            },
            "timestamp": "2022-03-23T04:45:21.193Z",
            "implementationDetails": {
                "name": "https://ns.adobe.com/experience/alloy/reactor",
                "version": "1.0",
                "environment": "serverapi"
            }
        },
        "data": {
            "page": {
                "pageInfo": {
                    "pageName": "Promotions",
                    "siteSection": "Home"
                },
                "promos": {
                    "heroPromos": "purse,shoes,sunglasses"
                },
                "customVariables": {
                    "testGroup": "orange/black theme"
                },
                "events": {
                    "homePage": true
                },
                "products": [
                    {
                        "productSKU": "abc123",
                        "productName": "shirt"
                    }
                ]
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### Resposta {#response}

A rede de borda retornará uma resposta semelhante à mostrada abaixo.

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Se o visitante se qualificar para uma atividade de personalização com base nos dados enviados para o [!DNL Offer Decisioning], o conteúdo de atividade relevante será encontrado no `handle` objeto, em que o tipo é `personalization:decisions`.

Outro conteúdo será retornado na variável `handle` também. Outros tipos de conteúdo não são relevantes para [!DNL Offer Decisioning] personalização. Se o visitante se qualificar para várias atividades, elas estarão contidas em uma matriz.

A tabela abaixo explica os principais elementos dessa parte da resposta.

| Propriedade | Descrição | Exemplo |
|---|---|---|
| `scope` | O escopo de decisão associado às ofertas propostas que foram retornadas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | O identificador exclusivo da atividade de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | O identificador exclusivo do posicionamento da oferta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | O identificador exclusivo da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | O schema do conteúdo associado à oferta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | O identificador exclusivo da oferta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | O formato do conteúdo associado à oferta proposta. | `"format": "text/html"` |
| `language` | Uma matriz de idiomas associados ao conteúdo da oferta proposta. | `"language": [ "en-US" ]` |
| `content` | Conteúdo associado à oferta proposta no formato de uma cadeia de caracteres. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Conteúdo de imagem associado à oferta proposta no formato de um URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Objeto JSON que contém as características associadas à oferta proposta. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
