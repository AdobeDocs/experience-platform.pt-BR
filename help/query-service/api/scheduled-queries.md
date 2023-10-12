---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consultas agendadas;consulta agendada;
solution: Experience Platform
title: Endpoint de agendamentos
description: As seções a seguir abordam as várias chamadas de API que podem ser feitas para consultas programadas com a API de serviço de consulta.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 958d5c322ff26f7372f8ab694a70ac491cbff56c
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 3%

---

# Endpoint de agendamentos

## Exemplos de chamadas de API

Agora que você entende quais cabeçalhos usar, você está pronto para começar a fazer chamadas para o [!DNL Query Service] API. As seções a seguir abordam as várias chamadas de API que podem ser feitas usando o [!DNL Query Service] API. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Recuperar uma lista de consultas agendadas

Você pode recuperar uma lista de todas as consultas agendadas para sua organização fazendo uma solicitação GET para o `/schedules` terminal.

**Formato da API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros de consulta**

Veja a seguir uma lista de parâmetros de consulta disponíveis para listar consultas programadas. Todos esses parâmetros são opcionais. Fazer uma chamada para esse endpoint sem parâmetros recuperará todas as consultas agendadas disponíveis para sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar resultados. Os campos compatíveis são `created` e `updated`. Por exemplo, `orderby=created` Os resultados serão classificados por criados em ordem crescente. Adicionar um `-` antes de criar (`orderby=-created`) classificará os itens por criados em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20*) |
| `start` | Especifique um carimbo de data e hora no formato ISO para ordenar os resultados. Se nenhuma data de início for especificada, a chamada à API retornará primeiro a consulta agendada mais antiga criada e, em seguida, continuará a listar os resultados mais recentes.<br> Os carimbos de data e hora ISO permitem diferentes níveis de granularidade na data e hora. Os carimbos de data e hora ISO básicos têm o formato de: `2020-09-07` para expressar a data em 7 de setembro de 2020. Um exemplo mais complexo seria escrito como `2022-11-05T08:15:30-05:00` e corresponde a 5 de novembro de 2022, 8:15:30 da manhã, Hora Padrão do Leste dos EUA. Um fuso horário pode ser fornecido com um deslocamento UTC e é indicado pelo sufixo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se nenhum fuso horário for fornecido, o padrão será zero. |
| `property` | Filtrar resultados com base em campos. Os filtros **deve** ser escapado por HTML. As vírgulas são usadas para combinar vários conjuntos de filtros. Os campos compatíveis são `created`, `templateId`, e `userId`. A lista de operadores compatíveis é `>` (maior que), `<` (menor que) e `==` (igual a). Por exemplo, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` retornará todas as consultas agendadas em que a ID do usuário esteja conforme especificado. |

**Solicitação**

A solicitação a seguir recupera a consulta agendada mais recente criada para sua organização.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de consultas agendadas para a organização especificada. A resposta a seguir retorna a consulta agendada mais recente criada para sua organização.

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

Você pode criar uma nova consulta agendada fazendo uma solicitação POST para a `/schedules` terminal. Ao criar uma consulta agendada na API, você também pode vê-la no Editor de consultas. Para obter mais informações sobre consultas programadas na interface do usuário, leia o [Documentação do Editor de consultas](../ui/user-guide.md#scheduled-queries).

**Formato da API**

```http
POST /schedules
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schedule.schedule` | O cronograma cron para a consulta. Para obter mais informações sobre cronogramas cron, leia a [formato de expressão do cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentação. Neste exemplo, &quot;30 * * * *&quot; significa que a consulta será executada a cada hora na marca de 30 minutos.<br><br>Como alternativa, você pode usar as seguintes expressões abreviadas:<ul><li>`@once`: a consulta é executada apenas uma vez.</li><li>`@hourly`: A consulta é executada a cada hora no início da hora. É equivalente à expressão cron `0 * * * *`.</li><li>`@daily`: O query é executado uma vez por dia à meia-noite. É equivalente à expressão cron `0 0 * * *`.</li><li>`@weekly`: O query é executado uma vez por semana, no domingo, à meia-noite. É equivalente à expressão cron `0 0 * * 0`.</li><li>`@monthly`: O query é executado uma vez por mês, no primeiro dia do mês, à meia-noite. É equivalente à expressão cron `0 0 1 * *`.</li><li>`@yearly`: O query é executado uma vez por ano, no dia 1º de janeiro, à meia-noite. É equivalente à expressão cron `1 0 0 1 1 *`. |
| `schedule.startDate` | A data de início da consulta agendada, gravada como carimbo de data e hora UTC. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com detalhes da consulta agendada recém-criada. Quando a ativação da consulta programada for concluída, a variável `state` mudará de `REGISTERING` para `ENABLED`.

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

Você pode recuperar informações de uma consulta agendada específica fazendo uma solicitação GET ao `/schedules` e fornecendo sua ID no caminho da solicitação.

**Formato da API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | A variável `id` valor da consulta programada que deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Você pode atualizar os detalhes de uma consulta agendada especificada fazendo uma solicitação PATCH para o `/schedules` e fornecendo a respectiva ID no caminho da solicitação.

A solicitação PATCH suporta dois caminhos diferentes: `/state` e `/schedule/schedule`.

### Atualizar estado de consulta agendada

Você pode atualizar o estado da consulta agendada selecionada definindo o `path` propriedade para `/state` e a variável `value` propriedade como um dos dois `enable` ou `disable`.

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | A variável `id` valor da consulta programada que você deseja PATCH. |


**Solicitação**

Essa solicitação de API usa a sintaxe do patch de JSON para sua carga. Para obter mais informações sobre como o Patch JSON funciona, leia o documento Fundamentos da API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | A operação a ser executada no agendamento de consulta. O valor aceito é `replace`. |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o estado da consulta agendada, é necessário definir o valor de `path` para `/state`. |
| `value` | O valor atualizado de `/state`. Esse valor pode ser definido como `enable` ou `disable` para ativar ou desativar a consulta programada. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Atualizar programação de consulta programada

Você pode atualizar a programação cron da consulta agendada definindo o parâmetro `path` propriedade para `/schedule/schedule` no corpo da solicitação. Para obter mais informações sobre cronogramas cron, leia a [formato de expressão do cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentação.

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | A variável `id` valor da consulta programada que você deseja PATCH. |

**Solicitação**

Essa solicitação de API usa a sintaxe do patch de JSON para sua carga. Para obter mais informações sobre como o Patch JSON funciona, leia o documento Fundamentos da API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | A operação a ser executada no agendamento de consulta. O valor aceito é `replace`. |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o agendamento da consulta agendada, é necessário definir o valor de `path` para `/schedule/schedule`. |
| `value` | O valor atualizado de `/schedule`. Esse valor precisa estar no formato de um cronograma cron. Portanto, neste exemplo, a consulta agendada será executada a cada hora na marca de 45 minutos. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Excluir uma consulta agendada especificada

Você pode excluir uma consulta agendada especificada fazendo uma solicitação DELETE à `/schedules` e fornecendo a ID da consulta agendada que deseja excluir no caminho da solicitação.

>[!NOTE]
>
>A programação **deve** ser desabilitado antes de ser excluído.

**Formato da API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | A variável `id` valor da consulta programada que você deseja DELETE. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
