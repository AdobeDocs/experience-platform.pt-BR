---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modelos
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 4%

---


# Modelos

Um modelo é uma instância de uma fórmula de aprendizado de máquina treinada usando dados históricos e configurações para solucionar um caso de uso comercial.

## Recuperar uma lista de modelos

É possível recuperar uma lista de detalhes do Modelo pertencentes a todos os Modelos, executando uma única solicitação de GET para /models. Por padrão, essa lista solicitará a si mesma o modelo criado mais antigo e limitará os resultados a 25. Você pode optar por filtrar os resultados especificando alguns parâmetros de query. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

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
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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

É possível recuperar uma lista de detalhes do Modelo pertencentes a um modelo específico, executando uma única solicitação de GET e fornecendo uma ID de modelo válida no caminho da solicitação. Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

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
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
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
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
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

## Registrar um modelo pré-gerado {#register-a-model}

Você pode registrar um Modelo pré-gerado fazendo uma solicitação POST para o `/models` endpoint. Para registrar seu Modelo, os valores de `modelArtifact` arquivo e `model` propriedade precisam ser incluídos no corpo da solicitação.

**Formato da API**

```http
POST /models
```

**Solicitação**

O POST a seguir contém os valores de `modelArtifact` arquivo e `model` propriedade necessários. Consulte a tabela abaixo para obter mais informações sobre esses valores.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| Parâmetro | Descrição |
| --- | --- |
| `modelArtifact` | A localização do artefato Modelo completo que você deseja incluir. |
| `model` | Os dados de formulário do objeto Model que precisam ser criados. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes de seu Modelo, incluindo o identificador exclusivo de Modelos (`id`).

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID correspondente ao Modelo. |
| `modelArtifactUri` | Um URI que indica onde o modelo está armazenado. O URI termina com o `id` valor do seu modelo. |

## Atualizar um modelo por ID

Você pode atualizar um Modelo existente sobrescrevendo suas propriedades por meio de uma solicitação de PUT que inclua a ID do Modelo de público alvo no caminho da solicitação e fornecendo uma carga JSON contendo propriedades atualizadas.

>[!TIP]
>
>Para garantir o sucesso dessa solicitação de PUT, recomenda-se que primeiro você execute uma solicitação de GET para recuperar o Modelo por ID. Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como carga para a solicitação de PUT.

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
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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

É possível excluir um único Modelo executando uma solicitação de DELETE que inclui a ID do Modelo de público alvo no caminho da solicitação.

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
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
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

## Criar uma nova transcodificação para um modelo {#create-transcoded-model}

A transcodificação é a conversão digital-para-digital direta de uma codificação para outra. Você cria uma nova transcodificação para um Modelo fornecendo o `{MODEL_ID}` e uma `targetFormat` saída na qual deseja que a nova saída esteja.

**Formato da API**

```http
POST /models/{MODEL_ID}/transcodings
```

| Parâmetro | Descrição |
| --- | --- |
| `{MODEL_ID}` | O identificador do Modelo treinado ou publicado. |

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um objeto JSON com as informações de sua transcodificação. Isso inclui o identificador exclusivo de transcodificação (`id`) usado na [recuperação de um Modelo](#retrieve-transcoded-model)transcodificado específico.

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## Recuperar uma lista de transcodificações para um modelo {#retrieve-transcoded-model-list}

Você pode recuperar uma lista de transcodificações que foram executadas em um Modelo executando uma solicitação de GET com seu `{MODEL_ID}`.

**Formato da API**

```http
GET /models/{MODEL_ID}/transcodings
```

| Parâmetro | Descrição |
| --- | --- |
| `{MODEL_ID}` | O identificador do Modelo treinado ou publicado. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um objeto json com uma lista de cada transcodificação executada no Modelo. Cada Modelo transcodificado recebe um identificador exclusivo (`id`).

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## Recuperar um modelo transcodificado específico {#retrieve-transcoded-model}

Você pode recuperar um Modelo transcodificado específico executando uma solicitação de GET com sua ID `{MODEL_ID}` e a ID de um modelo transcodificado.

**Formato da API**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{MODEL_ID}` | O identificador exclusivo de um Modelo treinado ou publicado. |
| `{TRANSCODING_ID}` | O identificador exclusivo de um Modelo transcodificado. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um objeto JSON com os dados do Modelo transcodificado.

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```


