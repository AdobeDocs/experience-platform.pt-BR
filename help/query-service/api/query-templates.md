---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Query Service
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 3%

---


# Modelos de Query

## Chamadas de API de exemplo

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para a API de serviço do Query. As seções a seguir percorrem várias chamadas de API que podem ser feitas usando a API de serviço de Query. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Recuperar uma lista de modelos de query

Você pode recuperar uma lista de todos os modelos de query para a organização IMS, fazendo uma solicitação GET ao `/query-templates` endpoint.

**Formato da API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por E comercial (`&`). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros do Query**

A seguir está uma lista de parâmetros de query disponíveis para a listagem de modelos de query. Todos esses parâmetros são opcionais. Efetuar uma chamada para este terminal sem parâmetros recuperará todos os modelos de query disponíveis para a sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar os resultados. Os campos suportados são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados em ordem crescente. A adição de um item `-` antes de criado (`orderby=-created`) classificará os itens em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados que são incluídos em uma página. (*Default value: 20*) |
| `start` | Desloca a lista de resposta, usando a numeração com base em zero. Por exemplo, `start=2` retornará uma lista a partir do query listado. (*Default value: 0*) |
| `property` | Filtrar resultados com base em campos. Os filtros **devem** ter escape de HTML. As vírgulas são usadas para combinar vários conjuntos de filtros. Os campos suportados são `name` e `userId`. O único operador suportado é `==` (igual a). Por exemplo, `name==my_template` retornará todos os modelos de query com o nome `my_template`. |

**Solicitação**

A solicitação a seguir recupera o modelo de query mais recente criado para sua organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de modelos de query para a Organização IMS especificada. A resposta a seguir retorna o modelo de query mais recente criado para sua organização IMS.

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir seu modelo](#delete-a-specified-query-template)de query.

### Criar um modelo de query

Você pode criar um modelo de query fazendo uma solicitação POST ao ponto de extremidade `/query-templates` .

**Formato da API**

```http
POST /query-templates
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `sql` | O query SQL que você deseja criar. |
| `name` | O nome do modelo de query. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com detalhes do modelo de query recém-criado.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir seu modelo](#delete-a-specified-query-template)de query.

### Recuperar um modelo de query especificado

Você pode recuperar um modelo de query específico, fazendo uma solicitação GET para o `/query-templates/{TEMPLATE_ID}` terminal e fornecendo a ID do modelo de query no caminho da solicitação.

**Formato da API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | O `id` valor do modelo de query que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do modelo de query especificado.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir seu modelo](#delete-a-specified-query-template)de query.

### Atualizar um modelo de query especificado

Você pode atualizar um modelo de query específico, fazendo uma solicitação PUT para o `/query-templates/{TEMPLATE_ID}` ponto de extremidade e fornecendo a ID do modelo de query no caminho da solicitação.

**Formato da API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{TEMPLATE_ID}` | O `id` valor do modelo de query que você deseja recuperar. |

**Solicitação**

>[!NOTE]
>
>A solicitação PUT exige que o sql e o campo de nome sejam preenchidos e **substituirá** o conteúdo atual desse modelo de query.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `sql` | O query SQL que você deseja atualizar. |
| `name` | O nome do query agendado. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com as informações atualizadas do modelo de query especificado.

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir seu modelo](#delete-a-specified-query-template)de query.

### Excluir um modelo de query especificado

É possível excluir um modelo de query específico, solicitando DELETE ao e fornecendo a ID do modelo de query no caminho da solicitação. `/query-templates/{TEMPLATE_ID}`

**Formato da API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{TEMPLATE_ID}` | O `id` valor do modelo de query que você deseja recuperar. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
