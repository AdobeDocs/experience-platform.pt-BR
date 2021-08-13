---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, consultas agendadas, consulta agendada;
solution: Experience Platform
title: Ponto de Extremidade da API de Consultas Agendadas
topic-legacy: scheduled queries
description: As seções a seguir abordam as várias chamadas de API que podem ser feitas para consultas agendadas com a API do serviço de consulta.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 0b1afcb23e070209006383d27eb68edcf92d02cd
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 2%

---

# Ponto de extremidade de consultas agendadas

## Exemplos de chamadas de API

Agora que você sabe quais cabeçalhos usar, está pronto para começar a fazer chamadas para a API [!DNL Query Service]. As seções a seguir abordam as várias chamadas de API que podem ser feitas usando a API [!DNL Query Service]. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e uma resposta de amostra.

### Recuperar uma lista de consultas agendadas

Você pode recuperar uma lista de todas as consultas agendadas para sua Organização IMS fazendo uma solicitação GET para o endpoint `/schedules`.

**Formato da API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros de consulta**

Veja a seguir uma lista de parâmetros de consulta disponíveis para listar consultas programadas. Todos esses parâmetros são opcionais. Fazer uma chamada para esse terminal sem parâmetros recuperará todas as consultas agendadas disponíveis para sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar os resultados. Os campos compatíveis são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados por criados em ordem crescente. Adicionar um `-` antes de criado (`orderby=-created`) classificará os itens por criado em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20*) |
| `start` | Desloca a lista de resposta usando a numeração baseada em zero. Por exemplo, `start=2` retornará uma lista a partir da terceira query listada. (*Valor padrão: 0*) |
| `property` | Filtre os resultados com base nos campos. Os filtros **devem** ter escape de HTML. Vírgulas são usadas para combinar vários conjuntos de filtros. Os campos compatíveis são `created`, `templateId` e `userId`. A lista de operadores compatíveis é `>` (maior que), `<` (menor que) e `==` (igual a). Por exemplo, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` retornará todas as consultas agendadas nas quais a ID do usuário está conforme especificado. |

**Solicitação**

A solicitação a seguir recupera a consulta agendada mais recente criada para a organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de consultas programadas para a Organização IMS especificada. A resposta a seguir retorna a consulta agendada mais recente criada para sua organização IMS.

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### Criar uma nova consulta agendada

Você pode criar uma nova consulta agendada fazendo uma solicitação de POST ao endpoint `/schedules`. Ao criar uma consulta agendada na API, você também pode vê-la no Editor de consultas. Para obter mais informações sobre consultas agendadas na interface do usuário, leia a [documentação do Editor de consultas](../ui/user-guide.md#scheduled-queries).

**Formato da API**

```http
POST /schedules
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| Propriedade | Descrição |
| -------- | ----------- |
| `query.dbName` | O nome do banco de dados para o qual você está criando uma consulta agendada. |
| `query.sql` | A consulta SQL que você deseja criar. |
| `query.name` | O nome da consulta agendada. |
| `schedule.schedule` | O cronograma de execução do query. Para obter mais informações sobre programações cron, leia a documentação [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Neste exemplo, &quot;30 * * * *&quot; significa que o query será executado a cada hora na marca de 30 minutos.<br><br>Como alternativa, você pode usar as seguintes expressões abreviadas:<ul><li>`@once`: A consulta só é executada uma vez.</li><li>`@hourly`: O query é executado a cada hora no início da hora. É equivalente à expressão cron `0 * * * *`.</li><li>`@daily`: O query é executado uma vez por dia à meia-noite. É equivalente à expressão cron `0 0 * * *`.</li><li>`@weekly`: O query é executado uma vez por semana, no domingo, à meia-noite. É equivalente à expressão cron `0 0 * * 0`.</li><li>`@monthly`: O query é executado uma vez por mês, no primeiro dia do mês, à meia-noite. É equivalente à expressão cron `0 0 1 * *`.</li><li>`@yearly`: O query é executado uma vez por ano, em 1º de janeiro, à meia-noite. É equivalente à expressão cron `1 0 0 1 1 *`. |
| `schedule.startDate` | A data de início da consulta agendada, escrita como um carimbo de data e hora UTC. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com detalhes da sua query agendada recém-criada. Quando a ativação da consulta agendada for concluída, `state` será alterado de `REGISTERING` para `ENABLED`.

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir a consulta agendada criada](#delete-a-specified-scheduled-query).

### Solicitar detalhes de uma consulta agendada especificada

Você pode recuperar informações de uma consulta agendada específica fazendo uma solicitação de GET para o endpoint `/schedules` e fornecendo sua ID no caminho da solicitação.

**Formato da API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` da consulta agendada que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da consulta agendada especificada.

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.delete` para [excluir a consulta agendada criada](#delete-a-specified-scheduled-query).

### Atualizar detalhes de uma consulta agendada especificada

Você pode atualizar os detalhes de uma consulta agendada especificada fazendo uma solicitação de PATCH para o endpoint `/schedules` e fornecendo sua ID no caminho da solicitação.

A solicitação PATCH suporta dois caminhos diferentes: `/state` e `/schedule/schedule`.

### Atualizar estado de consulta agendada

Você pode usar `/state` para atualizar o estado da consulta agendada selecionada - ATIVADA ou DESATIVADA. Para atualizar o estado, será necessário definir o valor como `enable` ou `disable`.

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` da consulta agendada que você deseja recuperar. |


**Solicitação**

Essa solicitação de API usa a sintaxe do Patch JSON para sua carga útil. Para obter mais informações sobre como o patch JSON funciona, leia o documento de fundamentos da API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o estado da consulta agendada, é necessário definir o valor de `path` como `/state`. |
| `value` | O valor atualizado de `/state`. Esse valor pode ser definido como `enable` ou `disable` para habilitar ou desabilitar a consulta agendada. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com a seguinte mensagem.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Atualizar agendamento de consulta agendada

Você pode usar `/schedule/schedule` para atualizar o cronograma do cron da consulta agendada. Para obter mais informações sobre programações cron, leia a documentação [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` da consulta agendada que você deseja recuperar. |

**Solicitação**

Essa solicitação de API usa a sintaxe do Patch JSON para sua carga útil. Para obter mais informações sobre como o patch JSON funciona, leia o documento de fundamentos da API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o agendamento da consulta agendada, é necessário definir o valor de `path` para `/schedule/schedule`. |
| `value` | O valor atualizado de `/schedule`. Esse valor precisa estar no formato de um cronograma de execução. Portanto, neste exemplo, a consulta agendada será executada a cada hora, na marca de 45 minutos. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com a seguinte mensagem.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Excluir uma consulta agendada especificada

Você pode excluir uma consulta agendada especificada, fazendo uma solicitação DELETE ao endpoint `/schedules` e fornecendo a ID da consulta agendada que deseja excluir no caminho da solicitação.

>[!NOTE]
>
>O agendamento **deve** ser desativado antes de ser excluído.

**Formato da API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` da consulta agendada que você deseja recuperar. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com a seguinte mensagem.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
