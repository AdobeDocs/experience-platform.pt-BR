---
title: Coleta de dados interativa
description: Saiba como a API do Adobe Experience Platform Edge Network Server executa a coleta de dados interativa.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f8434746c4a023ec895d23a59e04fca4baecfc36
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---

# Coleta de dados interativa

## Visão geral {#overview}

Os pontos de extremidade de coleta de dados interativos recebem um único evento e são usados quando o cliente espera que uma resposta seja retornada pelo servidor de Edge Network do Adobe Experience Platform. Esses endpoints também podem retornar conteúdo de outros serviços Edge Network enquanto executam a coleta de dados.

>[!IMPORTANT]
>
>A variável `/interact` O endpoint foi projetado principalmente para ser usado pelos SDKs do Experience Platform. Esse endpoint está sujeito a alterações aditivas e seu comportamento pode evoluir sem aviso prévio. Por exemplo, novos itens podem ser adicionados à carga de resposta no futuro.

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
