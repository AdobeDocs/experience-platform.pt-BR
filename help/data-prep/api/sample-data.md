---
keywords: Experience Platform, home, tópicos populares, preparação de dados, guia da api, dados de amostra;
solution: Experience Platform
title: Endpoint da API de dados de exemplo
topic: dados de amostra
description: 'Você pode usar o terminal `/samples na API do Adobe Experience Platform para recuperar, criar, atualizar e validar programaticamente os dados de amostra do mapeamento. '
translation-type: tm+mt
source-git-commit: a2c966ae2401faa572cbba974ce6f572d5280a8f
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 4%

---


# Ponto de extremidade de dados de amostra

Dados de amostra podem ser usados ao criar um esquema para seu conjunto de mapeamento. Você pode usar o terminal `/samples` na API de Preparação de dados para recuperar, criar e atualizar programaticamente os dados de amostra.

## Listar dados de amostra

Você pode recuperar uma lista de todos os dados de amostra do mapeamento para sua Organização IMS fazendo uma solicitação de GET para o endpoint `/samples`.

**Formato da API**

O ponto de extremidade `/samples` oferece suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Atualmente, você deve incluir os parâmetros `start` e `limit` como parte de sua solicitação.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{LIMIT}` | **Obrigatório**. Especifica o número de dados de amostra de mapeamento retornados. |
| `{START}` | **Obrigatório**. Especifica o deslocamento das páginas de resultados. Para obter a primeira página de resultados, defina o valor como `start=0`. |

**Solicitação**

A solicitação a seguir recuperará os dois últimos dados de amostra de mapeamento na organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre os dois últimos objetos de mapeamento de dados de amostra.

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `sampleData` |  |
| `sampleType` |  |

## Criar dados de amostra

Você pode criar dados de amostra fazendo uma solicitação POST para o endpoint `/samples`.

```http
POST /samples
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre seus dados de amostra recém-criados.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Criar dados de amostra fazendo upload de um arquivo

Você pode criar dados de amostra usando um arquivo, fazendo uma solicitação de POST ao endpoint `/samples/upload`.

**Formato da API**

```http
POST /samples/upload
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre seus dados de amostra recém-criados.

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Pesquisar um objeto de dados de amostra específico

Você pode pesquisar um objeto específico de dados de amostra fornecendo a ID no caminho de uma solicitação do GET para o endpoint `/samples`.

**Formato da API**

```http
GET /samples/{SAMPLE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SAMPLE_ID}` | A ID do objeto de dados de amostra que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações do objeto de dados de amostra que você deseja recuperar.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Atualizar dados de amostra

É possível atualizar um objeto de dados de amostra específico fornecendo a ID no caminho de uma solicitação PUT para o endpoint `/samples`.

**Formato da API**

```http
PUT /samples/{SAMPLE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SAMPLE_ID}` | A ID do objeto de dados de amostra que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza os dados de amostra especificados. Especificamente, ele atualiza o sobrenome de &quot;Smith&quot; para &quot;Lee&quot;.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre os dados de amostra atualizados.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
