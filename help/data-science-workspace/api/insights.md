---
keywords: Experience Platform, guia do desenvolvedor, endpoint, Data Science Workspace, tópicos populares, insights, api de aprendizado de máquina do sensei
solution: Experience Platform
title: Endpoint da API do Insights
topic-legacy: Developer guide
description: Os insights contêm métricas que são usadas para capacitar um cientista de dados a avaliar e escolher modelos de ML ideais ao exibir métricas de avaliação relevantes.
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# Ponto de extremidade de insights

Os insights contêm métricas que são usadas para capacitar um cientista de dados a avaliar e escolher modelos de ML ideais ao exibir métricas de avaliação relevantes.

## Recuperar uma lista de insights

Você pode recuperar uma lista de Insights executando uma única solicitação de GET para o endpoint de insights.  Para ajudar a filtrar resultados, você pode especificar parâmetros de consulta no caminho da solicitação. Para obter uma lista de queries disponíveis, consulte a seção Apêndice em [parâmetros de consulta para recuperação de ativos](./appendix.md#query).

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

Uma resposta bem-sucedida retorna uma carga que inclui uma lista de insights e cada insight tem um identificador exclusivo ( `id` ). Além disso, você receberá `context` que contém os identificadores exclusivos associados a esse insight específico, seguindo os eventos de Insights e os dados de métricas.

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `experimentRunId` | Uma ID de Execução de Experimento válida. |
| `modelId` | Uma ID de modelo válida. |

## Recuperar um Insight específico

Para procurar um insight específico faça uma solicitação do GET e forneça um `{INSIGHT_ID}` válido no caminho da solicitação. Para ajudar a filtrar resultados, você pode especificar parâmetros de consulta no caminho da solicitação. Para obter uma lista de queries disponíveis, consulte a seção Apêndice em [parâmetros de consulta para recuperação de ativos](./appendix.md#query).

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
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga que inclui o identificador exclusivo de insights (`id`). Além disso, você receberá `context` que contém os identificadores exclusivos que estão associados ao insight específico após os eventos de Insights e os dados de métricas.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `experimentRunId` | Uma ID de Execução de Experimento válida. |
| `modelId` | Uma ID de modelo válida. |

## Adicionar um novo insight de modelo

Você pode criar um novo Modelo de insight executando uma solicitação de POST e uma carga que fornece contexto, eventos e métricas para o novo Modelo de insight. O campo de contexto usado para criar um novo Model insight não é necessário para que os serviços existentes sejam anexados a ele, mas você pode optar por criar o novo Model insight com os serviços existentes fornecendo uma ou mais das IDs correspondentes:

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
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
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

Uma resposta bem-sucedida retornará uma carga que tem `{INSIGHT_ID}` e quaisquer parâmetros fornecidos na solicitação inicial.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `insightId` | A ID exclusiva que é criada para esse insight específico quando uma solicitação POST bem-sucedida é feita. |

## Recuperar uma lista de métricas padrão para algoritmos

Você pode recuperar uma lista de todas as métricas padrão e do algoritmo executando uma única solicitação do GET para o terminal de métricas. Para consultar uma métrica específica, faça uma solicitação GET e forneça um `{ALGORITHM}` válido no caminho da solicitação.

**Formato da API**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ALGORITHM}` | O identificador do tipo de algoritmo. |

**Solicitação**

A solicitação a seguir contém uma consulta e recupera uma métrica específica usando o identificador de algoritmo `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga que inclui o identificador exclusivo `algorithm` e uma matriz de métricas padrão.

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
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
