---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Experimentos
topic: Developer guide
translation-type: tm+mt
source-git-commit: 71e257c85790a96b5017dea314b757ec4ee07bed

---


# Experimentos

O desenvolvimento e o treinamento do modelo ocorrem no nível do Experimento, onde um Experimento consiste em uma instância MLI, execuções de treinamento e execuções de pontuação.

## Criar um experimento

Você pode criar um Experimento executando uma solicitação POST ao fornecer um nome e uma ID de instância MLI válida na carga da solicitação.

>[!NOTE] Ao contrário do treinamento de modelo na interface do usuário, a criação de um Experimento por meio de uma chamada explícita de API não cria e executa automaticamente uma execução de treinamento.

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
        "mlInstanceId": "{MLINSTANCE_ID}"
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o Experimento. A execução de treinamento correspondente a este Experimento herdará esse valor para ser exibido na interface do usuário como o nome da execução de treinamento. |
| `mlInstanceId` | Uma ID de instância MLI válida. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Experimento recém-criado, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Criar e executar um treinamento ou uma execução de pontuação

Você pode criar execuções de treinamento ou pontuação executando uma solicitação POST e fornecendo uma ID de Experimento válida e especificando a tarefa de execução. As execuções de pontuação podem ser criadas somente se o Experimento tiver uma execução de treinamento existente e bem-sucedida. A criação bem-sucedida de uma execução de treinamento inicializará o procedimento de treinamento do modelo e sua conclusão bem-sucedida gerará um modelo treinado. A geração de modelos treinados substituirá os modelos existentes anteriormente, de modo que um Experimento só possa utilizar um único modelo treinado a qualquer momento.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
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
| `{TASK}` | Especifica a tarefa da execução. Defina esse valor como `train` para treinamento, `score` para pontuação ou `fp` para pipeline de recursos. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes da execução recém-criada, incluindo os parâmetros de treinamento ou pontuação padrão herdados e a ID exclusiva (`{RUN_ID}`) da execução.

```json
{
    "id": "{RUN_ID}",
    "mode": "{TASK}",
    "experimentId": "{EXPERIMENT_ID}",
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

## Recuperar uma lista de experiências

Você pode recuperar uma lista de Experimentos pertencentes a uma determinada MLIntent, executando uma única solicitação GET e fornecendo uma ID de instância MLI válida como parâmetro de query. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](appendix.md#query)de ativos.


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
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId=={MLINSTANCE_ID} \
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
            "id": "{EXPERIMENT_ID}",
            "name": "A name for this Experiment",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 1",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 2",
            "mlInstanceId": "{MLINSTANCE_ID}",
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

Você pode recuperar os detalhes de um Experimento específico executando uma solicitação GET que inclui a ID do Experimento desejada no caminho da solicitação.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```


**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Experimento solicitado.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Recuperar uma lista de execuções de Experimento

Você pode recuperar uma lista de execuções de treinamento ou pontuação pertencentes a um Experimento específico, executando uma única solicitação GET e fornecendo uma ID de Experimento válida. Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista completa dos parâmetros de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](appendix.md#query)de ativos.

>[!NOTE] Ao combinar vários parâmetros de query, eles devem ser separados por E comercial (&amp;).

**Formato da API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPERIMENT_ID}` | Uma ID de Experimento válida. |
| `{QUERY_PARAMETER}` | Um dos parâmetros [de query](appendix.md#query) disponíveis usados para filtrar os resultados. |
| `{VALUE}` | O valor do parâmetro de query anterior. |

**Solicitação**

A solicitação a seguir contém um query e recupera uma lista de execuções de treinamento pertencentes a algum Experimento.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo uma lista de execuções e cada um de seus detalhes, incluindo a ID de execução do Experimento (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "{RUN_ID}",
            "mode": "train",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId=={EXPERIMENT_ID},deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Atualizar um experimento

Você pode atualizar um Experimento existente substituindo suas propriedades por meio de uma solicitação PUT que inclui a ID do Experimento do público alvo no caminho da solicitação e fornece uma carga JSON contendo propriedades atualizadas.

>[!TIP] Para garantir o sucesso desta solicitação PUT, recomenda-se que você primeiro execute uma solicitação GET para [recuperar o Experimento por ID](#retrieve-specific). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como carga para a solicitação PUT.

A amostra de chamada de API a seguir atualiza o nome de um Experimento ao ter essas propriedades inicialmente:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "{MLINSTANCE_ID}",
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
    "id": "{EXPERIMENT_ID}",
    "name": "An updated name",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Excluir um experimento

Você pode excluir um único Experimento executando uma solicitação DELETE que inclui a ID do Experimento do público alvo no caminho da solicitação.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
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

## Excluir experiências por ID de instância MLI

Você pode excluir todos os Experimentos que pertencem a uma determinada instância MLI executando uma solicitação DELETE que inclui a ID da instância MLI como um parâmetro de query.

**Formato da API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | ---|
| `{MLINSTANCE_ID}` | Uma ID de instância MLI válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId={MLINSTANCE_ID} \
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
