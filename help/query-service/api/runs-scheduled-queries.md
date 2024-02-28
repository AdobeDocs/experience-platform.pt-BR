---
keywords: Experience Platform;início;tópicos populares;serviço de consulta;executar consultas agendadas;executar consulta agendada;serviço de consulta;consultas agendadas;consulta agendada;
solution: Experience Platform
title: Ponto de Extremidade da API de Execuções de Consulta Agendada
description: As seções a seguir abordam as várias chamadas de API que podem ser feitas para executar consultas programadas com a API de serviço de consulta.
role: Developer
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# Ponto de extremidade de execuções de consulta agendada

## Exemplos de chamadas de API

Agora que você entende quais cabeçalhos usar, você está pronto para começar a fazer chamadas para o [!DNL Query Service] API. As seções a seguir abordam as várias chamadas de API que podem ser feitas usando o [!DNL Query Service] API. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

### Recupera uma lista de todas as execuções de uma consulta agendada especificada

Você pode recuperar uma lista de todas as execuções de uma consulta agendada específica, independentemente de estarem em execução no momento ou já concluídas. Isso é feito fazendo uma solicitação GET ao `/schedules/{SCHEDULE_ID}/runs` endpoint, onde `{SCHEDULE_ID}` é o `id` valor da consulta programada cujas execuções você deseja recuperar.

**Formato da API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | A variável `id` valor da consulta programada que deseja recuperar. |
| `{QUERY_PARAMETERS}` | (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros de consulta**

Veja a seguir uma lista de parâmetros de consulta disponíveis para execuções de listagem para uma consulta programada especificada. Todos esses parâmetros são opcionais. Fazer uma chamada para esse ponto de extremidade sem parâmetros recuperará todas as execuções disponíveis para a consulta agendada especificada.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | Especifica o campo pelo qual ordenar resultados. Os campos compatíveis são `created` e `updated`. Por exemplo, `orderby=created` Os resultados serão classificados por criados em ordem crescente. Adicionar um `-` antes de criar (`orderby=-created`) classificará os itens por criados em ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20*) |
| `start` | Especifique um carimbo de data e hora no formato ISO para ordenar os resultados. Se nenhuma data de início for especificada, a chamada da API retornará as execuções mais antigas primeiro e, em seguida, continuará a listar os resultados mais recentes<br> Os carimbos de data e hora ISO permitem diferentes níveis de granularidade na data e hora. Os carimbos de data e hora ISO básicos têm o formato de: `2020-09-07` para expressar a data em 7 de setembro de 2020. Um exemplo mais complexo seria escrito como `2022-11-05T08:15:30-05:00` e corresponde a 5 de novembro de 2022, 8:15:30 da manhã, Hora Padrão do Leste dos EUA. Um fuso horário pode ser fornecido com um deslocamento UTC e é indicado pelo sufixo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se nenhum fuso horário for fornecido, o padrão será zero. |
| `property` | Filtrar resultados com base em campos. Os filtros **deve** ser escapado por HTML. As vírgulas são usadas para combinar vários conjuntos de filtros. Os campos compatíveis são `created`, `state`, e `externalTrigger`. A lista de operadores compatíveis é `>` (maior que), `<` (menor que) e  `==` (igual a) e `!=` (diferente de). Por exemplo, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` retornará todas as execuções criadas manualmente, bem-sucedidas e criadas após 20 de abril de 2019. |

**Solicitação**

A solicitação a seguir recupera as quatro últimas execuções para a consulta programada especificada.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de execuções para a consulta agendada especificada como JSON. A resposta a seguir retorna as quatro últimas execuções da consulta agendada especificada.

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

### Acionar imediatamente uma execução para uma consulta programada específica

Você pode acionar imediatamente uma execução para uma consulta agendada especificada fazendo uma solicitação POST para o `/schedules/{SCHEDULE_ID}/runs` endpoint, onde `{SCHEDULE_ID}` é o `id` valor da consulta programada cuja execução você deseja acionar.

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

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Recuperar detalhes de uma execução para uma consulta agendada específica

Você pode recuperar detalhes sobre uma execução para uma consulta agendada específica fazendo uma solicitação GET para a `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` e fornecendo a ID da consulta agendada e a execução no caminho da solicitação.

**Formato da API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | A variável `id` valor da consulta programada cuja execução você deseja recuperar detalhes. |
| `{RUN_ID}` | A variável `id` valor da execução que você deseja recuperar. |

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

### Interromper imediatamente uma execução para uma consulta programada específica

Você pode interromper imediatamente uma execução para uma consulta agendada específica fazendo uma solicitação PATCH para o `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` e fornecendo a ID da consulta agendada e a execução no caminho da solicitação.

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | A variável `id` valor da consulta programada cuja execução você deseja recuperar detalhes. |
| `{RUN_ID}` | A variável `id` valor da execução que você deseja recuperar. |

**Solicitação**

Essa solicitação de API usa a sintaxe do patch de JSON para sua carga. Para obter mais informações sobre como o Patch JSON funciona, leia o documento Fundamentos da API.

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

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
