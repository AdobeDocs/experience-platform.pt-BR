---
title: Interação com o Adobe Analytics
description: Saiba como usar a API do servidor Edge Network para interagir com o Adobe Analytics.
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 5de1ec17b78c97be21c0d2afd6f0b119a6074b6f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Interação com o Adobe Analytics

## Visão geral {#overview}

A coleção de dados do Adobe Analytics funciona traduzindo dados XDM em um formato que o Adobe Analytics pode entender. Vários campos XDM são [mapeados automaticamente](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html) para variáveis do Analytics. Você também pode mapear manualmente valores XDM para variáveis herdadas do Analytics.

Para permitir que o Adobe Analytics receba dados da API do Servidor, você precisa [configurar sua sequência de dados](../datastreams/overview.md#adobe-analytics-settings) para encaminhar eventos para o Adobe Analytics, inserindo a ID do conjunto de relatórios na página de configuração da sequência de dados.

![Configuração da sequência de dados do Adobe Analytics](assets/analytics-datastream.png)

## Interação com o Adobe Analytics {#interacting-analytics}

### Formato da API {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Solicitação {#request}

A amostra abaixo inclui vários valores mapeados automaticamente do grupo de campos `_experience.analytics`. Também inclui camadas de dados baseadas em JSON. Embora essas camadas de dados não possam ser mapeadas automaticamente, é possível usar o [Preparo de Dados para a Coleção de Dados](../datastreams/data-prep.md) para mapear esses valores para um esquema que contenha os grupos de campos mencionados acima.

Todos os valores que os usuários mapeiam para esses campos serão mapeados automaticamente para os valores apropriados do Analytics, como se tivessem sido incluídos na solicitação da API.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
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
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
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
      }
   }
}'
```

### Resposta {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
