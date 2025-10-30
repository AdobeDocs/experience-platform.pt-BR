---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;guia da api;consultas;consulta;serviço de consulta;
solution: Experience Platform
title: Endpoint da API de consultas
description: As seções a seguir abordam as chamadas que você pode fazer usando o endpoint /queries na API de serviço de consulta.
role: Developer
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 3%

---

# Endpoint de consultas

## Exemplos de chamadas de API

As seções a seguir abordam chamadas que você pode fazer usando o ponto de extremidade `/queries` na API [!DNL Query Service]. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Recuperar uma lista de consultas

Você pode recuperar uma lista de todas as consultas para sua organização fazendo uma solicitação GET para o ponto de extremidade `/queries`.

**Formato da API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`). Os parâmetros disponíveis estão listados abaixo.

**Parâmetros de consulta**

Veja a seguir uma lista de parâmetros de consulta disponíveis para consultas de listagem. Todos esses parâmetros são opcionais. Fazer uma chamada para esse endpoint sem parâmetros recuperará todas as consultas disponíveis para sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar resultados. Os campos com suporte são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados por ordem crescente criada. Adicionar um `-` antes de criar (`orderby=-created`) classificará os itens por ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20*) |
| `start` | Especifique um carimbo de data e hora no formato ISO para ordenar os resultados. Se nenhuma data de início for especificada, a chamada à API retornará primeiro a consulta criada mais antiga e, em seguida, continuará a listar os resultados mais recentes.Os carimbos de data e hora ISO <br> permitem diferentes níveis de granularidade na data e hora. Os carimbos de data e hora ISO básicos assumem o formato de: `2020-09-07` para expressar a data em 7 de setembro de 2020. Um exemplo mais complexo seria escrito como `2022-11-05T08:15:30-05:00` e corresponde a 5 de novembro de 2022, às 8:15:30 am, Hora Padrão do Leste dos EUA. Um fuso horário pode ser fornecido com um deslocamento UTC e é indicado pelo sufixo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se nenhum fuso horário for fornecido, o padrão será zero. |
| `property` | Filtrar resultados com base em campos. Os filtros **devem** ter HTML com escape. As vírgulas são usadas para combinar vários conjuntos de filtros. Os campos com suporte são `created`, `updated`, `state` e `id`. A lista de operadores com suporte é `>` (maior que), `<` (menor que), `>=` (maior ou igual a), `<=` (menor ou igual a), `==` (igual a), `!=` (diferente de) e `~` (contém). Por exemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retornará todas as consultas com a ID especificada. |
| `excludeSoftDeleted` | Indica se uma consulta que foi excluída por software deve ser incluída. Por exemplo, `excludeSoftDeleted=false` irá **incluir** consultas excluídas por software. (*Booleano, valor padrão: true*) |
| `excludeHidden` | Indica se as consultas não orientadas por usuário devem ser exibidas. Se este valor for definido como falso **incluirá** consultas não orientadas por usuário, como definições de CURSOR, BUSCAR ou consultas de metadados. (*Booleano, valor padrão: true*) |
| `isPrevLink` | O parâmetro de consulta `isPrevLink` é usado para paginação. Os resultados da chamada de API são classificados usando o carimbo de data/hora `created` e a propriedade `orderby`. Ao navegar pelas páginas de resultados, `isPrevLink` é definido como verdadeiro quando a página é retroativa. Inverte a ordem da consulta. Consulte os links &quot;próximo&quot; e &quot;anterior&quot; como exemplos. |

**Solicitação**

A solicitação a seguir recupera a consulta mais recente criada para sua organização.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de consultas para a organização especificada como JSON. A resposta a seguir retorna a consulta mais recente criada para sua organização.

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

Você pode criar uma nova consulta fazendo uma solicitação POST para o ponto de extremidade `/queries`.

**Formato da API**

```http
POST /queries
```

**Solicitação**

A solicitação a seguir cria uma nova consulta, com uma instrução SQL fornecida na carga:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

O exemplo de solicitação abaixo cria uma nova consulta usando uma ID de modelo de consulta existente.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
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
| `queryParameters` | Um par de valores chave para substituir quaisquer valores parametrizados na instrução SQL. Somente é necessário **se** você estiver usando substituições de parâmetros no SQL fornecido. Nenhuma verificação de tipo de valor será feita nesses pares de valores principais. |
| `templateId` | O identificador exclusivo de uma consulta pré-existente. Você pode fornecer isso em vez de uma instrução SQL. |
| `insertIntoParameters` | (Opcional) Se essa propriedade for definida, essa consulta será convertida em uma consulta INSERT INTO. |
| `ctasParameters` | (Opcional) Se esta propriedade for definida, esta consulta será convertida em uma consulta CTAS. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com detalhes da consulta recém-criada. Quando a ativação da consulta for concluída e executada com êxito, `state` será alterado de `SUBMITTED` para `SUCCESS`.

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

Você pode recuperar informações detalhadas sobre uma consulta específica fazendo uma solicitação GET para o ponto de extremidade `/queries` e fornecendo o valor `id` da consulta no caminho da solicitação.

**Formato da API**

```http
GET /queries/{QUERY_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_ID}` | O valor `id` da consulta que você deseja recuperar. |

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

### Cancelar ou excluir uma consulta por software

Você pode solicitar o cancelamento ou a exclusão reversível de uma consulta especificada fazendo uma solicitação PATCH para o ponto de extremidade `/queries` e fornecendo o valor `id` da consulta no caminho da solicitação.

**Formato da API**

```http
PATCH /queries/{QUERY_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{QUERY_ID}` | O valor `id` da consulta na qual você deseja executar a operação. |


**Solicitação**

Essa solicitação de API usa a sintaxe do patch de JSON para sua carga. Para obter mais informações sobre como o Patch JSON funciona, leia o documento Fundamentos da API.

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
| `op` | O tipo de operação a ser executada no recurso. Os valores permitidos são `cancel` e `soft_delete`. Para cancelar a consulta, você deve definir o parâmetro op com o valor `cancel`. Observe que a operação de exclusão reversível impede que a consulta seja retornada em solicitações GET, mas não a exclui do sistema. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
