---
keywords: Experience Platform; guia do desenvolvedor; Extremidade; Área de trabalho de ciência de dados; tópicos populares; Experiências; api sensei de aprendizado de máquina
solution: Experience Platform
title: Terminal da API de experimentos
description: O desenvolvimento e o treinamento do modelo ocorrem no nível Experimento, onde um Experimento consiste em uma MLInstance, treinamento corridas e pontuação de corridas.
role: Developer
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 4%

---

# Terminal de experimentos

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

O desenvolvimento e o treinamento do modelo ocorrem no nível Experimento, onde um Experimento consiste em uma MLInstance, treinamento corridas e pontuação de corridas.

## Criar um Experimento {#create-an-experiment}

É possível criar um Experimento executando uma solicitação POST ao fornecer um nome e uma ID de MLInstance válida na carga solicitação.

>[!NOTE]
>
>Ao contrário do modelo treinamento no interface, criar uma Experimento por meio de uma chamada de API explícita não cria e executa automaticamente uma execução treinamento.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o experimento. A execução de treinamento correspondente a este Experimento herdará esse valor para ser exibido na interface do usuário como o nome da execução de treinamento. |
| `mlInstanceId` | Uma ID de MLInstance válida. |

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

Você pode criar execuções de treinamento ou de pontuação executando uma solicitação POST, fornecendo uma ID de experimento válida e especificando a tarefa de execução. As execuções de pontuação só poderão ser criadas se o Experimento tiver uma execução de treinamento existente e bem-sucedida. A criação bem-sucedida de uma execução de treinamento inicializará o procedimento de treinamento do modelo e sua conclusão bem-sucedida gerará um modelo treinado. A geração de modelos treinados substituirá quaisquer modelos existentes anteriormente, de modo que um Experimento possa utilizar apenas um único modelo treinado a qualquer momento.

**Formato de API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de experimento válida. |

**Solicitação**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `{TASK}` | Especifica o tarefa da execução. Defina esse valor como `train` para treinamento, `score` para pontuação ou `featurePipeline` para pipeline de recursos. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes da execução recém-criada, incluindo o padrão herdado treinamento ou parâmetros de pontuação, e a ID exclusiva (`{RUN_ID}`da execução).

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

Você pode recuperar uma lista de Experimentos pertencentes a uma MLInstance específica executando uma única solicitação de GET e fornecendo uma ID de MLInstance válida como parâmetro de consulta. Para obter uma lista de consultas disponíveis, consulte a seção do apêndice sobre [parâmetros de consulta para recuperação de ativos](./appendix.md#query).


**Formato da API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLINSTANCE_ID}` | Forneça uma ID de MLInstance válida para recuperar uma lista de Experimentos que pertencem a essa MLInstance específica. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de Experimentos que compartilham a mesma ID de MLInstance (`{MLINSTANCE_ID}`).

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

Você pode recuperar os detalhes de uma Experimento específica executando uma solicitação GET que inclui a ID da Experimento desejada no caminho solicitação.

**Formato da API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de experimento válida. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do experimento solicitado.

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

## Recuperar uma lista de execuções de experimento

Você pode recuperar uma lista de treinamentos ou execuções de pontuação pertencentes a um Experimento específico executando uma única solicitação de GET e fornecendo uma ID de experimento válida. Para ajudar a filtrar os resultados, você pode especificar parâmetros de consulta no caminho da solicitação. Para obter uma lista completa dos parâmetros de consulta disponíveis, consulte a seção do apêndice sobre [parâmetros de consulta para recuperação de ativos](./appendix.md#query).

>[!NOTE]
>
>Ao combinar vários parâmetros de consulta, eles devem ser separados pelo sinal gráfico (&amp;).

**Formato da API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de experimento válida. |
| `{QUERY_PARAMETER}` | Um dos [parâmetros de consulta disponíveis](./appendix.md#query) usados para filtrar resultados. |
| `{VALUE}` | O valor do parâmetro de query anterior. |

**Solicitação**

A solicitação a seguir contém um query e recupera uma lista de treinamento correções pertencentes a algumas Experimento.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo uma lista de execuções e cada um de seus detalhes, incluindo a ID de execução de experimento (`{RUN_ID}`).

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

## Atualizar um Experimento

Você pode atualizar uma Experimento existente sobrescrevendo suas propriedades por meio de uma solicitação PUT que inclui a ID do Direcionamento Experimento no caminho solicitação e fornecendo uma carga JSON contendo propriedades atualizadas.

>[!TIP]
>
>Em solicitar para garantir o sucesso desta solicitação PUT, sugere-se que primeiro você execute um solicitação GET para [recuperar o Experimento por ID](#retrieve-specific). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como a carga para o solicitação PUT.

A chamada de API de amostra a seguir atualiza o nome de um Experimentos, enquanto estas propriedades são inicialmente:

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

**Formato de API**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de experimento válida. |

**Solicitação**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Uma resposta bem-sucedida retorna uma carga contendo os detalhes atualizados do experimento.

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

Você pode excluir um único experimento executando uma solicitação DELETE que inclui a ID do experimento de destino no caminho da solicitação.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Excluir experimentos por ID de MLInstance

Você pode excluir todos os experimentos pertencentes a uma MLInstance específica executando uma solicitação DELETE que inclui a ID da MLInstance como parâmetro de consulta.

**Formato da API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | ---|
| `{MLINSTANCE_ID}` | Uma ID MLInstance válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "Experiments successfully deleted"
}
```
