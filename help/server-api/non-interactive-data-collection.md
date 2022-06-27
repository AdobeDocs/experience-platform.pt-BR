---
title: Coleta de dados não interativa
description: Saiba como a API do servidor de rede de borda do Adobe Experience Platform executa a coleta de dados não interativa.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 5%

---

# Coleta de dados não interativa

## Visão geral {#overview}

Os endpoints não interativos de coleta de dados do evento são usados para enviar vários eventos para conjuntos de dados do Experience Platform ou outros canais.

O envio de eventos em lote é recomendado quando os eventos do usuário final são enfileirados localmente por um curto período de tempo (por exemplo, quando não há conexão de rede).

Os eventos em lote não devem pertencer necessariamente ao mesmo usuário final, o que significa que os eventos podem ter identidades diferentes em seus `identityMap` objeto.

## Exemplo de chamada de API não interativa {#example}

### Formato da API {#api-format}

```http
POST /ee/v2/collect
```

### Solicitação {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
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
