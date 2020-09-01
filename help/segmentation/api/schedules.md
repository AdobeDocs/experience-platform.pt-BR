---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;schedules;schedule;api;API;
solution: Experience Platform
title: Programações
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 3%

---


# Ponto de extremidade de programação

As programações são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia. Você pode usar o `/config/schedules` ponto de extremidade para recuperar uma lista de programações, criar uma nova programação, recuperar detalhes de uma programação específica, atualizar uma programação específica ou excluir uma programação específica.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte o guia [de](./getting-started.md) introdução para obter informações importantes que você precisa saber para fazer chamadas à API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

## Recuperar uma lista de programações {#retrieve-list}

Você pode recuperar uma lista de todas as programações para sua Organização IMS, fazendo uma solicitação de GET para o `/config/schedules` endpoint.

**Formato da API**

O `/config/schedules` terminal suporta vários parâmetros de query para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Efetuar uma chamada para este terminal sem parâmetros recuperará todos os agendamentos disponíveis para a sua organização. Vários parâmetros podem ser incluídos, separados por E comercial (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{START}` | Especifica de qual página o deslocamento será start. Por padrão, esse valor será 0. |
| `{LIMIT}` | Especifica o número de programações retornadas. Por padrão, esse valor será 100. |

**Solicitação**

A solicitação a seguir recuperará os dez últimos agendamentos publicados na sua Organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de agendamentos para a organização IMS especificada como JSON.

>[!NOTE]
>
>A resposta a seguir foi truncada para espaço e mostra somente a primeira programação retornada.

```json
{
    "_page": {
        "totalCount": 10,
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

| Propriedade | Descrição |
| -------- | ------------ |
| `_page.totalCount` | O número total de programações retornadas. |
| `_page.pageSize` | O tamanho da página de agendamentos. |
| `children.name` | O nome do agendamento como uma string. |
| `children.type` | O tipo de tarefa como uma string. Os dois tipos suportados são &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `children.properties` | Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `children.properties.segments` | Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `children.schedule` | Uma string que contém a programação da tarefa. As ordens de produção só podem ser programadas para execução uma vez por dia, o que significa que você não pode programar uma ordem de produção para execução mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações de cron, leia a documentação do formato [de expressão de](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado à meia-noite no primeiro de cada mês. |
| `children.state` | Uma string contendo o estado da programação. Os dois estados suportados são &quot;ativos&quot; e &quot;inativos&quot;. Por padrão, o estado é definido como &quot;inativo&quot;. |

## Create a new schedule {#create}

Você pode criar uma nova programação fazendo uma solicitação POST para o `/config/schedules` endpoint.

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
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Propriedade | Descrição |
| -------- | ------------ |
| `name` | **Obrigatório.** O nome do agendamento como uma string. |
| `type` | **Obrigatório.** O tipo de tarefa como uma string. Os dois tipos suportados são &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `properties` | **Obrigatório.** Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | **Obrigatório quando`type`é igual a &quot;batch_segmentation&quot;.** Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | *Opcional.* Uma string que contém a programação da tarefa. As ordens de produção só podem ser programadas para execução uma vez por dia, o que significa que você não pode programar uma ordem de produção para execução mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações de cron, leia a documentação do formato [de expressão de](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado à meia-noite no primeiro de cada mês. <br><br>Se essa string não for fornecida, um agendamento gerado pelo sistema será gerado automaticamente. |
| `state` | *Opcional.* Uma string contendo o estado da programação. Os dois estados suportados são &quot;ativos&quot; e &quot;inativos&quot;. Por padrão, o estado é definido como &quot;inativo&quot;. |

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

## Recuperar uma programação específica {#get}

Você pode recuperar informações detalhadas sobre um agendamento específico, fazendo uma solicitação de GET para o `/config/schedules` endpoint e fornecendo a ID do agendamento que deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do agendamento que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
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
}
```

| Propriedade | Descrição |
| -------- | ------------ |
| `name` | O nome do agendamento como uma string. |
| `type` | O tipo de tarefa como uma string. Os dois tipos suportados são `batch_segmentation` e `export`. |
| `properties` | Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | Uma string que contém a programação da tarefa. As ordens de produção só podem ser programadas para execução uma vez por dia, o que significa que você não pode programar uma ordem de produção para execução mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações de cron, leia a documentação do formato [de expressão de](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado à meia-noite no primeiro de cada mês. |
| `state` | Uma string contendo o estado da programação. Os dois estados suportados são `active` e `inactive`. By default, the state is set to `inactive`. |

## Atualizar detalhes de uma programação específica {#update}

Você pode atualizar um agendamento específico, fazendo uma solicitação de PATCH para o `/config/schedules` endpoint e fornecendo a ID do agendamento que você está tentando atualizar no caminho da solicitação.

A solicitação de PATCH permite atualizar o [estado](#update-state) ou a programação [de](#update-schedule) cron para uma programação individual.

### Atualizar estado do agendamento {#update-state}

Você pode usar uma operação de Patch JSON para atualizar o estado da programação. Para atualizar o estado, declare a `path` propriedade como `/state` e defina `value` como `active` ou `inactive`. Para obter mais informações sobre o Patch JSON, leia a documentação do Patch [](http://jsonpatch.com/) JSON.

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do agendamento que você deseja atualizar. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
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
]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o estado do agendamento, é necessário definir o valor de `path` para &quot;/state&quot;. |
| `value` | O valor atualizado do estado do agendamento. Esse valor pode ser definido como &quot;ativo&quot; ou &quot;inativo&quot; para ativar ou desativar o agendamento. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

### Atualizar agendamento do cron {#update-schedule}

Você pode usar uma operação de Patch JSON para atualizar a programação de cron. Para atualizar o agendamento, declare a `path` propriedade como `/schedule` e defina o `value` como um agendamento de cron válido. Para obter mais informações sobre o Patch JSON, leia a documentação do Patch [](http://jsonpatch.com/) JSON. Para obter mais informações sobre programações de cron, leia a documentação do formato [de expressão de](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do agendamento que você deseja atualizar. |

**Solicitação**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `path` | O caminho do valor que você deseja atualizar. Nesse caso, como você está atualizando a programação de cron, é necessário definir o valor de `path` como `/schedule`. |
| `value` | O valor atualizado da programação de cron. Esse valor precisa estar na forma de um cronograma de execução. Neste exemplo, o agendamento será executado no segundo de cada mês. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

## Excluir uma programação específica

Você pode solicitar a exclusão de uma programação específica, fazendo uma solicitação de DELETE para o `/config/schedules` ponto final e fornecendo a ID da programação que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do agendamento que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

## Próximas etapas

Depois de ler este guia, agora você tem um melhor entendimento de como os agendamentos funcionam.