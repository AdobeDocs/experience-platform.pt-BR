---
keywords: Experience Platform, home, tópicos populares, ingestão em lote, ingestão em lote, ingestão, guia do desenvolvedor, guia da api, carregar, assimilar parquet, assimilar json;
solution: Experience Platform
title: Guia da API de assimilação em lote
description: Este documento fornece um guia abrangente para desenvolvedores que trabalham com APIs de assimilação em lote para Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '2373'
ht-degree: 5%

---

# Guia do desenvolvedor de assimilação em lote

Este documento fornece um guia abrangente sobre como usar o [endpoints da API de assimilação em lote](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion) no Adobe Experience Platform. Para obter uma visão geral das APIs de ingestão em lote, incluindo pré-requisitos e práticas recomendadas, comece lendo o [visão geral da API de assimilação de lote](overview.md).

O apêndice deste documento contém informações para [formatação de dados a serem usados para assimilação](#data-transformation-for-batch-ingestion), incluindo arquivos de dados CSV e JSON de amostra.

## Introdução

Os endpoints de API usados neste guia fazem parte do [API de assimilação de dados](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). A assimilação de dados fornece uma RESTful API através da qual você pode executar operações básicas de CRUD em relação aos tipos de objetos suportados.

Antes de continuar, reveja o [visão geral da API de assimilação de lote](overview.md) e [guia de introdução](getting-started.md).

## Assimilar arquivos JSON

>[!NOTE]
>
>As etapas a seguir são aplicáveis a arquivos pequenos (256 MB ou menos). Se você atingir o tempo limite do gateway ou solicitar erros de tamanho do corpo, precisará alternar para o upload de arquivo grande.

### Criar lote

Primeiro, você precisará criar um lote, com JSON como o formato de entrada. Ao criar o lote, é necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido.

>[!NOTE]
>
>Os exemplos abaixo são para JSON de linha única. Para assimilar JSON de várias linhas, a variável `isMultiLineJson` será necessário definir o sinalizador . Para obter mais informações, leia o [guia de solução de problemas de ingestão em lote](./troubleshooting.md).

**Formato da API**

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID do conjunto de dados de referência. |

**Resposta**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote recém-criado. |
| `{DATASET_ID}` | A ID do conjunto de dados referenciado. |

### Upload de arquivos

Agora que você criou um lote, é possível usar a ID do lote da resposta de criação do lote para fazer upload de arquivos para o lote. Você pode fazer upload de vários arquivos para o lote.

>[!NOTE]
>
>Consulte a seção de apêndice para obter uma [exemplo de um arquivo de dados JSON formatado corretamente](#data-transformation-for-batch-ingestion).

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Esse caminho de arquivo é o local onde o arquivo será salvo no lado do Adobe. |

**Solicitação**

>[!NOTE]
>
>A API suporta o upload de parte única. Certifique-se de que o tipo de conteúdo seja application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Esse caminho de arquivo é o caminho de arquivo local, como `Users/sample-user/Downloads/sample.json`. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |

**Solicitação**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```http
200 OK
```

## Assimilar arquivos do Parquet {#ingest-parquet-files}

>[!NOTE]
>
>As etapas a seguir são aplicáveis a arquivos pequenos (256 MB ou menos). Se você atingir o tempo limite do gateway ou solicitar erros de tamanho do corpo, precisará alternar para o upload de arquivo grande.

### Criar lote

Primeiro, você precisará criar um lote, com o Parquet como o formato de entrada. Ao criar o lote, é necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido.

**Solicitação**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| Parâmetro | Descrição |
| --------- | ------------ |
| `{DATASET_ID}` | A ID do conjunto de dados de referência. |

**Resposta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote recém-criado. |
| `{DATASET_ID}` | A ID do conjunto de dados referenciado. |
| `{USER_ID}` | A ID do usuário que criou o lote. |

### Upload de arquivos

Agora que você criou um lote, é possível usar a variável `batchId` de antes para carregar arquivos no lote. Você pode fazer upload de vários arquivos para o lote.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Esse caminho de arquivo é o local onde o arquivo será salvo no lado do Adobe. |

**Solicitação**

>[!CAUTION]
>
>Essa API suporta o upload de parte única. Certifique-se de que o tipo de conteúdo seja application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Esse caminho de arquivo é o caminho de arquivo local, como `Users/sample-user/Downloads/sample.json`. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você deseja sinalizar está pronta para conclusão. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

## Assimilar arquivos grandes do Parquet

>[!NOTE]
>
>Esta seção detalha como fazer upload de arquivos com mais de 256 MB. Os arquivos grandes são carregados em partes e depois compilados por um sinal de API.

### Criar lote

Primeiro, você precisará criar um lote, com o Parquet como o formato de entrada. Ao criar o lote, é necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido.

**Formato da API**

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID do conjunto de dados de referência. |

**Resposta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote recém-criado. |
| `{DATASET_ID}` | A ID do conjunto de dados referenciado. |
| `{USER_ID}` | A ID do usuário que criou o lote. |

### Inicializar arquivo grande

Após criar o lote, será necessário inicializar o arquivo grande antes de fazer upload das partes no lote.

**Formato da API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote recém-criado. |
| `{DATASET_ID}` | A ID do conjunto de dados referenciado. |
| `{FILE_NAME}` | O nome do arquivo que está prestes a ser inicializado. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
201 Created
```

### Fazer upload de partes grandes do arquivo

Agora que o arquivo foi criado, todos os fragmentos subsequentes podem ser carregados fazendo solicitações PATCH repetidas, uma para cada seção do arquivo.

**Formato da API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Esse caminho de arquivo é o local onde o arquivo será salvo no lado do Adobe. |

**Solicitação**

>[!CAUTION]
>
>Essa API suporta o upload de parte única. Certifique-se de que o tipo de conteúdo seja application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONTENT_RANGE}` | Em números inteiros, o início e o fim do intervalo solicitado. |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Esse caminho de arquivo é o caminho de arquivo local, como `Users/sample-user/Downloads/sample.json`. |


**Resposta**

```http
200 OK
```

### Arquivo grande completo

Agora que você criou um lote, é possível usar a variável `batchId` de antes para carregar arquivos no lote. Você pode fazer upload de vários arquivos para o lote.

**Formato da API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote do qual deseja sinalizar a conclusão. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo do qual deseja sinalizar a conclusão. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
201 Created
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote que deseja sinalizar está concluída. |


**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

## Assimilar arquivos CSV

Para assimilar arquivos CSV, é necessário criar uma classe, um esquema e um conjunto de dados compatível com CSV. Para obter informações detalhadas sobre como criar a classe e o schema necessários, siga as instruções fornecidas no [tutorial de criação de schema ad-hoc](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>As etapas a seguir são aplicáveis a arquivos pequenos (256 MB ou menos). Se você atingir o tempo limite do gateway ou solicitar erros de tamanho do corpo, precisará alternar para o upload de arquivo grande.

### Criar conjunto de dados

Após seguir as instruções acima para criar a classe e o schema necessários, será necessário criar um conjunto de dados que possa oferecer suporte a CSV.

**Formato da API**

```http
POST /catalog/dataSets
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TENANT_ID}` | Essa ID é usada para garantir que os recursos criados sejam namespacados corretamente e estejam contidos na Organização IMS. |
| `{SCHEMA_ID}` | A ID do esquema criado. |

### Criar lote

Em seguida, será necessário criar um lote com CSV como o formato de entrada. Ao criar o lote, é necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o schema vinculado ao conjunto de dados fornecido.

**Formato da API**

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID do conjunto de dados de referência. |

**Resposta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote recém-criado. |
| `{DATASET_ID}` | A ID do conjunto de dados referenciado. |
| `{USER_ID}` | A ID do usuário que criou o lote. |

### Upload de arquivos

Agora que você criou um lote, é possível usar a variável `batchId` de antes para carregar arquivos no lote. Você pode fazer upload de vários arquivos para o lote.

>[!NOTE]
>
>Consulte a seção de apêndice para obter uma [exemplo de um arquivo de dados CSV corretamente formatado](#data-transformation-for-batch-ingestion).

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Esse caminho de arquivo é o local onde o arquivo será salvo no lado do Adobe. |

**Solicitação**

>[!CAUTION]
>
>Essa API suporta o upload de parte única. Certifique-se de que o tipo de conteúdo seja application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Esse caminho de arquivo é o caminho de arquivo local, como `Users/sample-user/Downloads/sample.json`. |


**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```http
200 OK
```

## Cancelar um lote

Enquanto o lote está sendo processado, ele ainda pode ser cancelado. No entanto, quando um lote é finalizado (como um estado bem-sucedido ou com falha), o lote não pode ser cancelado.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você deseja cancelar. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

## Excluir um lote {#delete-a-batch}

Um lote pode ser excluído executando a seguinte solicitação de POST com o `action=REVERT` parâmetro de consulta para a ID do lote que você deseja excluir. O lote é o marcado como &quot;inativo&quot;, tornando-o elegível para a coleta de lixo. O lote será coletado de forma assíncrona e, nesse momento, será marcado como &quot;excluído&quot;.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você deseja excluir. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

## Patch um lote

Ocasionalmente, pode ser necessário atualizar os dados na Loja de perfis de sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. O Adobe Experience Platform oferece suporte à atualização ou ao patch dos dados da Loja de perfil por meio de uma ação de atualização ou &quot;correção de um lote&quot;.

>[!NOTE]
>
>Essas atualizações são permitidas somente em registros de perfil, não em eventos de experiência.

Para aplicar um sistema transdérmico num lote é necessário o seguinte:

- **Um conjunto de dados habilitado para atualizações de perfil e atributo.** Isso é feito por meio de tags de conjunto de dados e requer um `isUpsert:true` será adicionada à tag `unifiedProfile` matriz. Para obter detalhes sobre as etapas que mostram como criar um conjunto de dados ou configurar um conjunto de dados existente para atualização, siga o tutorial para [habilitar um conjunto de dados para atualizações de perfil](../../catalog/datasets/enable-upsert.md).
- **Um arquivo Parquet contendo os campos a serem corrigidos e os campos de identidade do Perfil.** O formato de dados para aplicar patches a um lote é semelhante ao processo normal de ingestão em lote. A entrada necessária é um arquivo Parquet e, além dos campos a serem atualizados, os dados carregados devem conter os campos de identidade para corresponderem aos dados na Loja de perfis.

Depois que você tiver um conjunto de dados ativado para Perfil e Upsert e um arquivo Parquet contendo os campos que deseja corrigir, bem como os campos de identidade necessários, você poderá seguir as etapas para [assimilação de arquivos do Parquet](#ingest-parquet-files) para completar o sistema através da ingestão de lote.

## Reproduzir um lote

Se quiser substituir um lote já assimilado, faça isso com &quot;repetição em lote&quot; - essa ação é equivalente a excluir o lote antigo e assimilar um novo.

### Criar lote

Primeiro, você precisará criar um lote, com JSON como o formato de entrada. Ao criar o lote, é necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido. Além disso, você precisará fornecer os lotes antigos como referência na seção de repetição . No exemplo abaixo, você está reproduzindo lotes com IDs `batchIdA` e `batchIdB`.

**Formato da API**

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| Parâmetro | Descrição |
| --------- | ----------- | 
| `{DATASET_ID}` | A ID do conjunto de dados de referência. |

**Resposta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote recém-criado. |
| `{DATASET_ID}` | A ID do conjunto de dados referenciado. |
| `{USER_ID}` | A ID do usuário que criou o lote. |


### Upload de arquivos

Agora que você criou um lote, é possível usar a variável `batchId` de antes para carregar arquivos no lote. Você pode fazer upload de vários arquivos para o lote.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Esse caminho de arquivo é o local onde o arquivo será salvo no lado do Adobe. |

**Solicitação**

>[!CAUTION]
>
>Essa API suporta o upload de parte única. Certifique-se de que o tipo de conteúdo seja application/octet-stream. Não use a opção curl -F, pois o padrão é a solicitação de várias partes incompatível com a API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Esse caminho de arquivo é o caminho de arquivo local, como `Users/sample-user/Downloads/sample.json`. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você deseja concluir. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```http
200 OK
```

## Apêndice

A seção a seguir contém informações adicionais para assimilação de dados no Experience Platform usando a ingestão em lote.

### Transformação de dados para ingestão em lote

Para assimilar um arquivo de dados no [!DNL Experience Platform], a estrutura hierárquica do processo deve estar em conformidade com a [Experience Data Model (XDM)](../../xdm/home.md) associado ao conjunto de dados para o qual está sendo carregado.

Informações sobre como mapear um arquivo CSV para estar em conformidade com um esquema XDM podem ser encontradas no [transformações de amostra](../../etl/transformations.md) documento, juntamente com um exemplo de um arquivo de dados JSON corretamente formatado. Arquivos de exemplo fornecidos no documento podem ser encontrados aqui:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
