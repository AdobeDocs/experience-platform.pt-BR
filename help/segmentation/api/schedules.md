---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; agendamentos; agendamento; api; API;
solution: Experience Platform
title: Agendamentos do Ponto de Extremidade da API
topic-legacy: developer guide
description: Os agendamentos são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 3%

---

# Ponto de extremidade de agendamentos

Os agendamentos são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia. Você pode usar o endpoint `/config/schedules` para recuperar uma lista de programações, criar uma nova programação, recuperar detalhes de uma programação específica, atualizar uma programação específica ou excluir uma programação específica.

## Introdução

Os endpoints usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

## Recuperar uma lista de programações {#retrieve-list}

Você pode recuperar uma lista de todos os agendamentos para sua Organização IMS fazendo uma solicitação de GET para o endpoint `/config/schedules`.

**Formato da API**

O ponto de extremidade `/config/schedules` oferece suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Fazer uma chamada para esse terminal sem parâmetros recuperará todos os agendamentos disponíveis para sua organização. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{START}` | Especifica de qual página o deslocamento começará. Por padrão, esse valor será 0. |
| `{LIMIT}` | Especifica o número de programações retornadas. Por padrão, esse valor será 100. |

**Solicitação**

A solicitação a seguir recuperará as últimas dez programações publicadas na organização IMS.

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
>A resposta a seguir foi truncada para espaço e mostra apenas o primeiro agendamento retornado.

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
| `children.type` | O tipo de trabalho como uma string. Os dois tipos compatíveis são &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `children.properties` | Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `children.properties.segments` | Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `children.schedule` | Uma string que contém a programação de tarefas. As tarefas só podem ser programadas para serem executadas uma vez por dia, o que significa que você não pode programar uma tarefa para ser executada mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações cron, leia a documentação [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado à meia-noite no primeiro de cada mês. |
| `children.state` | Uma string contendo o estado do agendamento. Os dois estados compatíveis são &quot;ativos&quot; e &quot;inativos&quot;. Por padrão, o estado é definido como &quot;inativo&quot;. |

## Criar um novo agendamento {#create}

Você pode criar um novo agendamento fazendo uma solicitação POST para o endpoint `/config/schedules`.

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
| `type` | **Obrigatório.** O tipo de trabalho como uma string. Os dois tipos compatíveis são &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `properties` | **Obrigatório.** Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | **Obrigatório quando  `type` é igual a &quot;batch_segmentation&quot;.** O uso de  `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | *Opcional.* Uma string que contém a programação de tarefas. As tarefas só podem ser programadas para serem executadas uma vez por dia, o que significa que você não pode programar uma tarefa para ser executada mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações cron, leia a documentação [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado à meia-noite no primeiro de cada mês. <br><br>Se essa sequência de caracteres não for fornecida, um agendamento gerado pelo sistema será gerado automaticamente. |
| `state` | *Opcional.* Uma string contendo o estado do agendamento. Os dois estados compatíveis são &quot;ativos&quot; e &quot;inativos&quot;. Por padrão, o estado é definido como &quot;inativo&quot;. |

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

## Recuperar um agendamento específico {#get}

Você pode recuperar informações detalhadas sobre um agendamento específico, fazendo uma solicitação do GET para o endpoint `/config/schedules` e fornecendo a ID do agendamento que deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` do agendamento que deseja recuperar. |

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
| `type` | O tipo de trabalho como uma string. Os dois tipos suportados são `batch_segmentation` e `export`. |
| `properties` | Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | Uma string que contém a programação de tarefas. As tarefas só podem ser programadas para serem executadas uma vez por dia, o que significa que você não pode programar uma tarefa para ser executada mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações cron, leia a documentação [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado à meia-noite no primeiro de cada mês. |
| `state` | Uma string contendo o estado do agendamento. Os dois estados compatíveis são `active` e `inactive`. Por padrão, o estado é definido como `inactive`. |

## Atualizar detalhes de um agendamento específico {#update}

Você pode atualizar um agendamento específico, fazendo uma solicitação PATCH para o endpoint `/config/schedules` e fornecendo a ID do agendamento que está tentando atualizar no caminho da solicitação.

A solicitação PATCH permite atualizar o [state](#update-state) ou o [cron schedule](#update-schedule) para um agendamento individual.

### Atualizar estado do agendamento {#update-state}

Você pode usar uma operação Patch JSON para atualizar o estado do agendamento. Para atualizar o estado, declare a propriedade `path` como `/state` e defina `value` como `active` ou `inactive`. Para obter mais informações sobre o Patch JSON, leia a documentação [Patch JSON](http://jsonpatch.com/).

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` do agendamento que deseja atualizar. |

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
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o estado do agendamento, é necessário definir o valor de `path` como &quot;/state&quot;. |
| `value` | O valor atualizado do estado do agendamento. Esse valor pode ser definido como &quot;ativo&quot; ou &quot;inativo&quot; para ativar ou desativar o agendamento. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

### Atualizar programação de cron {#update-schedule}

Você pode usar uma operação de Patch JSON para atualizar o agendamento do cron. Para atualizar o agendamento, declare a propriedade `path` como `/schedule` e defina `value` como um agendamento cron válido. Para obter mais informações sobre o Patch JSON, leia a documentação [Patch JSON](http://jsonpatch.com/). Para obter mais informações sobre programações cron, leia a documentação [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` do agendamento que deseja atualizar. |

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
| `path` | O caminho do valor que você deseja atualizar. Nesse caso, como você está atualizando o cronograma do cron, é necessário definir o valor de `path` como `/schedule`. |
| `value` | O valor atualizado da programação do cron. Esse valor precisa estar no formato de um cronograma de execução. Neste exemplo, o agendamento será executado no segundo de cada mês. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

## Excluir uma programação específica

Você pode solicitar a exclusão de um agendamento específico, fazendo uma solicitação DELETE para o endpoint `/config/schedules` e fornecendo a ID do agendamento que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` do agendamento que deseja excluir. |

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

Após a leitura deste guia, você tem uma melhor compreensão de como as programações funcionam.
