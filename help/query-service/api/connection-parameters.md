---
keywords: Experience Platform;início;tópicos populares;serviço de consulta;guia de api;parâmetros de conexão;Serviço de consulta;
solution: Experience Platform
title: Endpoint da API de Parâmetros de Conexão
description: Você pode recuperar os parâmetros de conexão para usar o serviço interativo fazendo uma solicitação GET para o endpoint /connection_parameters.
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Ponto de extremidade de parâmetros de conexão

## Exemplo de chamada de API

A seção a seguir orienta você pela chamada de API que pode ser feita usando o [!DNL Query Service] API. A chamada inclui o formato geral da API, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Solicitar parâmetros de conexão

Você pode recuperar os parâmetros de conexão fazendo uma solicitação GET para o `/connection_parameters` terminal. Para obter mais informações sobre clientes que usam parâmetros de conexão para se conectar via serviço interativo, leia a documentação em [Clientes do Serviço de consulta](../clients/overview.md).

**Formato da API**

```http
GET /connection_parameters
```

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com os parâmetros de conexão.

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
