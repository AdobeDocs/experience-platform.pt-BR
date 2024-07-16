---
keywords: Experience Platform;guia do desenvolvedor;endpoint;Data Science Workspace;tópicos populares;mlservices;api de aprendizado de máquina do sensei
solution: Experience Platform
title: Endpoint da API de MLServices
description: Um MLService é um modelo treinado publicado que fornece à sua organização a capacidade de acessar e reutilizar modelos desenvolvidos anteriormente. Um recurso importante dos MLServices é a capacidade de automatizar o treinamento e a pontuação de maneira programada. As execuções de treinamento programadas podem ajudar a manter a eficiência e a precisão de um modelo, enquanto as execuções de pontuação programadas podem garantir que novos insights sejam gerados de forma consistente.
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 2%

---

# Ponto de extremidade MLServices

Um MLService é um modelo treinado publicado que fornece à sua organização a capacidade de acessar e reutilizar modelos desenvolvidos anteriormente. Um recurso importante dos MLServices é a capacidade de automatizar o treinamento e a pontuação de maneira programada. As execuções de treinamento programadas podem ajudar a manter a eficiência e a precisão de um modelo, enquanto as execuções de pontuação programadas podem garantir que novos insights sejam gerados de forma consistente.

Os cronogramas automatizados de treinamento e pontuação são definidos com um carimbo de data e hora inicial, carimbo de data e hora final e uma frequência representada como uma [expressão cron](https://en.wikipedia.org/wiki/Cron). As agendas podem ser definidas ao [criar um MLService](#create-an-mlservice) ou aplicadas por [atualizar um MLService existente](#update-an-mlservice).

## Criar um MLService {#create-an-mlservice}

Você pode criar um MLService executando uma solicitação POST e uma carga que forneça um nome para o serviço e uma ID de MLInstance válida. A MLInstance usada para criar um MLService não é necessária para ter Experimentos de treinamento existentes, mas você pode optar por criar o MLService com um modelo treinado existente fornecendo a ID do experimento correspondente e a ID da execução de treinamento.

**Formato da API**

```http
POST /mlServices
```

**Solicitação**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o MLService. O serviço correspondente a este MLService herdará este valor para ser exibido na interface da Galeria de Serviços como o nome do serviço. |
| `description` | Uma descrição opcional para o MLService. O serviço correspondente a este MLService herdará este valor para ser exibido na interface da Galeria de Serviços como a descrição do serviço. |
| `mlInstanceId` | Uma ID de MLInstance válida. |
| `trainingDataSetId` | Uma ID do conjunto de dados de treinamento que, se fornecida, substituirá a ID do conjunto de dados padrão da MLInstance. Se a MLInstance usada para criar o MLService não definir um conjunto de dados de treinamento, você deverá fornecer uma ID de conjunto de dados de treinamento apropriada. |
| `trainingExperimentId` | Uma ID de experimento que você pode fornecer opcionalmente. Se esse valor não for fornecido, a criação do MLService também criará um novo Experimento usando as configurações padrão da MLInstance. |
| `trainingExperimentRunId` | Uma ID de execução de treinamento que você pode fornecer opcionalmente. Se esse valor não for fornecido, a criação do MLService também criará e executará uma execução de treinamento usando os parâmetros de treinamento default da MLInstance. |
| `trainingSchedule` | Uma programação para execuções de treinamento automatizado. Se essa propriedade for definida, o MLService executará automaticamente execuções de treinamento programadas. |
| `trainingSchedule.startTime` | Uma marca de data e hora para a qual as execuções de treinamento programadas serão iniciadas. |
| `trainingSchedule.endTime` | Um carimbo de data e hora para o qual as execuções de treinamento programadas terminarão. |
| `trainingSchedule.cron` | Uma expressão CRON que define a frequência das execuções automatizadas de treinamento. |
| `scoringSchedule` | Uma programação para execuções de pontuação automatizadas. Se essa propriedade for definida, o MLService executará automaticamente as execuções de pontuação de forma programada. |
| `scoringSchedule.startTime` | Um carimbo de data e hora para o qual as execuções de pontuação programadas serão iniciadas. |
| `scoringSchedule.endTime` | Um carimbo de data e hora para o qual as execuções de pontuação programadas terminarão. |
| `scoringSchedule.cron` | Uma expressão CRON que define a frequência das execuções de pontuação automatizada. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do MLService recém-criado, incluindo seu identificador exclusivo (`id`), ID de Experimento para treinamento (`trainingExperimentId`), ID de Experimento para pontuação (`scoringExperimentId`) e ID do conjunto de dados de treinamento de entrada (`trainingDataSetId`).

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Recuperar uma lista de MLServices {#retrieve-a-list-of-mlservices}

Você pode recuperar uma lista de MLServices executando uma única solicitação GET. Para ajudar a filtrar os resultados, você pode especificar parâmetros de consulta no caminho da solicitação. Para obter uma lista de consultas disponíveis, consulte a seção do apêndice sobre [parâmetros de consulta para recuperação de ativos](./appendix.md#query).

**Formato da API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMETER}` | Um dos [parâmetros de consulta disponíveis](./appendix.md#query) usados para filtrar resultados. |
| `{VALUE}` | O valor do parâmetro de consulta anterior. |

**Solicitação**

A solicitação a seguir contém uma consulta e recupera uma lista de MLServices que compartilham a mesma ID de MLInstance (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de MLServices e seus detalhes, incluindo a ID de MLService (`{MLSERVICE_ID}`), a ID de Experimento para treinamento (`{TRAINING_ID}`), a ID de Experimento para pontuação (`{SCORING_ID}`) e a ID de conjunto de dados de treinamento de entrada (`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## Recuperar um MLService específico {#retrieve-a-specific-mlservice}

Você pode recuperar os detalhes de um Experimento específico executando uma solicitação GET que inclui a ID do MLService desejada no caminho da solicitação.

**Formato da API**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: uma ID de MLService válida.

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do MLService solicitado.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Atualizar um MLService {#update-an-mlservice}

Você pode atualizar um MLService existente substituindo suas propriedades por meio de uma solicitação PUT que inclui a ID do MLService de destino no caminho da solicitação e fornecendo uma carga JSON contendo propriedades atualizadas.

>[!TIP]
>
>Para garantir o sucesso dessa solicitação PUT, sugere-se que primeiro você execute uma solicitação GET para [recuperar o MLService pela ID](#retrieve-a-specific-mlservice). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como a carga da solicitação PUT.

**Formato da API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: uma ID de MLService válida.

**Solicitação**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes atualizados do MLService.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## Excluir um MLService

Você pode excluir um único MLService executando uma solicitação DELETE que inclui a ID do MLService de destino no caminho da solicitação.

**Formato da API**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLSERVICE_ID}` | Uma ID de MLService válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLService deletion was successful"
}
```

## Excluir MLServices por ID de MLInstance

Você pode excluir todos os MLServices pertencentes a uma MLInstance específica executando uma solicitação DELETE que especifica uma ID de MLInstance como parâmetro de consulta.

**Formato da API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLINSTANCE_ID}` | Uma ID de MLInstance válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLServices deletion was successful"
}
```
