---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Serviços
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 2%

---


# MLServices

Um MLService é um modelo treinado publicado que fornece à sua organização a capacidade de acessar e reutilizar modelos desenvolvidos anteriormente. Um recurso essencial do MLServices é a capacidade de automatizar o treinamento e a pontuação de acordo com o agendamento. As execuções de treinamento programadas podem ajudar a manter a eficiência e a precisão de um modelo, enquanto as execuções de pontuação programadas podem garantir que novos insights sejam gerados de forma consistente.

As programações de treinamento e pontuação automatizadas são definidas com um carimbo de data e hora inicial, um carimbo de data e hora final e uma frequência representada como uma expressão [](https://en.wikipedia.org/wiki/Cron)cron. As programações podem ser definidas ao [criar um MLService](#create-an-mlservice) ou aplicadas ao [atualizar um MLService](#update-an-mlservice)existente.

## Criar um MLService {#create-an-mlservice}

Você pode criar um MLService executando uma solicitação POST e uma carga que fornece um nome para o serviço e uma ID de instância MLI válida. A instância MLI usada para criar um MLService não é necessária para ter Experimentos de treinamento existentes, mas você pode optar por criar o MLService com um modelo treinado existente fornecendo a ID de experiência e a ID de execução de treinamento correspondentes.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | O nome desejado para o MLService. O serviço correspondente a este MLService herdará esse valor para ser exibido na interface do usuário da Galeria de Serviços como o nome do serviço. |
| `description` | Uma descrição opcional para o MLService. O serviço correspondente a este MLService herdará esse valor para ser exibido na interface do usuário da Service Gallery como a descrição do serviço. |
| `mlInstanceId` | Uma ID de instância MLI válida. |
| `trainingDataSetId` | Uma ID do conjunto de dados de treinamento que, se fornecida, substituirá a ID do conjunto de dados padrão da MLInposition. Se a instância MLI usada para criar o MLService não definir um conjunto de dados de treinamento, você deverá fornecer uma ID de conjunto de dados de treinamento apropriada. |
| `trainingExperimentId` | Uma ID de Experimento que você pode fornecer opcionalmente. Se esse valor não for fornecido, a criação do MLService também criará um novo Experimento usando as configurações padrão da MLInposition. |
| `trainingExperimentRunId` | Uma ID de execução de treinamento que você pode fornecer opcionalmente. Se esse valor não for fornecido, a criação do MLService também criará e executará uma execução de treinamento usando os parâmetros de treinamento padrão da MLInpresence. |
| `trainingSchedule` | Um agendamento para execução de treinamento automatizado. Se essa propriedade for definida, o MLService executará automaticamente execuções de treinamento de acordo com uma programação. |
| `trainingSchedule.startTime` | Um carimbo de data e hora para o qual as execuções de treinamento programado começarão. |
| `trainingSchedule.endTime` | Um carimbo de data e hora para o qual as execuções de treinamento programado terminarão. |
| `trainingSchedule.cron` | Uma expressão cron que define a frequência das execuções de treinamento automatizado. |
| `scoringSchedule` | Um agendamento para execuções de pontuação automatizadas. Se essa propriedade for definida, o MLService executará automaticamente execuções de pontuação de acordo com uma programação. |
| `scoringSchedule.startTime` | Um carimbo de data e hora para o qual as execuções de pontuação programadas começarão. |
| `scoringSchedule.endTime` | Um carimbo de data e hora para o qual as execuções de pontuação programadas terminarão. |
| `scoringSchedule.cron` | Uma expressão cron que define a frequência das execuções de pontuação automatizada. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do MLService recém-criado, incluindo seu identificador exclusivo (`id`), ID de Experimento para treinamento (`trainingExperimentId`), ID de Experimento para pontuação (`scoringExperimentId`) e a ID do conjunto de dados de treinamento de entrada (`trainingDataSetId`).

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

Você pode recuperar uma lista de MLServices executando uma única solicitação GET. Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

**Formato da API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMETER}` | Um dos parâmetros [de query](./appendix.md#query) disponíveis usados para filtrar os resultados. |
| `{VALUE}` | O valor do parâmetro de query anterior. |

**Solicitação**

A solicitação a seguir contém um query e recupera uma lista de MLServices compartilhando a mesma ID de instância MLI (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de MLServices e seus detalhes, incluindo a ID do serviço MLS (`{MLSERVICE_ID}`), a ID do experimento para treinamento (`{TRAINING_ID}`), a ID do experimento para pontuação (`{SCORING_ID}`) e a ID do conjunto de dados de treinamento de entrada (`{DATASET_ID}`).

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

* `{MLSERVICE_ID}`: Uma ID MLService válida.

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Você pode atualizar um MLService existente substituindo suas propriedades por meio de uma solicitação PUT que inclui a ID do público alvo MLService no caminho da solicitação e fornece uma carga JSON contendo propriedades atualizadas.

>[!TIP]
>
>Para garantir o sucesso desta solicitação PUT, recomenda-se que primeiro você execute uma solicitação GET para [recuperar o MLService por ID](#retrieve-a-specific-mlservice). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como carga para a solicitação PUT.

**Formato da API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Uma ID MLService válida.

**Solicitação**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Você pode excluir um único MLService executando uma solicitação DELETE que inclui a ID do público alvo MLService no caminho da solicitação.

**Formato da API**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLSERVICE_ID}` | Uma ID MLService válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Excluir MLServices por ID de instância MLI

Você pode excluir todos os MLServices pertencentes a uma determinada MLInposition executando uma solicitação DELETE que especifica uma ID de instância MLI como parâmetro de query.

**Formato da API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLINSTANCE_ID}` | Uma ID de instância MLI válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
