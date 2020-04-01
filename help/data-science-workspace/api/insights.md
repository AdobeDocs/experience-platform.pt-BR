---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Insights
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Insights

Os insights contêm métricas que são usadas para permitir que um cientista de dados avalie e escolha modelos ML ideais exibindo métricas de avaliação relevantes.

## Recuperar uma lista de insights

Você pode recuperar uma lista de Insights executando uma única solicitação GET ao endpoint de insights.  Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

**Formato da API**

```http
GET /insights
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga que inclui uma lista de insights e cada insight tem um identificador exclusivo ( `id` ). Além disso, você receberá `context` os identificadores exclusivos associados a esse insight específico, seguindo os dados de eventos e métricas do Insights.

```json
{
    "children": [
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID correspondente ao Insight. |
| `experimentId` | Uma ID de Experimento válida. |
| `experimentRunId` | Uma ID de execução de experimento válida. |
| `modelId` | Uma ID de modelo válida. |

## Recuperar um insight específico

Para procurar um insight específico, faça uma solicitação GET e forneça um valor válido `{INSIGHT_ID}` no caminho da solicitação. Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

**Formato da API**

```http
GET /insights/{INSIGHT_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{INSIGHT_ID}` | O identificador exclusivo de um insight do Sensei. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/{INSIGHT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga que inclui o identificador único (`id`) do insights. Além disso, você receberá `context` os identificadores exclusivos que estão associados ao insight específico após os dados de eventos e métricas do Insights.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID correspondente ao Insight. |
| `experimentId` | Uma ID de Experimento válida. |
| `experimentRunId` | Uma ID de execução de experimento válida. |
| `modelId` | Uma ID de modelo válida. |

## Adicionar um novo insight de Modelo

Você pode criar um novo insight do Modelo executando uma solicitação POST e uma carga que fornece contexto, eventos e métricas para o novo insight do Modelo. O campo de contexto usado para criar um novo insight do Modelo não é necessário para ter serviços existentes anexados a ele, mas você pode optar por criar o novo insight do Modelo com serviços existentes fornecendo uma ou mais IDs correspondentes:

```json
"context": {
    "clientId": "{CLIENT_ID}",
    "notebookId": "{NOTEBOOK_ID}",
    "experimentId": "{EXPERIMENT_ID}",
    "engineId": "{ENGINE_ID}",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "modelId": "{MODEL_ID}",
    "dataSetId": "{DATASET_ID}"
  }
```

**Formato da API**

```http
POST /insights
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**Resposta**

Uma resposta bem-sucedida retornará uma carga que tem um `{INSIGHT_ID}` e quaisquer parâmetros que você forneceu na solicitação inicial.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Propriedade | Descrição |
| --- | --- |
| `insightId` | A ID exclusiva criada para esse insight específico quando uma solicitação POST bem-sucedida é feita. |

## Recuperar uma lista de métricas padrão para algoritmos

Você pode recuperar uma lista de todas as métricas padrão e do algoritmo executando uma única solicitação GET para o terminal de métricas. Para query de uma métrica específica faça uma solicitação GET e forneça uma solicitação válida `{ALGORITHM}` no caminho da solicitação.

**Formato da API**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ALGORITHM}` | O identificador do tipo de algoritmo. |

**Solicitação**

A solicitação a seguir contém um query e recupera uma métrica específica usando o identificador de algoritmo `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga que inclui o identificador `algorithm` exclusivo e uma matriz de métricas padrão.

```json
{
    "children": [
        {
            "algorithm": "{ALGORITHM}",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```
