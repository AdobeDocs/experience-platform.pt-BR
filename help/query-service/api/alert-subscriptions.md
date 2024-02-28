---
keywords: Experience Platform;início;tópicos populares;serviço de consulta;Serviço de consulta;alerta;
title: Ponto de Extremidade de Assinaturas de Alerta
description: Este guia fornece exemplos de solicitações HTTP e respostas para as várias chamadas de API que você pode fazer para o endpoint de assinaturas de alerta com a API de serviço de consulta.
role: Developer
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2666'
ht-degree: 2%

---

# Endpoint de assinaturas de alerta

O Adobe Experience Platform Query Service permite assinar alertas para consultas ad hoc e programadas. Os alertas podem ser recebidos por email, na interface do usuário da Platform, ou em ambos. O conteúdo da notificação é o mesmo para alertas na plataforma e alertas de email. Atualmente, alertas de consulta só podem ser inscritos usando o [API do serviço de consulta](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>Para receber alertas de email, primeiro você deve ativar essa configuração na interface do usuário. Consulte a documentação para [instruções sobre como ativar alertas de email](../../observability/alerts/ui.md#enable-email-alerts).

A tabela abaixo explica os tipos de alertas compatíveis com diferentes tipos de consultas:

| Tipo de consulta | Tipos de alerta suportados |
|---|---|
| Consultas ad hoc | `success` ou `failed` execuções. |
| Consultas programadas | `start`, `success`ou `failed` execuções. |

>[!NOTE]
>
>Todas as consultas não SELECT suportam assinaturas de alerta e você não precisa ser o criador da consulta para assinar um alerta. Outros usuários também podem se inscrever em alertas em uma consulta que não tenha sido criada.

Os seguintes alertas se aplicam sem uma assinatura de alerta:

* Quando um trabalho de consulta em lote é concluído, os usuários recebem uma notificação.
* Quando a duração de um trabalho de consulta em lote excede um limite, um alerta é acionado para a pessoa que agendou a consulta.

>[!NOTE]
>
>As consultas usadas para teste podem ser excluídas desses alertas se configuradas adequadamente.

## Exemplos de chamadas de API

As seções a seguir abordam as várias chamadas de API que podem ser feitas usando a API do Serviço de consulta. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

## Recuperar uma lista de todos os alertas de uma organização e uma sandbox {#get-list-of-org-alert-subs}

Recupere uma lista de todos os alertas para uma sandbox da organização fazendo uma solicitação GET para o `/alert-subscriptions` terminal.

**Formato da API**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| Propriedade | Descrição |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | (Opcional) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (&amp;). Os parâmetros disponíveis estão listados abaixo. |

**Parâmetros de consulta**

Veja a seguir uma lista de parâmetros de consulta disponíveis para consultas de listagem. Todos esses parâmetros são opcionais. Fazer uma chamada para esse endpoint sem parâmetros recuperará todas as consultas disponíveis para sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `orderby` | O campo que especifica a ordem dos resultados. Os campos compatíveis são `created` e `updated`. Incluir o nome da propriedade como prefixo `+` para ascendente e `-` para ordem decrescente. O padrão é `-created`. Observe que o sinal de mais (`+`) tem de ser evitada com `%2B`. Por exemplo `%2Bcreated` é o valor de uma ordem criada crescente. |
| `pagesize` | Use esse parâmetro para controlar o número de registros que você deseja obter da chamada de API por página. O limite padrão é definido com a quantidade máxima de 50 registros por página. |
| `page` | Indique o número da página dos resultados retornados para os quais você deseja ver os registros. |
| `property` | Filtre os resultados com base nos campos escolhidos. Os filtros **deve** ser escapado por HTML. As vírgulas são usadas para combinar vários conjuntos de filtros. As seguintes propriedades permitem a filtragem: <ul><li>id</li><li>assetId</li><li>status</li><li>alertType</li></ul> Os operadores compatíveis são `==` (igual a). Por exemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retornará o alerta com uma ID correspondente. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna um status HTTP 200 e a variável `alerts` matriz com informações de paginação e versão. A variável `alerts` O array contém detalhes de todos os alertas para uma organização e uma sandbox específica. No máximo três alertas estão disponíveis por resposta. Um alerta para cada tipo de alerta está contido no corpo da resposta.

>[!NOTE]
>
>A variável `alerts._links` objeto no `alerts` a matriz foi truncada por brevidade. Um exemplo completo da `alerts._links` o objeto pode ser encontrado no [resposta da solicitação POST](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `alerts.assetId` | A ID da consulta que associou o alerta a uma consulta específica. |
| `alerts.id` | O nome do alerta. Esse nome é gerado pelo serviço Alertas e é usado no painel Alertas. O nome do alerta é composto da pasta que armazena o alerta, a variável `alertType`e a ID do fluxo. Informações sobre os alertas disponíveis podem ser encontradas no [Documentação do painel de Alertas da plataforma](../../observability/alerts/ui.md). |
| `alerts.status` | O alerta tem quatro valores de status: `enabled`, `enabling`, `disabled`, e `disabling`. Um alerta está ouvindo ativamente os eventos, pausado para uso futuro enquanto mantém todos os assinantes e configurações relevantes ou em transição entre esses estados. |
| `alerts.alertType` | O tipo de alerta. Há três valores possíveis para um alerta: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul> |
| `alerts._links` | Fornece informações sobre os métodos e endpoints disponíveis que podem ser usados para recuperar, atualizar, editar ou excluir informações relacionadas a esta ID de alerta. |
| `_page` | O objeto contém propriedades para descrever a ordem, o tamanho, o número total de páginas e a página atual. |
| `_links` | O objeto contém referências de URI que podem ser usadas para obter a página de recursos seguinte ou anterior. |

## Recuperar as informações de assinatura de alerta para uma consulta específica ou ID de agendamento {#retrieve-all-alert-subscriptions-by-id}

Recupere as informações de assinatura de alerta para uma ID de consulta específica ou ID de agendamento fazendo uma solicitação GET para o `/alert-subscriptions/{QUERY_ID}` ou o `/alert-subscriptions/{SCHEDULE_ID}` terminal.

**Formato da API**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{QUERY_ID}` | A ID da consulta para a qual você deseja retornar as informações de assinatura. |
| `{SCHEDULE_ID}` | A ID da consulta agendada para a qual você deseja retornar as informações de assinatura. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna um status HTTP de 200 e a variável `alerts` matriz que contém informações de assinatura da consulta ou ID de agendamento fornecida.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `assetId` | O alerta está associado a essa ID. A ID pode ser uma ID de consulta ou uma ID de agendamento. |
| `id` | O nome do alerta. Esse nome é gerado pelo serviço Alertas e é usado no painel Alertas. O nome do alerta é composto da pasta que armazena o alerta, a variável `alertType`e a ID do fluxo. Informações sobre os alertas disponíveis podem ser encontradas no [Documentação do painel de Alertas da plataforma](../../observability/alerts/ui.md). |
| `status` | O alerta tem quatro valores de status: `enabled`, `enabling`, `disabled`, e `disabling`. Um alerta está ouvindo ativamente os eventos, pausado para uso futuro enquanto mantém todos os assinantes e configurações relevantes ou em transição entre esses estados. |
| `alertType` | Cada alerta pode ter três tipos diferentes. São eles: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul> |
| `subscriptions.emailNotifications` | Uma matriz de endereços de email registrados em Adobe para usuários que se inscreveram para receber emails do alerta. |
| `subscriptions.inContextNotifications` | Uma matriz de endereços de email registrados em Adobe para usuários que assinaram notificações da interface do usuário para o alerta. |

## Recuperar informações de assinatura de alerta para uma determinada consulta ou ID de agendamento e tipo de alerta {#get-alert-info-by-id-and-alert-type}

Recupere as informações de assinatura do alerta para uma ID e um tipo de alerta específicos fazendo uma solicitação GET para o `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` terminal. Isso se aplica às IDs de consulta ou consulta programada.

**Formato da API**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parâmetros | Descrição |
| -------- | ----------- |
| `ALERT_TYPE` | Essa propriedade descreve o estado de execução da consulta que aciona um alerta. A resposta só incluirá informações de assinatura de alerta para alertas desse tipo. Cada alerta pode ter três tipos diferentes. São eles: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul> |
| `QUERY_ID` | O identificador exclusivo da consulta a ser atualizada. |
| `SCHEDULE_ID` | O identificador exclusivo da consulta agendada a ser atualizada. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna um status HTTP 200 e todos os alertas nos quais você está inscrito. Isso inclui a ID do alerta, o tipo de alerta, as IDs de email registradas do Adobe do assinante e o canal de notificação preferido.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `assetId` | A ID da consulta que associou o alerta a uma consulta específica. |
| `alertType` | O tipo de alerta. Há três valores possíveis para um alerta: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul> |
| `subscriptions` | Um objeto usado para transmitir as IDs de email registradas do Adobe associadas aos alertas e os canais nos quais os usuários receberão os alertas. |
| `subscriptions.inContextNotifications` | Uma matriz de endereços de email registrados em Adobe para usuários que assinaram notificações da interface do usuário para o alerta. |
| `subscriptions.emailNotifications` | Uma matriz de endereços de email registrados em Adobe para usuários que se inscreveram para receber emails do alerta. |

## Recuperar uma lista de todos os alertas que um usuário assina {#get-alert-subscription-list}

Recupere uma lista de todos os alertas que um usuário assina fazendo uma solicitação GET para o `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` terminal. A resposta inclui o nome do alerta, as IDs, o status, o tipo de alerta e os canais de notificação.

**Formato da API**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parâmetros | Descrição |
| -------- | ----------- |
| `{EMAIL_ID}` | Um endereço de email que está registrado em uma conta Adobe, é usado para identificar os usuários inscritos nos alertas. |
| `orderby` | O campo que especifica a ordem dos resultados. Os campos compatíveis são `created` e `updated`. Incluir o nome da propriedade como prefixo `+` para ascendente e `-` para ordem decrescente. O padrão é `-created`. Observe que o sinal de mais (`+`) tem de ser evitada com `%2B`. Por exemplo `%2Bcreated` é o valor de uma ordem criada crescente. |
| `pagesize` | Use esse parâmetro para controlar o número de registros que você deseja obter da chamada de API por página. O limite padrão é definido com a quantidade máxima de 50 registros por página. |
| `page` | Indique o número da página dos resultados retornados para os quais você deseja ver os registros. |
| `property` | Filtre os resultados com base nos campos escolhidos. Os filtros **deve** ser escapado por HTML. As vírgulas são usadas para combinar vários conjuntos de filtros. As seguintes propriedades permitem a filtragem: <ul><li>id</li><li>assetId</li><li>status</li><li>alertType</li></ul> Os operadores compatíveis são `==` (igual a). Por exemplo, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` retornará o alerta com uma ID correspondente. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 e a variável `items` com detalhes dos alertas assinados pelo `emailId` fornecidos.

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome do alerta. Esse nome é gerado pelo serviço Alertas e é usado no painel Alertas. O nome do alerta é composto da pasta que armazena o alerta, a variável `alertType`e a ID do fluxo. Informações sobre os alertas disponíveis podem ser encontradas no [Documentação do painel de Alertas da plataforma](../../observability/alerts/ui.md). |
| `assetId` | A ID da consulta que associou o alerta a uma consulta específica. |
| `status` | O alerta tem quatro valores de status: `enabled`, `enabling`, `disabled`, e `disabling`. Um alerta está ouvindo ativamente os eventos, pausado para uso futuro enquanto mantém todos os assinantes e configurações relevantes ou em transição entre esses estados. |
| `alertType` | O tipo de alerta. Há três valores possíveis para um alerta: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul> |
| `subscriptions` | Um objeto usado para transmitir as IDs de email registradas do Adobe associadas aos alertas e os canais nos quais os usuários receberão os alertas. |
| `subscriptions.inContextNotifications` | Um valor booleano que determina como os usuários recebem notificações de alerta. A `true` O valor confirma que os alertas devem ser fornecidos por meio da interface do usuário. A `false` garante que os usuários não sejam notificados por meio desse canal. |
| `subscriptions.emailNotifications` | Um valor booleano que determina como os usuários recebem notificações de alerta. A `true` O valor confirma que os alertas devem ser fornecidos por email. A `false` garante que os usuários não sejam notificados por meio desse canal. |

## Criar um alerta e inscrever usuários {#subscribe-users}

Para criar um alerta e assinar um usuário para recebê-lo, faça um `POST` solicitação à `/alert-subscriptions` terminal. Esta solicitação associa uma consulta a um alerta recém-criado usando um `assetId` propriedade e assina os usuários aos alertas para essa consulta por meio do uso de `emailIds`.

>[!IMPORTANT]
>
>Você pode enviar até cinco IDs de email registradas Adobe em uma única solicitação. Para inscrever mais de cinco usuários em um alerta, é necessário fazer solicitações subsequentes.

**Formato da API**

```http
POST /alert-subscriptions
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `assetId` | O alerta está associado a essa ID. A ID pode ser uma ID de consulta ou uma ID de agendamento. |
| `alertType` | O tipo de alerta. Há três valores possíveis para um alerta: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul> |
| `subscriptions` | Um objeto usado para transmitir as IDs de email registradas do Adobe associadas aos alertas e os canais nos quais os usuários receberão os alertas. |
| `subscriptions.emailIds` | Uma matriz de endereços de email para identificar os usuários que devem receber os alertas. Os endereços de email **deve** ser registrado em uma conta Adobe. |
| `subscriptions.inContextNotifications` | Um valor booleano que determina como os usuários recebem notificações de alerta. A `true` O valor confirma que os alertas devem ser fornecidos por meio da interface do usuário. A `false` garante que os usuários não sejam notificados por meio desse canal. |
| `subscriptions.emailNotifications` | Um valor booleano que determina como os usuários recebem notificações de alerta. A `true` O valor confirma que os alertas devem ser fornecidos por email. A `false` garante que os usuários não sejam notificados por meio desse canal. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Aceito) com detalhes do alerta recém-criado.

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O nome do alerta. Esse nome é gerado pelo serviço Alertas e é usado no painel Alertas. O nome do alerta é composto da pasta que armazena o alerta, a variável `alertType`e a ID do fluxo. Informações sobre os alertas disponíveis podem ser encontradas no [Documentação do painel de Alertas da plataforma](../../observability/alerts/ui.md). |
| `_links` | Fornece informações sobre os métodos e endpoints disponíveis que podem ser usados para recuperar, atualizar, editar ou excluir informações relacionadas a esta ID de alerta. |

## Ativar ou desativar um alerta {#enable-or-disable-alert}

Esta solicitação faz referência a um alerta específico usando uma consulta ou ID de agendamento e um tipo de alerta e atualiza o status do alerta para `enable` ou `disable`. Você pode atualizar o status de um alerta fazendo uma `PATCH` solicitação à `/alert-subscriptions/{queryId}/{alertType}` ou `/alert-subscriptions/{scheduleId}/{alertType}` terminal.

**Formato da API**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parâmetros | Descrição |
| -------- | ----------- |
| `ALERT_TYPE` | O tipo de alerta. Há três valores possíveis para um alerta: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul>Você deve especificar o tipo de alerta atual no namespace do ponto de extremidade para alterá-lo. |
| `QUERY_ID` | O identificador exclusivo da consulta a ser atualizada. |
| `SCHEDULE_ID` | O identificador exclusivo da consulta agendada a ser atualizada. |

**Solicitação**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `op` | A operação a ser executada. Atualmente, o único valor aceito é `replace`. |
| `path` | Esse valor está relacionado ao namespace no endpoint. Atualmente, o único valor aceito é `/status`. |
| `value` | Em uma solicitação de PATCH bem-sucedida, isso altera o `status` valor do alerta. Atualmente, os valores aceitos são `enable` ou `disable`. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes sobre o status, o tipo e a ID do alerta, bem como a consulta à qual ele está relacionado.

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O nome do alerta. Esse nome é gerado pelo serviço Alertas e é usado no painel Alertas. O nome do alerta é composto da pasta que armazena o alerta, a variável `alertType`e a ID do fluxo. Informações sobre os alertas disponíveis podem ser encontradas no [Documentação do painel de Alertas da plataforma](../../observability/alerts/ui.md). |
| `assetId` | O alerta está associado a essa ID. A ID pode ser uma ID de consulta ou uma ID de agendamento. |
| `alertType` | Cada alerta pode ter três tipos diferentes. São eles: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul> |
| `status` | O alerta tem quatro valores de status: `enabled`, `enabling`, `disabled`, e `disabling`. Um alerta está ouvindo ativamente os eventos, pausado para uso futuro enquanto mantém todos os assinantes e configurações relevantes ou em transição entre esses estados. |

## Excluir o alerta para uma consulta e um tipo de alerta específicos {#delete-alert-info-by-id-and-alert-type}

Exclua um alerta para uma consulta específica ou ID de programação e tipo de alerta fazendo uma solicitação DELETE para o `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` ou `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` terminal.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parâmetros | Descrição |
| -------- | ----------- |
| `ALERT_TYPE` | O tipo de alerta. Há três valores possíveis para um alerta: <ul><li>`start`: notifica um usuário quando a execução da consulta começou.</li><li>`success`: notifica o usuário quando a consulta é concluída.</li><li>`failure`: notifica o usuário se a consulta falhar.</li></ul> A solicitação DELETE se aplica somente ao tipo de alerta específico fornecido. |
| `QUERY_ID` | O identificador exclusivo da consulta a ser atualizada. |
| `SCHEDULE_ID` | O identificador exclusivo da consulta agendada a ser atualizada. |

**Solicitação**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna um status HTTP 200 e uma mensagem de confirmação que inclui a ID do ativo e o tipo de alerta do alerta excluído.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Próximas etapas

Este guia abordou o uso do `/alert-subscriptions` endpoint na API do Serviço de consulta. Depois de ler este guia, você compreenderá melhor como criar um alerta para uma consulta, inscrever usuários no alerta, os tipos de alertas disponíveis e como as informações de inscrição do alerta podem ser recuperadas, atualizadas e excluídas.

Consulte a [Guia da API do Serviço de consulta](./getting-started.md) para saber mais sobre outros recursos e operações disponíveis.
