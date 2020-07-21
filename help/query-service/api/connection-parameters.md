---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Query Service
topic: connection parameters
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---


# Parâmetros de conexão

## Chamadas de API de exemplo

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para a [!DNL Query Service] API. As seções a seguir percorrem as várias chamadas de API que podem ser feitas usando a [!DNL Query Service] API. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Solicitar parâmetros de conexão para o serviço interativo

Você pode recuperar seus parâmetros de conexão para usar o serviço [](../creating-queries/writing-queries.md) interativo, fazendo uma solicitação GET ao `/connection_parameters` endpoint. Para obter mais informações sobre clientes que usam parâmetros de conexão para se conectar via serviço interativo, leia a documentação sobre clientes [do Serviço de](../clients/overview.md)Query.

**Formato da API**

```http
GET /connection_parameters
```

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com seus parâmetros de conexão.

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
