---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Query Service
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 2%

---


# É executado para query agendados

## Chamadas de API de exemplo

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para a API de serviço do Query. As seções a seguir percorrem várias chamadas de API que podem ser feitas usando a API de serviço de Query. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Recuperar uma lista de todas as execuções de um query agendado especificado

Você pode recuperar uma lista de todas as execuções para um query programado específico, independentemente de elas estarem em execução ou já concluídas. Isso é feito fazendo uma solicitação GET para o `/schedules/{SCHEDULE_ID}/runs` terminal, onde `{SCHEDULE_ID}` é o `id` valor do query agendado cujas execuções você deseja recuperar.

**Formato da API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do query programado que você deseja recuperar. |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por E comercial (`&`). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros do Query**

A seguir está uma lista de parâmetros de query disponíveis para listar execuções de um query programado especificado. Todos esses parâmetros são opcionais. Efetuar uma chamada para este terminal sem parâmetros recuperará todas as execuções disponíveis para o query agendado especificado.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar os resultados. Os campos suportados são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados em ordem crescente. A adição de um item `-` antes de criado (`orderby=-created`) classificará os itens em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados que são incluídos em uma página. (*Default value: 20*) |
| `start` | Desloca a lista de resposta, usando a numeração com base em zero. Por exemplo, `start=2` retornará uma lista a partir do query listado. (*Default value: 0*) |
| `property` | Filtrar resultados com base em campos. Os filtros **devem** ter escape de HTML. As vírgulas são usadas para combinar vários conjuntos de filtros. Os campos suportados são `created`, `state`e `externalTrigger`. A lista dos operadores suportados é `>` (maior que), `<` (menor que) e `==` (igual a) e `!=` (diferente de). Por exemplo, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` retornará todas as execuções criadas manualmente, bem-sucedidas e criadas após 20 de abril de 2019. |

**Solicitação**

A solicitação a seguir recupera as quatro últimas execuções do query agendado especificado.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de execuções para o query agendado especificado como JSON. A resposta a seguir retorna as quatro últimas execuções do query agendado especificado.

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
>Você pode usar o valor de `_links.cancel` para [interromper uma execução de um query](#immediately-stop-a-run-for-a-specific-scheduled-query)agendado especificado.

### Acionar imediatamente uma execução para um query programado específico

Você pode disparar imediatamente uma execução para um query programado especificado fazendo uma solicitação POST para o `/schedules/{SCHEDULE_ID}/runs` ponto final, onde `{SCHEDULE_ID}` é o `id` valor do query programado cuja execução você deseja acionar.

**Formato da API**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Recuperar detalhes de uma execução para um query agendado específico

Você pode recuperar detalhes sobre uma execução para um query programado específico, fazendo uma solicitação GET ao `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` terminal e fornecendo a ID do query programado e a execução no caminho da solicitação.

**Formato da API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do query agendado cuja execução você deseja recuperar detalhes. |
| `{RUN_ID}` | O `id` valor da execução que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

### Interromper imediatamente uma execução para um query programado específico

Você pode interromper imediatamente uma execução de um query programado específico fazendo uma solicitação PATCH para o `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` ponto final e fornecendo a ID do query programado e a execução no caminho da solicitação.

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do query agendado cuja execução você deseja recuperar detalhes. |
| `{RUN_ID}` | O `id` valor da execução que você deseja recuperar. |

**Solicitação**

Essa solicitação de API usa a sintaxe do Patch JSON para sua carga. Para obter mais informações sobre como a correção JSON funciona, leia o documento de fundamentos da API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
