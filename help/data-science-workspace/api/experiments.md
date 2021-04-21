---
keywords: Experience Platform, guia do desenvolvedor, endpoint, Data Science Workspace, tópicos populares, experimentos, api de aprendizado de máquina do sensei
solution: Experience Platform
title: Ponto de extremidade da API de experimentos
topic-legacy: Developer guide
description: O desenvolvimento e o treinamento do modelo ocorrem no nível do Experimento, onde um Experimento consiste em uma Instância MLI, execuções de treinamento e execuções de pontuação.
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# Ponto de extremidade de experimentos

O desenvolvimento e o treinamento do modelo ocorrem no nível do Experimento, onde um Experimento consiste em uma Instância MLI, execuções de treinamento e execuções de pontuação.

## Criar um experimento {#create-an-experiment}

Você pode criar um Experimento executando uma solicitação de POST, fornecendo um nome e uma ID de instância MLI válida no payload da solicitação.

>[!NOTE]
>
>Ao contrário do treinamento de modelo na interface do usuário, criar um Experimento por meio de uma chamada explícita de API não cria e executa automaticamente uma execução de treinamento.

**Formato da API**

```http
POST /experiments
```

**Solicitação**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o Experimento. A execução de treinamento correspondente a este Experimento herdará esse valor a ser exibido na interface do usuário como o nome da execução de treinamento. |
| `mlInstanceId` | Uma ID de Instância MLI válida. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Experimento recém-criado, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Criar e executar um treinamento ou uma execução de pontuação {#experiment-training-scoring}

Você pode criar execuções de treinamento ou pontuação executando uma solicitação de POST e fornecendo uma ID de Experimento válida e especificando a tarefa de execução. As execuções de pontuação podem ser criadas somente se o Experimento tiver uma execução de treinamento existente e bem-sucedida. A criação bem-sucedida de uma execução de treinamento inicializará o procedimento de treinamento modelo e sua conclusão bem-sucedida gerará um modelo treinado. A geração de modelos treinados substituirá os já existentes, de modo que um Experimento só possa utilizar um modelo treinado único em um determinado momento.

**Formato da API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de Experimento válida. |

**Solicitação**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `{TASK}` | Especifica a tarefa da execução. Defina esse valor como `train` para treinamento, `score` para pontuação ou `featurePipeline` para pipeline de recursos. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes da execução recém-criada, incluindo o treinamento padrão herdado ou os parâmetros de pontuação, e a ID exclusiva da execução (`{RUN_ID}`).

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Recuperar uma lista de experimentos

Você pode recuperar uma lista de Experimentos pertencentes a uma instância MLI específica executando uma única solicitação de GET e fornecendo uma ID de instância MLI válida como um parâmetro de consulta. Para obter uma lista de queries disponíveis, consulte a seção Apêndice em [parâmetros de consulta para recuperação de ativos](./appendix.md#query).


**Formato da API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLINSTANCE_ID}` | Forneça uma ID de instância MLI válida para recuperar uma lista de Experimentos pertencentes a essa instância MLI específica. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de Experimentos compartilhando a mesma ID de instância MLI (`{MLINSTANCE_ID}`).

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## Recuperar um experimento específico {#retrieve-specific}

Você pode recuperar os detalhes de um Experimento específico executando uma solicitação do GET que inclui a ID do Experimento desejada no caminho da solicitação.

**Formato da API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de Experimento válida. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Experimento solicitado.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Recuperar uma lista de execuções de Experimento

Você pode recuperar uma lista de execuções de treinamento ou pontuação pertencentes a um Experimento específico executando uma única solicitação de GET e fornecendo uma ID de Experimento válida. Para ajudar a filtrar resultados, você pode especificar parâmetros de consulta no caminho da solicitação. Para obter uma lista completa dos parâmetros de consulta disponíveis, consulte a seção Apêndice em [parâmetros de consulta para recuperação de ativos](./appendix.md#query).

>[!NOTE]
>
>Ao combinar vários parâmetros de consulta, eles devem ser separados por &quot;E&quot; comercial (&amp;).

**Formato da API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de Experimento válida. |
| `{QUERY_PARAMETER}` | Um dos [parâmetros de consulta disponíveis](./appendix.md#query) usados para filtrar resultados. |
| `{VALUE}` | O valor do parâmetro de consulta anterior. |

**Solicitação**

A solicitação a seguir contém um query e recupera uma lista de execuções de treinamento pertencentes a algum Experimento.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo uma lista de execuções e cada um de seus detalhes, incluindo a ID de execução de Experimento (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Atualizar um experimento

Você pode atualizar um Experimento existente, sobrescrevendo suas propriedades por meio de uma solicitação de PUT que inclua a ID do Experimento de destino no caminho da solicitação e fornecendo uma carga JSON contendo propriedades atualizadas.

>[!TIP]
>
>Para garantir o sucesso dessa solicitação do PUT, sugerimos que primeiro você execute uma solicitação do GET para [recuperar o Experimento por ID](#retrieve-specific). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como a carga para a solicitação PUT.

O exemplo de chamada de API a seguir atualiza o nome de um Experimento ao ter essas propriedades inicialmente:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**Formato da API**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de Experimento válida. |

**Solicitação**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes atualizados do Experimento.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Excluir um experimento

Você pode excluir um único Experimento executando uma solicitação de DELETE que inclui a ID do Experimento de destino no caminho da solicitação.

**Formato da API**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de Experimento válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
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
    "detail": "Experiment successfully deleted"
}
```

## Excluir experimentos pela ID de instância da MLI

Você pode excluir todos os Experimentos pertencentes a uma instância MLI específica executando uma solicitação DELETE que inclui a ID da instância MLI como um parâmetro de consulta.

**Formato da API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | ---|
| `{MLINSTANCE_ID}` | Uma ID de Instância MLI válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "Experiments successfully deleted"
}
```
