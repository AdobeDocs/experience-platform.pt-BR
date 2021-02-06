---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: Endpoint da API Parâmetros de Conexão
topic: connection parameters
description: Você pode recuperar seus parâmetros de conexão para usar o serviço interativo, fazendo uma solicitação de GET para o terminal /connection_parameters.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 1%

---


# Ponto final dos parâmetros de conexão

## Chamadas de API de exemplo

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para a API [!DNL Query Service]. As seções a seguir percorrem as várias chamadas de API que podem ser feitas usando a API [!DNL Query Service]. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Solicitar parâmetros de conexão

Você pode recuperar seus parâmetros de conexão fazendo uma solicitação de GET para o terminal `/connection_parameters`. Para obter mais informações sobre clientes que usam parâmetros de conexão para se conectar via serviço interativo, leia a documentação em [clientes do Serviço de Query](../clients/overview.md).

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
