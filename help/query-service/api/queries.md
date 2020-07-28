---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Query Service
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---


# Queries

## Chamadas de API de exemplo

As seções a seguir percorrem as chamadas que você pode fazer usando o `/queries` terminal na [!DNL Query Service] API. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Recuperar uma lista de query

Você pode recuperar uma lista de todos os query para a Organização IMS, fazendo uma solicitação de GET para o `/queries` endpoint.

**Formato da API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por E comercial (`&`). Os parâmetros disponíveis estão listados abaixo.

**Parâmetros do Query**

A seguir está uma lista de parâmetros de query disponíveis para listar query. Todos esses parâmetros são opcionais. Efetuar uma chamada para este terminal sem parâmetros recuperará todos os query disponíveis para a sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar os resultados. Os campos suportados são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados em ordem crescente. A adição de um item `-` antes de criado (`orderby=-created`) classificará os itens em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados que são incluídos em uma página. (*Default value: 20*) |
| `start` | Desloca a lista de resposta, usando a numeração com base em zero. Por exemplo, `start=2` retornará uma lista a partir do query listado. (*Default value: 0*) |
| `property` | Filtrar resultados com base em campos. Os filtros **devem** ter escape de HTML. As vírgulas são usadas para combinar vários conjuntos de filtros. Os campos suportados são `created`, `updated`, `state`e `id`. A lista dos operadores suportados é `>` (maior que), `<` (menor que), `>=` (maior que ou igual a), `<=` (menor que ou igual a), `==` (igual a), `!=` (diferente de) e `~` (contém). Por exemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retornará todos os query com a ID especificada. |
| `excludeSoftDeleted` | Indica se um query que tenha sido excluído de forma suave deve ser incluído. Por exemplo, `excludeSoftDeleted=false` incluirá **** query suaves excluídos. (*Booliano, valor padrão: true*) |
| `excludeHidden` | Indica se query não controlados pelo usuário devem ser exibidos. Ter esse valor definido como falso **incluirá** query não controlados pelo usuário, como definições CURSOR, FETCH ou query de metadados. (*Booliano, valor padrão: true*) |

**Solicitação**

A solicitação a seguir recupera o query mais recente criado para sua organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de query para a Organização IMS especificada como JSON. A resposta a seguir retorna o query mais recente criado para sua organização IMS.

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

### Criar um query

Você pode criar um novo query, fazendo uma solicitação de POST para o `/queries` terminal.

**Formato da API**

```http
POST /queries
```

**Solicitação**

A solicitação a seguir cria um novo query, configurado pelos valores fornecidos na carga:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query"
        "description": "Sample Description"
    }  
```

| Propriedade | Descrição |
| -------- | ----------- |
| `dbName` | O nome do banco de dados para o qual você está criando um query SQL. |
| `sql` | O query SQL que você deseja criar. |
| `name` | O nome do seu query SQL. |
| `description` | A descrição do seu query SQL. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com detalhes do query recém-criado. Quando o query terminar de ser ativado e for executado com êxito, ele `state` será alterado de `SUBMITTED` para `SUCCESS`.

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
>Você pode usar o valor de `_links.cancel` para [cancelar o query](#cancel-a-query)criado.

### Recuperar um query por ID

Você pode recuperar informações detalhadas sobre um query específico, fazendo uma solicitação de GET para o ponto final e fornecendo o `/queries` `id` valor do query no caminho da solicitação.

**Formato da API**

```http
GET /queries/{QUERY_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_ID}` | O `id` valor do query que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o query especificado.

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
>Você pode usar o valor de `_links.cancel` para [cancelar o query](#cancel-a-query)criado.

### Cancelar um query

Você pode solicitar a exclusão de um query especificado, fazendo uma solicitação de PATCH para o `/queries` endpoint e fornecendo o valor do query `id` no caminho da solicitação.

**Formato da API**

```http
PATCH /queries/{QUERY_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_ID}` | O `id` valor do query que você deseja cancelar. |


**Solicitação**

Essa solicitação de API usa a sintaxe do Patch JSON para sua carga. Para obter mais informações sobre como a correção JSON funciona, leia o documento de fundamentos da API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `op` | Para cancelar o query, é necessário definir o parâmetro op com o valor `cancel `. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
