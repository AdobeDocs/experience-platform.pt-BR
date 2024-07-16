---
title: Coleção de dados não interativa
description: Saiba como a API do Adobe Experience Platform Edge Network Server executa a coleta de dados não interativa.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---


# Coleção de dados não interativa

## Visão geral {#overview}

Os pontos de extremidade de coleção de dados de evento não interativos são usados para enviar vários eventos para conjuntos de dados de Experience Platform ou outras tomadas.

O envio de eventos em lote é recomendado quando os eventos do usuário final são enfileirados localmente por um curto período de tempo (por exemplo, quando não há conexão de rede).

Os eventos em lote não devem pertencer necessariamente ao mesmo usuário final, o que significa que os eventos podem conter identidades diferentes em seu objeto `identityMap`.

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
| `dataStreamId` | `String` | Sim | A ID da sequência de dados usada pelo ponto de extremidade de coleta de dados. |
| `requestId` | `String` | Não | Forneça uma ID de rastreamento de solicitação externa. Se nenhum for fornecido, o Edge Network gerará um para você e o retornará de volta no corpo/cabeçalhos de resposta. |
| `silent` | `Boolean` | Não | Parâmetro booleano opcional que indica se o Edge Network deve retornar uma resposta `204 No Content` com uma carga vazia ou não. Erros críticos são relatados usando o código de status HTTP e a carga correspondentes. |

### Resposta {#response}

Uma resposta bem-sucedida retorna um dos seguintes status, e um `requestID` se nenhum tiver sido fornecido na solicitação.

* `202 Accepted` quando a solicitação foi processada com êxito;
* `204 No Content` quando a solicitação foi processada com êxito e o parâmetro `silent` foi definido como `true`;
* `400 Bad Request` quando a solicitação não foi formada corretamente (por exemplo, a identidade primária obrigatória não foi encontrada).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
