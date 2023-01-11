---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, modelos de consulta, guia de api, modelos, serviço de query;
solution: Experience Platform
title: Ponto de extremidade da API de modelos de consulta
description: Este guia detalha as várias chamadas de API de modelo de consulta que podem ser feitas usando a API do serviço de consulta.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: ee6a54aeba4ddfeb98ee5e11283c299f00969a53
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 4%

---

# Ponto de extremidade de modelos de consulta

## Exemplos de chamadas de API

As seções a seguir descrevem as várias chamadas de API que podem ser feitas usando o [!DNL Query Service] API. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e uma resposta de amostra.

Consulte a [Documentação dos modelos de consulta da interface do usuário](../ui/query-templates.md) para obter informações sobre como criar modelos por meio da interface do usuário do Experience Platform.

### Recuperar uma lista de templates de query

Você pode recuperar uma lista de todos os modelos de consulta para sua Organização IMS fazendo uma solicitação de GET para a `/query-templates` endpoint .

**Formato da API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros de consulta**

Esta é uma lista de parâmetros de consulta disponíveis para listar templates de query. Todos esses parâmetros são opcionais. Fazer uma chamada para esse terminal sem parâmetros recuperará todos os modelos de consulta disponíveis para sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar os resultados. Os campos compatíveis são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados por criados em ordem crescente. Adicionar um `-` antes de criar (`orderby=-created`) classificará os itens por criados em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20º*) |
| `start` | Desloca a lista de resposta usando a numeração baseada em zero. Por exemplo, `start=2` retornará uma lista a partir da terceira query listada. (*Valor padrão: 0*) |
| `property` | Filtre os resultados com base nos campos. Os filtros **must** ser HTML escapado. Vírgulas são usadas para combinar vários conjuntos de filtros. Os campos compatíveis são `name` e `userId`. O único operador suportado é `==` (igual a). Por exemplo, `name==my_template` retornará todos os modelos de consulta com o nome `my_template`. |

**Solicitação**

A solicitação a seguir recupera o modelo de consulta mais recente criado para sua organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de modelos de consulta para a Organização IMS especificada. A resposta a seguir retorna o modelo de consulta mais recente criado para sua organização IMS.

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
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
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
>Você pode usar o valor de `_links.delete` para [excluir seu modelo de consulta](#delete-a-specified-query-template).

### Criar um modelo de consulta

Você pode criar um template de query fazendo uma solicitação POST para a variável `/query-templates` endpoint .

**Formato da API**

```http
POST /query-templates
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `sql` | A consulta SQL que você deseja criar. Você pode usar o SQL padrão ou uma substituição de parâmetro. Para usar uma substituição de parâmetro no SQL, você deve anexar a chave de parâmetro com um `$`. Por exemplo, `$key`e fornecer os parâmetros usados no SQL como pares de valores-chave JSON no `queryParameters` campo. Os valores passados aqui serão os parâmetros padrão usados no modelo. Se quiser substituir esses parâmetros, você deve substituí-los na solicitação do POST. |
| `name` | O nome do template de query. |
| `queryParameters` | Um emparelhamento de valor principal para substituir quaisquer valores parametrizados na instrução SQL. Só é necessário **if** você está usando substituições de parâmetros dentro do SQL fornecido. Nenhuma verificação de tipo de valor será feita nesses pares de valores chave. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com detalhes do modelo de consulta recém-criado.

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir seu modelo de consulta](#delete-a-specified-query-template).

### Recuperar um modelo de consulta especificado

Você pode recuperar um template de query específico fazendo uma solicitação do GET para o `/query-templates/{TEMPLATE_ID}` e fornecer a ID do modelo de consulta no caminho da solicitação.

**Formato da API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | O `id` valor do template de query que deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do modelo de consulta especificado.

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir seu modelo de consulta](#delete-a-specified-query-template).

### Atualizar um modelo de consulta especificado

Você pode atualizar um template de query específico fazendo uma solicitação de PUT para a variável `/query-templates/{TEMPLATE_ID}` e fornecer a ID do modelo de consulta no caminho da solicitação.

**Formato da API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{TEMPLATE_ID}` | O `id` valor do template de query que deseja recuperar. |

**Solicitação**

>[!NOTE]
>
>A solicitação de PUT requer que o sql e o campo de nome sejam preenchidos e o **substituir** o conteúdo atual desse template de query.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `sql` | A consulta SQL que você deseja criar. Você pode usar o SQL padrão ou uma substituição de parâmetro. Para usar uma substituição de parâmetro no SQL, você deve anexar a chave de parâmetro com um `$`. Por exemplo, `$key`e fornecer os parâmetros usados no SQL como pares de valores-chave JSON no `queryParameters` campo. Os valores passados aqui serão os parâmetros padrão usados no modelo. Se quiser substituir esses parâmetros, você deve substituí-los na solicitação do POST. |
| `name` | O nome do template de query. |
| `queryParameters` | Um emparelhamento de valor principal para substituir quaisquer valores parametrizados na instrução SQL. Só é necessário **if** você está usando substituições de parâmetros dentro do SQL fornecido. Nenhuma verificação de tipo de valor será feita nesses pares de valores chave. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com as informações atualizadas para seu template de query especificado.

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir seu modelo de consulta](#delete-a-specified-query-template).

### Excluir um modelo de consulta especificado

Você pode excluir um modelo de consulta específico fazendo uma solicitação DELETE para a variável `/query-templates/{TEMPLATE_ID}` e fornecer a ID do modelo de consulta no caminho da solicitação.

**Formato da API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{TEMPLATE_ID}` | O `id` valor do template de query que deseja recuperar. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com a seguinte mensagem.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
