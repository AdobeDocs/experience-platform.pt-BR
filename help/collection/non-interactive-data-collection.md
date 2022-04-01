---
title: Coleta de dados não interativa
description: Saiba como a API do servidor de rede de borda do Adobe Experience Platform executa a coleta de dados não interativa
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs non-interactive data collection
keywords: coleta de dados, coleta, rede de borda da adobe experience platform, api, coleta de dados não interativa
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---


# Coleta de dados não interativa

## Visão geral {#overview}

Os endpoints não interativos de coleta de dados do evento são usados para enviar vários eventos para conjuntos de dados do Experience Platform ou outros canais.

O envio de eventos em lote é recomendado quando os eventos do usuário final são enfileirados localmente por um curto período de tempo (por exemplo, quando não há conexão de rede).

Os eventos em lote não devem pertencer necessariamente ao mesmo usuário final, o que significa que os eventos podem ter identidades diferentes em seus `identityMap` objeto.


<!-- However, when an `ECID` identity is sent via a cookie or metadata (in Edge Network accepted format), the Edge Network will read it and associate it with each event in the batch.

Each event should include the corresponding `XDM` content that needs to be collected.

>[!NOTE]
>
>[Experience Edge Identity Protocol](visitor-identification.md#experience-edge-identity-protocol) (`ECID` generation) is not applicable for data collection requests, meaning that events sent to this API should already have at least one identity associated to them. For server datastreams (calls to `server.adobedc.net`), the API requires that each event contains an identity **explicitly set as primary**. For device datastreams, the Edge Network will attempt to set the `ECID` as primary, when it is present, and no other primary identity is explicitly set.

-->

## Exemplo de chamada de API não interativa {#example}

### Formato da API {#api-format}

```http
POST /ee/v2/collect
```

### Solicitação {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
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
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sim | A ID do armazenamento de dados usada pelo endpoint da coleta de dados. |
| `requestId` | `String` | Não | Forneça uma ID de rastreamento de solicitação externa. Se nenhum for fornecido, a Edge Network gerará um para você e o retornará aos cabeçalhos/corpo da resposta. |
| `silent` | `Boolean` | Não | Parâmetro booleano opcional que indica se a Rede de Borda deve retornar um `204 No Content` com uma carga vazia ou não. Erros críticos são relatados usando o código de status HTTP e a carga útil correspondentes. |


### Resposta {#response}

Uma resposta bem-sucedida retorna um dos seguintes status e um `requestID` se nenhum tiver sido fornecido na solicitação.

* `202 Accepted` quando o pedido foi processado com êxito;
* `204 No Content` quando a solicitação foi processada com êxito e o `silent` foi definido como `true`;
* `400 Bad Request` quando a solicitação não foi formada corretamente (por exemplo, a identidade primária obrigatória não foi encontrada).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
