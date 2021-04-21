---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, guia de api, parâmetros de conexão, serviço de query;
solution: Experience Platform
title: Endpoint da API Parâmetros de conexão
topic-legacy: connection parameters
description: Você pode recuperar os parâmetros de conexão para usar o serviço interativo, fazendo uma solicitação GET para o endpoint /connection_parameters .
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 1%

---

# Ponto final de parâmetros de conexão

## Exemplos de chamadas de API

Agora que você sabe quais cabeçalhos usar, está pronto para começar a fazer chamadas para a API [!DNL Query Service]. As seções a seguir abordam as várias chamadas de API que podem ser feitas usando a API [!DNL Query Service]. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e uma resposta de amostra.

### Solicitar parâmetros de conexão

Você pode recuperar os parâmetros de conexão fazendo uma solicitação GET para o endpoint `/connection_parameters`. Para obter mais informações sobre clientes que usam parâmetros de conexão para se conectar via serviço interativo, leia a documentação em [Clientes do Serviço de Consulta](../clients/overview.md).

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
