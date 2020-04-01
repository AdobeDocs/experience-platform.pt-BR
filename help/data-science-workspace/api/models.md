---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modelos
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Modelos

Um modelo é uma instância de uma fórmula de aprendizado de máquina treinada usando dados históricos e configurações para solucionar um caso de uso comercial.

## Recuperar uma lista de modelos

Você pode recuperar uma lista de detalhes do Modelo pertencentes a todos os Modelos, executando uma única solicitação GET para /models. Por padrão, essa lista solicitará a si mesma o modelo criado mais antigo e limitará os resultados a 25. Você pode optar por filtrar os resultados especificando alguns parâmetros de query. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

**Formato da API**

```http
GET /models
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes de seus Modelos, incluindo cada identificador exclusivo (`id`) dos Modelos.

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID correspondente ao Modelo. |
| `modelArtifactUri` | Um URI que indica onde o modelo está armazenado. O URI termina com o `name` valor do modelo. |
| `experimentId` | Uma ID de Experimento válida. |
| `experimentRunId` | Uma ID de execução de experimento válida. |

## Recuperar um modelo específico

É possível recuperar uma lista de detalhes do Modelo pertencentes a um modelo específico, executando uma única solicitação GET e fornecendo uma ID de modelo válida no caminho da solicitação. Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

**Formato da API**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MODEL_ID}` | O identificador do Modelo treinado ou publicado. |
| `{EXPERIMENT_RUN_ID}` | O identificador da execução do experimento. |

**Solicitação**

A solicitação a seguir contém um query e recupera uma lista de Modelos treinados compartilhando a mesma experienceRunID ({EXPERIMENT_RUN_ID}).

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes de seu Modelo, incluindo o identificador exclusivo de Modelos (`id`).

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
        "count": 1
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID correspondente ao Modelo. |
| `modelArtifactUri` | Um URI que indica onde o modelo está armazenado. O URI termina com o `name` valor do modelo. |
| `experimentId` | Uma ID de Experimento válida. |
| `experimentRunId` | Uma ID de execução de experimento válida. |

## Atualizar um modelo por ID

Você pode atualizar um Modelo existente substituindo suas propriedades por meio de uma solicitação PUT que inclui a ID do Modelo de público alvo no caminho da solicitação e fornece uma carga JSON que contém propriedades atualizadas.

>[!TIP] Para garantir o sucesso desta solicitação PUT, recomenda-se que primeiro você execute uma solicitação GET para recuperar o Modelo por ID. Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como carga para a solicitação PUT.

**Formato da API**

```http
PUT /models/{MODEL_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MODEL_ID}` | O identificador do Modelo treinado ou publicado. |

**Solicitação**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes atualizados do Experimento.

```json
{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## Excluir um modelo por ID

Você pode excluir um único Modelo executando uma solicitação DELETE que inclui a ID do Modelo de público alvo no caminho da solicitação.

**Formato da API**

```http
DELETE /models/{MODEL_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MODEL_ID}` | O identificador do Modelo treinado ou publicado. |

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um status 200 confirmando a exclusão do Modelo.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```
