---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;mlinstances;sensei machine learning api
solution: Experience Platform
title: MLInentons
topic: Developer guide
description: Uma instância MLI é um emparelhamento de um Mecanismo existente com um conjunto apropriado de configurações que define quaisquer parâmetros de treinamento, parâmetros de pontuação ou configurações de recursos de hardware.
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 4%

---


# MLInentons

Uma instância MLI é um emparelhamento de um [Mecanismo](./engines.md) existente com um conjunto apropriado de configurações que define quaisquer parâmetros de treinamento, parâmetros de pontuação ou configurações de recursos de hardware.

## Criar uma instância MLI {#create-an-mlinstance}

Você pode criar uma instância MLI executando uma solicitação de POST ao fornecer uma carga de solicitação que consiste em uma ID de mecanismo (`{ENGINE_ID}`) válida e um conjunto apropriado de configurações padrão.

Se a ID do mecanismo fizer referência a um PySpark ou Spark Engine, você terá a capacidade de configurar a quantidade de recursos de computação, como o número de núcleos ou a quantidade de memória. Se um Mecanismo Python for referenciado, você poderá escolher entre usar uma CPU ou uma GPU para fins de treinamento e pontuação. Consulte as seções do apêndice nas configurações [de recursos](./appendix.md#resource-config) PySpark e Spark e nas configurações [de CPU e GPU](./appendix.md#cpu-gpu-config) Python para obter mais informações.

**Formato da API**

```http
POST /mlInstances
```

**Solicitação**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para a instância MLI. O Modelo que corresponde a essa instância MLI herdará esse valor para ser exibido na interface do usuário como o nome do Modelo. |
| `description` | Uma descrição opcional para a instância MLI. O Modelo que corresponde a essa instância MLI herdará esse valor para ser exibido na interface do usuário como a descrição do Modelo. Esta propriedade é obrigatória. Se você não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `engineId` | A ID de um mecanismo existente. |
| `tasks` | Um conjunto de configurações para treinamento, pontuação ou pipeline de recursos. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes da MLI recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Recuperar uma lista de MLInentons

Você pode recuperar uma lista de MLInentons executando uma única solicitação de GET. Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

**Formato da API**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMETER}` | Um dos parâmetros [de query](./appendix.md#query) disponíveis usados para filtrar os resultados. |
| `{VALUE}` | O valor do parâmetro de query anterior. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de MLInentons e seus detalhes.

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## Recuperar uma instância MLI específica {#retrieve-specific}

Você pode recuperar os detalhes de uma instância MLI específica executando uma solicitação de GET que inclui a ID da instância MLI desejada no caminho da solicitação.

**Formato da API**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLINSTANCE_ID}` | A ID da instância MLI desejada. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da instância MLI.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Atualizar uma instância MLI

Você pode atualizar uma instância MLI existente substituindo suas propriedades por meio de uma solicitação de PUT que inclua a ID da instância MLI do público alvo no caminho da solicitação e fornecendo uma carga JSON contendo propriedades atualizadas.

>[!TIP]
>
>Para garantir o sucesso desta solicitação de PUT, recomenda-se que você execute primeiro uma solicitação de GET para [recuperar a instância MLI por ID](#retrieve-specific). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como carga para a solicitação de PUT.

A chamada de API de exemplo a seguir atualizará os parâmetros de treinamento e pontuação de uma MLInpresence ao ter essas propriedades inicialmente:

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**Formato da API**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLINSTANCE_ID}` | Uma ID de instância MLI válida. |

**Solicitação**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes atualizados da MLInpresence.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## Excluir MLInentons por ID do mecanismo

É possível excluir todas as MLInentons que compartilham o mesmo Mecanismo, executando uma solicitação de DELETE que inclui a ID do mecanismo como um parâmetro de query.

**Formato da API**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENGINE_ID}` | Uma ID de mecanismo válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
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
    "detail": "MLInstances successfully deleted"
}
```

## Excluir uma instância MLI

É possível excluir uma única instância MLI executando uma solicitação de DELETE que inclua a ID da instância MLI do público alvo no caminho da solicitação.

**Formato da API**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLINSTANCE_ID}` | Uma ID de instância MLI válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLInstance deletion was successful"
}
```
