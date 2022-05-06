---
keywords: Experience Platform, guia do desenvolvedor, endpoint, Data Science Workspace, tópicos populares, circunstâncias, api de aprendizado de máquina do sensei
solution: Experience Platform
title: Ponto de Extremidade da API MLInpositions
topic-legacy: Developer guide
description: Uma MLInposition é um emparelhamento de um Mecanismo existente com um conjunto apropriado de configurações que define quaisquer parâmetros de treinamento, parâmetros de pontuação ou configurações de recursos de hardware.
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 4%

---

# Ponto de extremidade MLInances

Uma instância MLI é um emparelhamento de um [Mecanismo](./engines.md) com um conjunto apropriado de configurações que define quaisquer parâmetros de treinamento, parâmetros de pontuação ou configurações de recursos de hardware.

## Criar uma instância MLI {#create-an-mlinstance}

Você pode criar uma instância MLI executando uma solicitação POST enquanto fornece uma carga de solicitação que consiste em uma ID de mecanismo válida (`{ENGINE_ID}`) e um conjunto apropriado de configurações padrão.

Se a ID do mecanismo fizer referência a um PySpark ou Spark Engine, você terá a capacidade de configurar a quantidade de recursos de computação, como o número de núcleos ou a quantidade de memória. Se um Mecanismo Python for referenciado, você poderá optar entre usar uma CPU ou GPU para fins de treinamento e pontuação. Consulte as seções do apêndice em [Configurações de recursos PySpark e Spark](./appendix.md#resource-config) e [Configurações de CPU Python e GPU](./appendix.md#cpu-gpu-config) para obter mais informações.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | O nome desejado para a instância MLI. O Modelo correspondente a esta instância MLI herdará este valor a ser exibido na interface do usuário como o nome do Modelo. |
| `description` | Uma descrição opcional para a instância MLI. O Modelo correspondente a esta instância MLI herdará este valor a ser exibido na interface do usuário como a descrição do Modelo. Esta propriedade é obrigatória. Se não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `engineId` | A ID de um mecanismo existente. |
| `tasks` | Um conjunto de configurações para treinamento, pontuação ou pipelines de recursos. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes da MLIntent recém-criada, incluindo seu identificador exclusivo (`id`).

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

## Recuperar uma lista de MLInpositions

Você pode recuperar uma lista de MLInpositions executando uma única solicitação do GET. Para ajudar a filtrar resultados, você pode especificar parâmetros de consulta no caminho da solicitação. Para obter uma lista de queries disponíveis, consulte a seção Apêndice em [parâmetros de consulta para recuperação de ativos](./appendix.md#query).

**Formato da API**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMETER}` | Um dos [parâmetros de consulta disponíveis](./appendix.md#query) usado para filtrar resultados. |
| `{VALUE}` | O valor do parâmetro de consulta anterior. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de MLInpositions e seus detalhes.

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

Você pode recuperar os detalhes de uma instância MLI específica executando uma solicitação do GET que inclui a ID da instância MLI desejada no caminho da solicitação.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Você pode atualizar uma instância MLI existente, sobrescrevendo suas propriedades por meio de uma solicitação PUT que inclua a ID da instância MLI de destino no caminho da solicitação e fornecendo uma carga JSON contendo propriedades atualizadas.

>[!TIP]
>
>Para garantir o sucesso dessa solicitação do PUT, sugerimos que primeiro você execute uma solicitação do GET para [recuperar a MLIntent por ID](#retrieve-specific). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como a carga para a solicitação PUT.

O exemplo de chamada de API a seguir atualizará os parâmetros de treinamento e pontuação de uma instância do MLI com essas propriedades inicialmente:

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
| `{MLINSTANCE_ID}` | Uma ID de Instância MLI válida. |

**Solicitação**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Uma resposta bem-sucedida retorna uma carga contendo os detalhes atualizados da instância MLI.

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

É possível excluir todas as MLInpositions que compartilham o mesmo mecanismo executando uma solicitação de DELETE que inclui a ID do mecanismo como um parâmetro de consulta.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Você pode excluir uma única instância MLI executando uma solicitação DELETE que inclui a ID da instância MLI do destino no caminho da solicitação.

**Formato da API**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MLINSTANCE_ID}` | Uma ID de Instância MLI válida. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLInstance deletion was successful"
}
```
