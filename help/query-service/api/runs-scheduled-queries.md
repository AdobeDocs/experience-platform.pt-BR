---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, executar consultas agendadas, executar consultas agendadas, serviço de consultas, consultas agendadas, consulta agendada;
solution: Experience Platform
title: Consulta agendada executa Ponto de Extremidade da API
topic-legacy: runs for scheduled queries
description: As seções a seguir abordam as várias chamadas de API que podem ser feitas para a execução de consultas agendadas com a API do serviço de consulta.
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# A consulta agendada executa o ponto de extremidade

## Exemplos de chamadas de API

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para o [!DNL Query Service] API. As seções a seguir abordam as várias chamadas de API que você pode fazer usando o [!DNL Query Service] API. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e uma resposta de amostra.

### Recuperar uma lista de todas as execuções de uma consulta agendada especificada

Você pode recuperar uma lista de todas as execuções de uma consulta agendada específica, independentemente de elas estarem em execução ou já terem sido concluídas. Isso é feito fazendo uma solicitação GET para o `/schedules/{SCHEDULE_ID}/runs` endpoint, em que `{SCHEDULE_ID}` é `id` valor da query agendada cujas execuções você deseja recuperar.

**Formato da API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor da consulta agendada que deseja recuperar. |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros de consulta**

Veja a seguir uma lista de parâmetros de consulta disponíveis para listar execuções de uma query programada especificada. Todos esses parâmetros são opcionais. Efetuar uma chamada para este ponto de extremidade sem parâmetros recuperará todas as execuções disponíveis para a consulta agendada especificada.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar os resultados. Os campos compatíveis são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados por criados em ordem crescente. Adicionar um `-` antes de criar (`orderby=-created`) classificará os itens por criados em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20º*) |
| `start` | Desloca a lista de resposta usando a numeração baseada em zero. Por exemplo, `start=2` retornará uma lista a partir da terceira query listada. (*Valor padrão: 0*) |
| `property` | Filtre os resultados com base nos campos. Os filtros **must** ser HTML escapado. Vírgulas são usadas para combinar vários conjuntos de filtros. Os campos compatíveis são `created`, `state`e `externalTrigger`. A lista de operadores compatíveis é `>` (maior que), `<` (menor que), e  `==` (igual a), e `!=` (não igual a). Por exemplo, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` retornará todas as execuções criadas, bem-sucedidas e criadas manualmente após 20 de abril de 2019. |

**Solicitação**

A solicitação a seguir recupera as quatro últimas execuções da consulta agendada especificada.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de execuções para a consulta agendada especificada como JSON. A resposta a seguir retorna as quatro últimas execuções da query agendada especificada.

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>Você pode usar o valor de `_links.cancel` para [interromper uma execução para uma consulta agendada especificada](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Acionar imediatamente uma execução para uma consulta agendada específica

Você pode acionar imediatamente uma execução para uma consulta agendada específica fazendo uma solicitação de POST para a `/schedules/{SCHEDULE_ID}/runs` endpoint, em que `{SCHEDULE_ID}` é `id` valor da query agendada cuja execução você deseja acionar.

**Formato da API**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com a seguinte mensagem.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Recuperar detalhes de uma execução para uma consulta agendada específica

Você pode recuperar detalhes sobre uma execução de uma consulta agendada específica fazendo uma solicitação de GET para a `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` e fornecendo a ID da consulta agendada e a execução no caminho da solicitação.

**Formato da API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor da query agendada cuja execução você deseja recuperar detalhes. |
| `{RUN_ID}` | O `id` valor da execução que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da execução especificada.

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### Interromper imediatamente uma execução para uma consulta agendada específica

Você pode interromper imediatamente uma execução de uma consulta agendada específica fazendo uma solicitação de PATCH para a `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` e fornecendo a ID da consulta agendada e a execução no caminho da solicitação.

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor da query agendada cuja execução você deseja recuperar detalhes. |
| `{RUN_ID}` | O `id` valor da execução que você deseja recuperar. |

**Solicitação**

Essa solicitação de API usa a sintaxe do Patch JSON para sua carga útil. Para obter mais informações sobre como o patch JSON funciona, leia o documento de fundamentos da API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted) com a seguinte mensagem.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
