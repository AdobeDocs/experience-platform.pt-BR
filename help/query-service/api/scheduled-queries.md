---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consultas agendadas;consulta agendada;
solution: Experience Platform
title: Endpoint de agendamentos
description: As seções a seguir abordam as várias chamadas de API que podem ser feitas para consultas programadas com a API de serviço de consulta.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 2%

---

# Endpoint de agendamentos

Saiba como criar, gerenciar e monitorar consultas agendadas de forma programática usando a API de agendamentos do Serviço de consulta com informações detalhadas e exemplos.

## Requisitos e pré-requisitos

Você pode criar consultas programadas usando uma conta técnica (autenticada por meio de credenciais de servidor para servidor do OAuth) ou uma conta de usuário pessoal (token de usuário). No entanto, a Adobe recomenda utilizar uma conta técnica para garantir a execução ininterrupta e segura de consultas programadas, especialmente para cargas de trabalho de longo prazo ou de produção.

Os queries criados com uma conta de usuário pessoal falharão se o acesso desse usuário for revogado ou sua conta for desativada. As contas técnicas oferecem maior estabilidade porque não estão vinculadas ao status de emprego ou aos direitos de acesso de um usuário individual.

>[!IMPORTANT]
>
>Considerações importantes ao gerenciar consultas programadas:<ul><li>As consultas programadas falharão se a conta (técnica ou usuário) usada para criá-las perder acesso ou permissões.</li><li>As consultas programadas devem ser desativadas antes de excluir por meio da API ou da interface do usuário.</li><li>Não há suporte para agendamento indefinido sem uma data final; uma data final deve ser sempre especificada.</li></ul>

Para obter orientações detalhadas sobre requisitos de conta, configuração de permissões e gerenciamento de consultas agendadas, consulte a [Documentação de agendamentos de consulta](../ui/query-schedules.md#technical-account-user-requirements). Para obter instruções passo a passo sobre como criar e configurar uma conta técnica, consulte a [instalação do Developer Console](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman) e a [configuração completa de conta técnica](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup).

## Exemplos de chamadas de API

Após configurar os cabeçalhos de autenticação necessários (consulte o [guia de autenticação de API](../../landing/api-authentication.md)), você pode começar a fazer chamadas para a API [!DNL Query Service]. As seções a seguir demonstram várias chamadas de API com formatos gerais, exemplos de solicitações, incluindo cabeçalhos obrigatórios e exemplos de respostas.

### Recuperar uma lista de consultas agendadas

Você pode recuperar uma lista de todas as consultas agendadas para sua organização fazendo uma solicitação GET para o ponto de extremidade `/schedules`.

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
| `orderby` | Especifica o campo pelo qual ordenar resultados. Os campos com suporte são `created` e `updated`. Por exemplo, `orderby=created` classificará os resultados por ordem crescente criada. Adicionar um `-` antes de criar (`orderby=-created`) classificará os itens por ordem decrescente. |
| `limit` | Especifica o limite de tamanho de página para controlar o número de resultados incluídos em uma página. (*Valor padrão: 20*) |
| `start` | Especifique um carimbo de data e hora no formato ISO para ordenar os resultados. Se nenhuma data de início for especificada, a chamada à API retornará primeiro a consulta agendada mais antiga criada e, em seguida, continuará a listar os resultados mais recentes.Os carimbos de data e hora ISO <br> permitem diferentes níveis de granularidade na data e hora. Os carimbos de data e hora ISO básicos assumem o formato de: `2020-09-07` para expressar a data em 7 de setembro de 2020. Um exemplo mais complexo seria escrito como `2022-11-05T08:15:30-05:00` e corresponde a 5 de novembro de 2022, às 8:15:30 am, Hora Padrão do Leste dos EUA. Um fuso horário pode ser fornecido com um deslocamento UTC e é indicado pelo sufixo &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se nenhum fuso horário for fornecido, o padrão será zero. |
| `property` | Filtrar resultados com base em campos. Os filtros **devem** ter HTML com escape. As vírgulas são usadas para combinar vários conjuntos de filtros. Os campos com suporte são `created`, `templateId` e `userId`. A lista de operadores com suporte é `>` (maior que), `<` (menor que) e `==` (igual a). Por exemplo, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` retornará todas as consultas agendadas em que a ID do usuário é a especificada. |

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

Você pode criar uma nova consulta agendada fazendo uma solicitação POST para o ponto de extremidade `/schedules`. Ao criar uma consulta agendada na API, você também pode vê-la no Editor de consultas. Para obter mais informações sobre consultas agendadas na interface, leia a [documentação do Editor de consultas](../ui/user-guide.md#scheduled-queries).

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
| `query.dbName` | O nome do banco de dados em que a consulta agendada será executada. |
| `query.sql` | A consulta SQL a ser executada no agendamento definido. |
| `query.name` | O nome da consulta agendada. |
| `query.description` | Uma descrição opcional para a consulta agendada. |
| `schedule.schedule` | O cronograma cron para a consulta. Consulte [Crontab.guru](https://crontab.guru/) para obter uma maneira interativa de criar, validar e entender expressões cron. Neste exemplo, &quot;`30 * * * *`&quot; significa que a consulta será executada a cada hora na marca de 30 minutos.<br><br>Como alternativa, você pode usar as seguintes expressões abreviadas:<ul><li>`@once`: a consulta é executada apenas uma vez.</li><li>`@hourly`: A consulta é executada a cada hora no início da hora. É equivalente à expressão CRON `0 * * * *`.</li><li>`@daily`: A consulta é executada uma vez por dia à meia-noite. É equivalente à expressão CRON `0 0 * * *`.</li><li>`@weekly`: A consulta é executada uma vez por semana, no domingo, à meia-noite. É equivalente à expressão CRON `0 0 * * 0`.</li><li>`@monthly`: A consulta é executada uma vez por mês, no primeiro dia do mês, à meia-noite. É equivalente à expressão CRON `0 0 1 * *`.</li><li>`@yearly`: A consulta é executada uma vez por ano, em 1º de janeiro, à meia-noite. É equivalente à expressão CRON `0 0 1 1 *`. |
| `schedule.startDate` | A data de início da consulta agendada, gravada como carimbo de data e hora UTC. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com detalhes da consulta agendada recém-criada. Quando a ativação da consulta agendada for concluída, o `state` será alterado de `REGISTERING` para `ENABLED`.

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

Você pode recuperar informações para uma consulta agendada específica fazendo uma solicitação GET para o ponto de extremidade `/schedules` e fornecendo sua ID no caminho da solicitação.

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

Você pode atualizar os detalhes de uma consulta agendada especificada fazendo uma solicitação PATCH para o ponto de extremidade `/schedules` e fornecendo sua ID no caminho da solicitação.

A solicitação PATCH oferece suporte a dois caminhos diferentes: `/state` e `/schedule/schedule`.

### Atualizar estado de consulta agendada

Você pode atualizar o estado da consulta agendada selecionada definindo a propriedade `path` como `/state` e a propriedade `value` como `enable` ou `disable`.

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` da consulta agendada que você deseja PATCH. |


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
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o estado da consulta agendada, é necessário definir o valor de `path` como `/state`. |
| `value` | O valor atualizado de `/state`. Este valor pode ser definido como `enable` ou `disable` para habilitar ou desabilitar a consulta agendada. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com a seguinte mensagem.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Atualizar programação de consulta programada

Você pode atualizar o cronograma cron da consulta agendada definindo a propriedade `path` como `/schedule/schedule` no corpo da solicitação. Para obter mais informações sobre cronogramas cron, leia a documentação [formato de expressão cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Formato da API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` da consulta agendada que você deseja PATCH. |

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
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o agendamento da consulta agendada, é necessário definir o valor de `path` como `/schedule/schedule`. |
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

Você pode excluir uma consulta agendada especificada fazendo uma solicitação DELETE para o ponto de extremidade `/schedules` e fornecendo a ID da consulta agendada que você deseja excluir no caminho da solicitação.

>[!NOTE]
>
>O cronograma **deve** ser desabilitado antes de ser excluído.

**Formato da API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` da consulta agendada que você deseja DELETE. |

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
