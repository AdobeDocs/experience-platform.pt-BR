---
title: Coleta de dados interativa
description: Saiba como a API do servidor de rede de borda do Adobe Experience Platform executa a coleta de dados interativa
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs interactive data collection
keywords: coleta de dados, coleta, rede de borda da experience platform, api, coleta de dados interativa
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: 0dce36d690cbe0b666bf30acfa69f52a8c6cac57
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 7%

---

# Coleta de dados interativa

## Visão geral {#overview}

Os endpoints interativos de coleta de dados recebem um único evento e são usados quando o cliente espera que uma resposta seja retornada pelo servidor da Rede de borda do Adobe Experience Platform. Esses endpoints também podem retornar conteúdo de outros serviços da Experience Edge, enquanto realizam a coleta de dados.

A resposta do servidor inclui um ou mais `Handle` como mostrado abaixo.

## Exemplo de chamada de API

### Formato da API {#format}

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

Uma resposta bem-sucedida retorna o status HTTP `200 OK`com um ou mais `Handle` objetos, dependendo dos serviços de borda em tempo real habilitados na configuração do conjunto de dados.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
