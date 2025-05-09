---
keywords: Experience Platform;página inicial;tópicos populares;assimilação em lote;Assimilação em lote;assimilação;guia do desenvolvedor;guia da api;carregar;assimilar parquet;assimilar json;
solution: Experience Platform
title: Guia da API de assimilação em lote
description: Este documento fornece um guia abrangente para desenvolvedores que trabalham com APIs de assimilação em lote para o Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '2435'
ht-degree: 6%

---

# Guia do desenvolvedor de assimilação em lote

Este documento fornece um guia abrangente sobre o uso de [pontos de extremidade da API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) no Adobe Experience Platform. Para obter uma visão geral das APIs de assimilação em lote, incluindo pré-requisitos e práticas recomendadas, comece lendo a [visão geral da API de assimilação em lote](overview.md).

O apêndice deste documento fornece informações sobre [dados de formatação a serem usados para assimilação](#data-transformation-for-batch-ingestion), incluindo arquivos de dados CSV e JSON de exemplo.

## Introdução

Os pontos de extremidade de API usados neste guia fazem parte da [API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). A assimilação em lote é fornecida por meio de uma API RESTful, na qual você pode executar operações CRUD básicas em relação aos tipos de objeto compatíveis.

Antes de continuar, revise a [visão geral da API de assimilação em lote](overview.md) e o [guia de introdução](getting-started.md).

## Assimilar arquivos JSON

>[!NOTE]
>
>- As etapas a seguir se aplicam a arquivos pequenos (256 MB ou menos). Se você atingir um tempo limite do gateway ou solicitar erros de tamanho do corpo, será necessário alternar para upload de arquivo grande.
>
>- Use JSON de linha única em vez de JSON de várias linhas como entrada para assimilação em lote. O JSON de linha única permite melhor desempenho, pois o sistema pode dividir um arquivo de entrada em várias partes e processá-las em paralelo, enquanto o JSON de várias linhas não pode ser dividido. Isso pode reduzir significativamente os custos de processamento de dados e melhorar a latência do processamento em lote.

### Criar lote

Primeiro, será necessário criar um lote, com JSON como formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido.

>[!NOTE]
>
>Os exemplos abaixo são para JSON de linha única. Para assimilar JSON multilinha, o sinalizador `isMultiLineJson` precisará ser definido. Para obter mais informações, leia o [guia de solução de problemas de assimilação em lote](./troubleshooting.md).

**Formato da API**

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

### Fazer upload de arquivos

Agora que você criou um lote, pode usar a ID do lote da resposta de criação do lote para fazer upload dos arquivos para o lote. É possível fazer upload de vários arquivos para o lote.

>[!NOTE]
>
>Consulte a seção do apêndice para obter um [exemplo de um arquivo de dados JSON formatado corretamente](#data-transformation-for-batch-ingestion).

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Certifique-se de usar um nome de arquivo exclusivo para que ele não entre em conflito com outro arquivo para o lote de arquivos que está sendo enviado. |

**Solicitação**

>[!NOTE]
>
>A API é compatível com o upload de parte única. Verifique se o tipo de conteúdo é application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Este caminho de arquivo é o caminho de arquivo local, como `acme/customers/campaigns/summer.json`. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, você precisará sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>As etapas a seguir se aplicam a arquivos pequenos (256 MB ou menos). Se você atingir um tempo limite do gateway ou solicitar erros de tamanho do corpo, será necessário alternar para upload de arquivo grande.

### Criar lote

Primeiro, será necessário criar um lote, com Parquet como formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido.

**Solicitação**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
    "imsOrg": "{ORG_ID}",
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

### Fazer upload de arquivos

Agora que você criou um lote, pode usar o `batchId` de antes para carregar arquivos no lote. É possível fazer upload de vários arquivos para o lote.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Certifique-se de usar um nome de arquivo exclusivo para que ele não entre em conflito com outro arquivo para o lote de arquivos que está sendo enviado. |

**Solicitação**

>[!CAUTION]
>
>Essa API oferece suporte para upload de parte única. Verifique se o tipo de conteúdo é application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Este caminho de arquivo é o caminho de arquivo local, como `acme/customers/campaigns/summer.parquet`. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, você precisará sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Esta seção detalha como carregar arquivos com mais de 256 MB. Os arquivos grandes são carregados em partes e depois compilados por um sinal de API.

### Criar lote

Primeiro, será necessário criar um lote, com Parquet como formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido.

**Formato da API**

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Depois de criar o lote, será necessário inicializar o arquivo grande antes de fazer upload dos blocos no lote.

**Formato da API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote recém-criado. |
| `{DATASET_ID}` | A ID do conjunto de dados referenciado. |
| `{FILE_NAME}` | O nome do arquivo que será inicializado. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
201 Created
```

### Fazer upload de grandes partes de arquivo

Agora que o arquivo foi criado, todos os blocos subsequentes podem ser carregados fazendo solicitações repetidas do PATCH, uma para cada seção do arquivo.

**Formato da API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Certifique-se de usar um nome de arquivo exclusivo para que ele não entre em conflito com outro arquivo para o lote de arquivos que está sendo enviado. |

**Solicitação**

>[!CAUTION]
>
>Essa API oferece suporte para upload de parte única. Verifique se o tipo de conteúdo é application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONTENT_RANGE}` | Em números inteiros, o início e o fim do intervalo solicitado. |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Este caminho de arquivo é o caminho de arquivo local, como `acme/customers/campaigns/summer.json`. |


**Resposta**

```http
200 OK
```

### Arquivo grande completo

Agora que você criou um lote, pode usar o `batchId` de antes para carregar arquivos no lote. É possível fazer upload de vários arquivos para o lote.

**Formato da API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote do qual você deseja sinalizar a conclusão. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo do qual você deseja sinalizar a conclusão. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
201 Created
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, você precisará sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você deseja sinalizar está concluída. |


**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

## Assimilar arquivos CSV

Para assimilar arquivos CSV, você precisará criar uma classe, esquema e um conjunto de dados que seja compatível com CSV. Para obter informações detalhadas sobre como criar a classe e o esquema necessários, siga as instruções fornecidas no [tutorial de criação de esquema ad-hoc](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>As etapas a seguir se aplicam a arquivos pequenos (256 MB ou menos). Se você atingir um tempo limite do gateway ou solicitar erros de tamanho do corpo, será necessário alternar para upload de arquivo grande.

### Criar conjunto de dados

Depois de seguir as instruções acima para criar a classe e o esquema necessários, será necessário criar um conjunto de dados que seja compatível com CSV.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{TENANT_ID}` | Essa ID é usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. |
| `{SCHEMA_ID}` | A ID do esquema criado. |

### Criar lote

Em seguida, será necessário criar um lote com CSV como o formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema vinculado ao conjunto de dados fornecido.

**Formato da API**

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

### Fazer upload de arquivos

Agora que você criou um lote, pode usar o `batchId` de antes para carregar arquivos no lote. É possível fazer upload de vários arquivos para o lote.

>[!NOTE]
>
>Consulte a seção do apêndice para obter um [exemplo de um arquivo de dados CSV corretamente formatado](#data-transformation-for-batch-ingestion).

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Certifique-se de usar um nome de arquivo exclusivo para que ele não entre em conflito com outro arquivo para o lote de arquivos que está sendo enviado. |

**Solicitação**

>[!CAUTION]
>
>Essa API oferece suporte para upload de parte única. Verifique se o tipo de conteúdo é application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Este caminho de arquivo é o caminho de arquivo local, como `acme/customers/campaigns/summer.csv`. |


**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, você precisará sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

**Formato da API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```http
200 OK
```

## Cancelar um lote

Enquanto o lote estiver sendo processado, ele ainda poderá ser cancelado. No entanto, uma vez que um lote é finalizado (como sucesso ou falha), ele não pode ser cancelado.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

## Excluir um lote {#delete-a-batch}

Um lote pode ser excluído executando a seguinte solicitação POST com o parâmetro de consulta `action=REVERT` para a ID do lote que você deseja excluir. O lote é marcado como &quot;inativo&quot;, tornando-o qualificado para a coleta de lixo. O lote será coletado de forma assíncrona e nesse momento será marcado como &quot;excluído&quot;.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

## Correção de um lote

Ocasionalmente, pode ser necessário atualizar os dados no armazenamento de perfil de sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. A Adobe Experience Platform oferece suporte à atualização ou correção de dados do Repositório de perfis por meio de uma ação de substituição ou &quot;correção de um lote&quot;.

>[!NOTE]
>
>Essas atualizações são permitidas somente em registros de perfil, não em eventos de experiência.

Para corrigir um lote, é necessário o seguinte:

- **Um conjunto de dados habilitado para atualizações de Perfil e atributo.** Isso é feito por meio de marcas de conjunto de dados e requer que uma marca `isUpsert:true` específica seja adicionada à matriz `unifiedProfile`. Para obter detalhes sobre as etapas que mostram como criar um conjunto de dados ou configurar um conjunto de dados existente para substituição, siga o tutorial para [habilitar um conjunto de dados para atualizações de Perfil](../../catalog/datasets/enable-upsert.md).
- **Um arquivo Parquet contendo os campos a serem corrigidos e os campos de identidade para o Perfil.** O formato dos dados para corrigir um lote é semelhante ao processo normal de assimilação de lotes. A entrada necessária é um arquivo Parquet e, além dos campos que serão atualizados, os dados carregados devem conter os campos de identidade para corresponder aos dados no armazenamento de Perfil.

Depois de habilitar um conjunto de dados para Perfil e substituição e um arquivo Parquet contendo os campos que você deseja corrigir, bem como os campos de identidade necessários, você pode seguir as etapas para [assimilar arquivos Parquet](#ingest-parquet-files) para concluir o patch por meio da assimilação em lote.

## Reproduzir um lote novamente

Se quiser substituir um lote já assimilado, faça isso com &quot;repetição em lote&quot;. Essa ação equivale a excluir o lote antigo e assimilar um novo.

### Criar lote

Primeiro, será necessário criar um lote, com JSON como formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido. Além disso, será necessário fornecer os lotes antigos como referência na seção de repetição. No exemplo abaixo, você está reproduzindo lotes com IDs `batchIdA` e `batchIdB`.

**Formato da API**

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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


### Fazer upload de arquivos

Agora que você criou um lote, pode usar o `batchId` de antes para carregar arquivos no lote. É possível fazer upload de vários arquivos para o lote.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja fazer upload. Certifique-se de usar um nome de arquivo exclusivo para que ele não entre em conflito com outro arquivo para o lote de arquivos que está sendo enviado. |

**Solicitação**

>[!CAUTION]
>
>Essa API oferece suporte para upload de parte única. Verifique se o tipo de conteúdo é application/octet-stream. Não use a opção curl -F, pois o padrão é uma solicitação de várias partes incompatível com a API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. Este caminho de arquivo é o caminho de arquivo local, como `acme/customers/campaigns/summer.json`. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, você precisará sinalizar que os dados foram totalmente carregados e que o lote está pronto para promoção.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```http
200 OK
```

## Apêndice

A seção a seguir contém informações adicionais para assimilação de dados no Experience Platform usando a assimilação em lote.

### Transformação de dados para assimilação em lote

Para assimilar um arquivo de dados em [!DNL Experience Platform], a estrutura hierárquica do arquivo deve estar em conformidade com o esquema [Experience Data Model (XDM)](../../xdm/home.md) associado ao conjunto de dados no qual está sendo carregado.

Informações sobre como mapear um arquivo CSV para estar em conformidade com um esquema XDM podem ser encontradas no documento [transformações de amostra](../../etl/transformations.md), juntamente com um exemplo de um arquivo de dados JSON formatado corretamente. Os arquivos de exemplo fornecidos no documento podem ser encontrados aqui:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
