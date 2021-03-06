---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, guia de api, consultas, query, serviço de query;
solution: Experience Platform
title: Ponto de Extremidade da API de Consultas
topic-legacy: queries
description: As seções a seguir abordam as chamadas que você pode fazer usando o endpoint /queries na API do Serviço de query.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 4%

---

# Ponto de extremidade de consultas

## Exemplos de chamadas à API

As seções a seguir abordam as chamadas que você pode fazer usando o `/queries` endpoint no [!DNL Query Service] API. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e uma resposta de amostra.

### Recuperar uma lista de consultas

Você pode recuperar uma lista de todas as consultas da Organização IMS fazendo uma solicitação do GET para a `/queries` endpoint .

**Formato da API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`). Os parâmetros disponíveis estão listados abaixo.

**Parâmetros de consulta**

Veja a seguir uma lista de parâmetros de query disponíveis para listar queries. Todos esses parâmetros são opcionais. Fazer uma chamada para esse terminal sem parâmetros recuperará todas as consultas disponíveis para sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar os resultados. Os campos compatíveis são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados por criados em ordem crescente. Adicionar um `-` antes de criar (`orderby=-created`) classificará os itens por criados em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20º*) |
| `start` | Desloca a lista de resposta usando a numeração baseada em zero. Por exemplo, `start=2` retornará uma lista a partir da terceira query listada. (*Valor padrão: 0*) |
| `property` | Filtre os resultados com base nos campos. Os filtros **must** ser HTML escapado. Vírgulas são usadas para combinar vários conjuntos de filtros. Os campos compatíveis são `created`, `updated`, `state`e `id`. A lista de operadores compatíveis é `>` (maior que), `<` (inferior a), `>=` (maior ou igual a), `<=` (menor que ou igual a), `==` (igual a), `!=` (não igual a), e `~` (contém). Por exemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retornará todas as consultas com a ID especificada. |
| `excludeSoftDeleted` | Indica se uma consulta que foi excluída de forma flexível deve ser incluída. Por exemplo, `excludeSoftDeleted=false` will **incluir** consultas excluídas por software. (*Booleano, valor padrão: true*) |
| `excludeHidden` | Indica se consultas não orientadas por usuários devem ser exibidas. Ter este valor definido como false **incluir** consultas não orientadas por usuários, como definições CURSOR, FETCH ou consultas de metadados. (*Booleano, valor padrão: true*) |

**Solicitação**

A solicitação a seguir recupera a consulta mais recente criada para a organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de consultas para a Organização IMS especificada como JSON. A resposta a seguir retorna a consulta mais recente criada para a organização IMS.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### Criar uma consulta

Você pode criar um novo query fazendo uma solicitação POST para a variável `/queries` endpoint .

**Formato da API**

```http
POST /queries
```

**Solicitação**

A solicitação a seguir cria um novo query, configurado pelos valores fornecidos no payload:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| Propriedade | Descrição |
| -------- | ----------- |
| `dbName` | O nome do banco de dados para o qual você está criando uma consulta SQL. |
| `sql` | A consulta SQL que você deseja criar. |
| `name` | O nome da sua consulta SQL. |
| `description` | A descrição da sua consulta SQL. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com detalhes da sua query recém-criada. Quando o query terminar de ativar e for executado com êxito, a variável `state` mudará de `SUBMITTED` para `SUCCESS`.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.cancel` para [cancelar a consulta criada](#cancel-a-query).

### Recuperar uma consulta por ID

Você pode recuperar informações detalhadas sobre um query específico fazendo uma solicitação do GET para o `/queries` e fornecer o `id` no caminho da solicitação.

**Formato da API**

```http
GET /queries/{QUERY_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_ID}` | O `id` do query que deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a consulta especificada.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.cancel` para [cancelar a consulta criada](#cancel-a-query).

### Cancelar uma consulta

Você pode solicitar a exclusão de uma consulta especificada fazendo uma solicitação de PATCH para a variável `/queries` e fornecer o `id` no caminho da solicitação.

**Formato da API**

```http
PATCH /queries/{QUERY_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_ID}` | O `id` valor da consulta que deseja cancelar. |


**Solicitação**

Essa solicitação de API usa a sintaxe do Patch JSON para sua carga útil. Para obter mais informações sobre como o patch JSON funciona, leia o documento de fundamentos da API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `op` | Para cancelar a consulta, você deve definir o parâmetro op com o valor `cancel `. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com a seguinte mensagem:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
