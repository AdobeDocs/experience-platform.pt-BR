---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;modelos de consulta;guia de api;modelos;Serviço de consulta;
solution: Experience Platform
title: Endpoint da API de Modelos de Consulta
description: Este guia detalha as várias chamadas de API do modelo de consulta que você pode fazer usando a API do Serviço de consulta.
role: Developer
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 3%

---

# Endpoint de modelos de consulta

## Exemplos de chamadas de API

As seções a seguir descrevem as várias chamadas de API que você pode fazer usando a API [!DNL Query Service]. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

Consulte a [documentação de modelos de consulta da interface](../ui/query-templates.md) para obter informações sobre como criar modelos por meio da interface do Experience Platform.

### Recuperar uma lista de modelos de consulta

Você pode recuperar uma lista de todos os modelos de consulta para sua organização fazendo uma solicitação GET para o ponto de extremidade `/query-templates`.

**Formato da API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros de consulta**

Veja a seguir uma lista de parâmetros de consulta disponíveis para listar modelos de consulta. Todos esses parâmetros são opcionais. Fazer uma chamada para esse endpoint sem parâmetros recuperará todos os modelos de consulta disponíveis para sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar resultados. Os campos com suporte são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados por ordem crescente criada. Adicionar um `-` antes de criar (`orderby=-created`) classificará os itens por ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20*) |
| `start` | Especifique um carimbo de data e hora no formato ISO para ordenar os resultados. Se nenhuma data de início for especificada, a chamada à API retornará primeiro os modelos criados mais antigos e, em seguida, continuará a listar os resultados mais recentes.Os carimbos de data e hora ISO <br> permitem diferentes níveis de granularidade na data e hora. Os carimbos de data e hora ISO básicos assumem o formato de: `2020-09-07` para expressar a data em 7 de setembro de 2020. Um exemplo mais complexo seria escrito como `2022-11-05T08:15:30-05:00` e corresponde a 5 de novembro de 2022, às 8:15:30 am, Hora Padrão do Leste dos EUA. Um fuso horário pode ser fornecido com um deslocamento UTC e é indicado pelo sufixo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se nenhum fuso horário for fornecido, o padrão será zero. |
| `property` | Filtrar resultados com base em campos. Os filtros **devem** ter HTML de escape. As vírgulas são usadas para combinar vários conjuntos de filtros. Os campos com suporte são `name` e `userId`. O único operador com suporte é `==` (igual a). Por exemplo, `name==my_template` retornará todos os modelos de consulta com o nome `my_template`. |

**Solicitação**

A solicitação a seguir recupera o modelo de consulta mais recente criado para sua organização.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de modelos de consulta para a organização especificada. A resposta a seguir retorna o modelo de consulta mais recente criado para sua organização.

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

Você pode criar um modelo de consulta fazendo uma solicitação POST para o ponto de extremidade `/query-templates`.

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
| `sql` | A consulta SQL que você deseja criar. Você pode usar SQL padrão ou uma substituição de parâmetro. Para usar uma substituição de parâmetro no SQL, você deve anexar uma `$` à chave de parâmetro. Por exemplo, `$key` e forneça os parâmetros usados no SQL como pares de valores da chave JSON no campo `queryParameters`. Os valores transmitidos aqui serão os parâmetros padrão usados no modelo. Se quiser substituir esses parâmetros, você deverá substituí-los na solicitação POST. |
| `name` | O nome do modelo de consulta. |
| `queryParameters` | Um par de valores chave para substituir quaisquer valores parametrizados na instrução SQL. Somente é necessário **se** você estiver usando substituições de parâmetros no SQL fornecido. Nenhuma verificação de tipo de valor será feita nesses pares de valores principais. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com detalhes do modelo de consulta recém-criado.

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

Você pode recuperar um modelo de consulta específico fazendo uma solicitação GET para o ponto de extremidade `/query-templates/{TEMPLATE_ID}` e fornecendo a ID do modelo de consulta no caminho da solicitação.

**Formato da API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | O valor `id` do modelo de consulta que você deseja recuperar. |

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

Você pode atualizar um modelo de consulta específico fazendo uma solicitação PUT para o ponto de extremidade `/query-templates/{TEMPLATE_ID}` e fornecendo a ID do modelo de consulta no caminho da solicitação.

**Formato da API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{TEMPLATE_ID}` | O valor `id` do modelo de consulta que você deseja recuperar. |

**Solicitação**

>[!NOTE]
>
>A solicitação PUT exige que os campos sql e name sejam preenchidos e **substituirá** o conteúdo atual desse modelo de consulta.

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
| `sql` | A consulta SQL que você deseja criar. Você pode usar SQL padrão ou uma substituição de parâmetro. Para usar uma substituição de parâmetro no SQL, você deve anexar uma `$` à chave de parâmetro. Por exemplo, `$key` e forneça os parâmetros usados no SQL como pares de valores da chave JSON no campo `queryParameters`. Os valores transmitidos aqui serão os parâmetros padrão usados no modelo. Se quiser substituir esses parâmetros, você deverá substituí-los na solicitação POST. |
| `name` | O nome do modelo de consulta. |
| `queryParameters` | Um par de valores chave para substituir quaisquer valores parametrizados na instrução SQL. Somente é necessário **se** você estiver usando substituições de parâmetros no SQL fornecido. Nenhuma verificação de tipo de valor será feita nesses pares de valores principais. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com as informações atualizadas para o modelo de consulta especificado.

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

Você pode excluir um modelo de consulta específico fazendo uma solicitação DELETE para `/query-templates/{TEMPLATE_ID}` e fornecendo a ID do modelo de consulta no caminho da solicitação.

**Formato da API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{TEMPLATE_ID}` | O valor `id` do modelo de consulta que você deseja recuperar. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
