---
keywords: Experience Platform, home, tópicos populares, ingestão em lote, ingestão em lote, ingestão, guia do desenvolvedor, guia da api, carregar, assimilar parquet, assimilar json;
solution: Experience Platform
title: Guia da API de assimilação em lote
topic: guia do desenvolvedor
description: Este documento fornece uma visão geral abrangente do uso de APIs de ingestão em lote.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 6%

---

# Guia da API de assimilação em lote

Este documento fornece uma visão geral abrangente do uso de [APIs de assimilação em lote](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

O apêndice a este documento fornece informações para [formatação de dados a serem usados para assimilação](#data-transformation-for-batch-ingestion), incluindo arquivos de dados CSV e JSON de amostra.

## Introdução

A assimilação de dados fornece uma RESTful API através da qual você pode executar operações básicas de CRUD em relação aos tipos de objetos suportados.

As seções a seguir fornecem informações adicionais que você precisará saber ou ter em mãos para fazer chamadas com êxito para a API de assimilação de lote.

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Ingestão](./overview.md) em lote: Permite assimilar dados no Adobe Experience Platform como arquivos em lote.
- [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

As solicitações que contêm uma carga útil (POST, PUT, PATCH) podem exigir um cabeçalho `Content-Type` adicional. Os valores aceitos específicos para cada chamada são fornecidos nos parâmetros de chamada .

## Tipos

Ao assimilar dados, é importante entender como os esquemas [!DNL Experience Data Model] (XDM) funcionam. Para obter mais informações sobre como os tipos de campos XDM mapeiam para diferentes formatos, leia o [Guia do desenvolvedor do Registro de Schema](../../xdm/api/getting-started.md).

Há alguma flexibilidade na assimilação de dados - se um tipo não corresponder ao que está no schema de target, os dados serão convertidos para o tipo de target expresso. Se não for possível, ocorrerá falha no lote com um `TypeCompatibilityException`.

Por exemplo, nem JSON nem CSV têm um tipo de data ou hora. Como resultado, esses valores são expressos usando [ISO 8061 strings formatadas](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) ou Unix Time formatado em milissegundos (153126 (3959000) e são convertidos no momento da assimilação para o tipo XDM de destino.

A tabela abaixo mostra as conversões suportadas ao assimilar dados.

| Entrada (linha) vs Destino (col) | String | Byte | Curto | Número inteiro | Longo | Duplo | Data | Data e hora | Objeto | Mapa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| String | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Curto | X | X | X | X | X | X |  |  |  |  |
| Número inteiro | X | X | X | X | X | X |  |  |  |  |
| Longo | X | X | X | X | X | X | X | X |  |  |
| Duplo | X | X | X | X | X | X |  |  |  |  |
| Data |  |  |  |  |  |  | X |  |  |  |
| Data e hora |  |  |  |  |  |  |  | X |  |  |
| Objeto |  |  |  |  |  |  |  |  | X | X |
| Mapa |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Booleanos e matrizes não podem ser convertidos em outros tipos.

## Restrições de assimilação

A assimilação de dados em lote tem algumas restrições:
- Número máximo de arquivos por lote: 1500
- Tamanho máximo do lote: 100 GB
- Número máximo de propriedades ou campos por linha: 10000
- Número máximo de lotes por minuto, por usuário: 138

## Assimilar arquivos JSON

>[!NOTE]
>
>As etapas a seguir são aplicáveis a arquivos pequenos (256 MB ou menos). Se você atingir o tempo limite do gateway ou solicitar erros de tamanho do corpo, precisará alternar para o upload de arquivo grande.

### Criar lote

Primeiro, você precisará criar um lote, com JSON como o formato de entrada. Ao criar o lote, é necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o esquema XDM vinculado ao conjunto de dados fornecido.

>[!NOTE]
>
>Os exemplos abaixo são para JSON de linha única. Para assimilar JSON de várias linhas, o sinalizador `isMultiLineJson` precisará ser definido. Para obter mais informações, leia o [guia de solução de problemas de ingestão em lote](./troubleshooting.md).

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
  -H 'x-api-key : {API_KEY}' \
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

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. Você pode fazer upload de vários arquivos para o lote.

>[!NOTE]
>
>Consulte a seção de apêndice para obter um [exemplo de um arquivo de dados JSON corretamente formatado](#data-transformation-for-batch-ingestion).

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
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```http
200 OK
```

## Assimilar arquivos do Parquet

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
  -H "x-api-key : {API_KEY}" \
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

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. Você pode fazer upload de vários arquivos para o lote.

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
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-api-key : {API_KEY}' \
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

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. Você pode fazer upload de vários arquivos para o lote.

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
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-api-key : {API_KEY}' \
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

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. Você pode fazer upload de vários arquivos para o lote.

>[!NOTE]
>
>Consulte a seção de apêndice para obter um [exemplo de um arquivo de dados CSV corretamente formatado](#data-transformation-for-batch-ingestion).

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
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

## Excluir um lote {#delete-a-batch}

Um lote pode ser excluído executando a seguinte solicitação de POST com o parâmetro de consulta `action=REVERT` para a ID do lote que você deseja excluir. O lote é o marcado como &quot;inativo&quot;, tornando-o elegível para a coleta de lixo. O lote será coletado de forma assíncrona e, nesse momento, será marcado como &quot;excluído&quot;.

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
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
200 OK
```

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
  -H 'x-api-key : {API_KEY}' \
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

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. Você pode fazer upload de vários arquivos para o lote.

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
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```http
200 OK
```

## Apêndice

### Transformação de dados para ingestão em lote

Para assimilar um arquivo de dados em [!DNL Experience Platform], a estrutura hierárquica do arquivo deve estar em conformidade com o esquema [Experience Data Model (XDM)](../../xdm/home.md) associado ao conjunto de dados para o qual o upload está sendo feito.

Informações sobre como mapear um arquivo CSV para estar em conformidade com um esquema XDM podem ser encontradas no documento [de transformações de amostra](../../etl/transformations.md), juntamente com um exemplo de um arquivo de dados JSON formatado corretamente. Arquivos de exemplo fornecidos no documento podem ser encontrados aqui:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
