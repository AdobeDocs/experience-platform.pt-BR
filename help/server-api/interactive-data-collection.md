---
title: Coleta de dados interativa
description: Saiba como a API do servidor de rede de borda da Adobe Experience Platform realiza a coleta interativa de dados.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 7%

---

# Coleta de dados interativa

## Visão geral {#overview}

Os pontos de extremidade de coleta de dados interativos recebem um único evento e são usados quando o cliente espera que uma resposta seja retornada pelo servidor da Rede de borda da Adobe Experience Platform. Esses endpoints também podem retornar conteúdo de outros serviços da rede de borda ao realizar a coleta de dados.

A resposta do servidor inclui um ou mais `Handle` objetos, conforme mostrado abaixo.

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
| `dataStreamId` | `String` | Sim. | ID da sequência de dados. |
| `requestId` | `String` | Não | Forneça uma ID aleatória do cliente para correlacionar solicitações internas do servidor. Se nenhum for fornecido, a rede de borda gerará um e o retornará na resposta. |

### Resposta {#response}

Uma resposta bem-sucedida retorna o status HTTP `200 OK`, com um ou mais `Handle` objetos, dependendo dos serviços de borda em tempo real ativados na configuração da sequência de dados.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
