---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Programações
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Agende o guia do desenvolvedor

introdução

- Recuperar uma lista de programações
- Criar um novo agendamento
- Recuperar uma programação específica
- Atualizar um agendamento específico
- Excluir uma programação específica

## Introdução

Os pontos finais da API usados neste guia fazem parte da API de segmentação. Antes de continuar, consulte o guia [do desenvolvedor de](./getting-started.md)Segmentação.

Em particular, a seção [de](./getting-started.md#getting-started) introdução do guia do desenvolvedor de Segmentação inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra no documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API da plataforma de experiência.

## Recuperar uma lista de programações

Você pode recuperar uma lista de todas as programações para sua Organização IMS, fazendo uma solicitação GET ao `/config/schedules` endpoint.

**Formato da API**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Opcional*) Parâmetros adicionados ao caminho da solicitação que configuram os resultados retornados na resposta. Vários parâmetros podem ser incluídos, separados por E comercial (`&`). Os parâmetros disponíveis estão listados abaixo.

**Parâmetros do Query**

A seguir está uma lista de parâmetros de query disponíveis para agendamento de lista. Todos esses parâmetros são opcionais. Efetuar uma chamada para este terminal sem parâmetros recuperará todos os agendamentos disponíveis para a sua organização.

| Parâmetro | Descrição |
| --------- | ----------- |
| `start` | Especifica de qual página o deslocamento será start. Por padrão, esse valor será 0. |
| `limit` | Especifica o número de programações retornadas. Por padrão, esse valor será 100. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de agendamentos para a organização IMS especificada como JSON.

```json
{
    "_page": {
        "totalCount": 1,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## Criar um novo agendamento

Você pode criar uma nova programação fazendo uma solicitação POST para o `/config/schedules` ponto de extremidade.

**Formato da API**

```http
POST /config/schedules
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| Parâmetro | Descrição |
| --------- | ------------ |
| `name` | **Obrigatório.** O nome do agendamento como uma string. |
| `type` | **Obrigatório.** O tipo de tarefa como uma string. Os dois tipos suportados são `batch_segmentation` e `export`. |
| `properties` | **Obrigatório.** Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | **Obrigatório quando`type`igual`batch_segmentation`.** Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | **Obrigatório.** Uma string que contém a programação da tarefa. Para obter mais informações sobre programações de cron, leia a documentação do formato [de expressão de](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado à meia-noite no primeiro de cada mês. |
| `state` | *Opcional.* Uma string contendo o estado da programação. Os dois estados suportados são `active` e `inactive`. Por padrão, o estado é definido como `inactive`. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do agendamento recém-criado.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## Recuperar uma programação específica

Você pode recuperar informações detalhadas sobre uma programação específica fazendo uma solicitação GET ao ponto de extremidade `/config/schedules` e fornecendo o `id` valor da programação no caminho da solicitação.

**Formato da API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: O `id` valor do agendamento que você deseja recuperar.

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o agendamento especificado.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
```

## Atualizar detalhes de uma programação específica

Você pode atualizar uma programação especificada fazendo uma solicitação PATCH para o `/config/schedules` ponto final e fornecendo o `id` valor da programação no caminho da solicitação.

A solicitação PATCH suporta dois caminhos diferentes: `/state` e `/schedule`.

### Atualizar estado do agendamento

Pode utilizar `/state` para atualizar o estado do agendamento - ATIVO ou INATIVO. Para atualizar o estado, é necessário definir o valor como `active` ou `inactive`.

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: O `id` valor do agendamento que você deseja atualizar.

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/state",
    "value": "active"
  }
]
'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o estado do agendamento, é necessário definir o valor de `path` como `/state`. |
| `value` | O valor atualizado do `/state`. Esse valor pode ser definido como `active` ou `inactive` para ativar ou desativar o agendamento. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

### Atualizar agendamento de execução de programação

Você pode usar `schedule` para atualizar o cronograma de execução. Para obter mais informações sobre programações de cron, leia a documentação do formato [de expressão de](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: O `id` valor do agendamento que você deseja atualizar.

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o cronograma de execução da programação, é necessário definir o valor de `path` como `/schedule`. |
| `value` | O valor atualizado do `/state`. Esse valor precisa estar na forma de um cronograma de execução. Neste exemplo, o agendamento será executado no segundo de cada mês. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

## Excluir uma programação específica

Você pode solicitar a exclusão de um agendamento especificado fazendo uma solicitação DELETE para o e fornecendo o `/config/schedules` `id` valor do agendamento no caminho da solicitação.

**Formato da API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: O `id` valor do agendamento que você deseja excluir.

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) com a seguinte mensagem:

```json
(No Content) Schedule deleted successfully
```

## Próximas etapas
