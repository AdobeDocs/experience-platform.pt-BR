---
title: Interação com a Adobe Analytics
description: Saiba como usar a API do Edge Network Server para interagir com o Adobe Analytics
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Analytics
keywords: recolha de dados; Saída; análises; api de rede de borda da Adobe Experience Platform; analytics
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---


# Interação com a Adobe Analytics

## Visão geral {#overview}

A coleta de dados do Adobe Analytics funciona ao traduzir dados XDM em um formato que a Adobe Analytics pode entender. Vários campos XDM são [mapeado automaticamente](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) para variáveis do Analytics.

Você também pode [mapear manualmente valores XDM](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) para variáveis herdadas do Analytics.

Para permitir que o Adobe Analytics receba dados da API do servidor, é necessário [configurar seu conjunto de dados](../edge/fundamentals/datastreams.md#adobe-analytics-settings) para encaminhar eventos para o Adobe Analytics, inserindo a ID do conjunto de relatórios na página de configuração do conjunto de dados.

![Configuração de fluxo de dados do Adobe Analytics](assets/analytics-datastream.png)

## Interação com a Adobe Analytics {#interacting-analytics}

### Formato da API {#format}

```http
POST https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Solicitação {#request}

A amostra abaixo inclui vários valores mapeados automaticamente do `_experience.analytics` grupo de campos. Também inclui camadas de dados baseadas em JSON. Embora essas camadas de dados não possam ser mapeadas automaticamente, é possível usar [Preparação de dados para coleta de dados](../edge/fundamentals/datastreams.md#data-prep) para mapear esses valores para um schema que contenha grupos de campos referenciados acima.

Todos os valores que os usuários mapeiam para esses campos serão mapeados automaticamente para os valores adequados do Analytics, como se fossem incluídos na solicitação da API.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
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
