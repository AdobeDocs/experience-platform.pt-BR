---
title: Coleta de dados interativa
description: Learn how the Adobe Experience Platform Edge Network Server API performs interactive data collection
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs interactive data collection
keywords: coleta de dados, coleta, rede de borda da experience platform, api, coleta de dados interativa
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 7%

---


# Interactive data collection

## Visão geral {#overview}

Os endpoints interativos de coleta de dados recebem um único evento e são usados quando o cliente espera que uma resposta seja retornada pelo servidor da Rede de borda do Adobe Experience Platform. Esses endpoints também podem retornar conteúdo de outros serviços da Experience Edge, enquanto realizam a coleta de dados.

The server response includes one or more `Handle` objects, as shown below.

## API call example

### Formato da API {#format}

```http
POST /ee/v2/interact
```

### Solicitação {#request}

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
               }
            ]
         },
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev/",
               "name": "home-demo-Home Page"
            }
         },
         "timestamp": "2021-08-09T14:09:20.859Z"
      },
      "data": {
         "prop1": "custom value"
      }
   }
}'
```

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sim. | ID do conjunto de dados. |
| `requestId` | `String` | Não | Forneça uma ID aleatória do cliente para correlacionar solicitações internas do servidor. Se nenhum for fornecido, a Edge Network gerará um e o retornará na resposta. |

### Resposta {#response}

A successful response returns HTTP status `200 OK`, with one or more `Handle` objects, depending on the real-time edge services enabled in the datastream configuration.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
