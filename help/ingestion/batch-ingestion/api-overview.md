---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor de ingestão em lote de Adobe Experience Platform
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 6%

---


# Guia do desenvolvedor de ingestão em lote

Este documento fornece uma visão geral abrangente do uso de APIs [de ingestão em](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)lote.

O apêndice deste documento fornece informações para a [formatação de dados a serem usados para ingestão](#data-transformation-for-batch-ingestion), incluindo arquivos de dados CSV e JSON de amostra.

## Introdução

A ingestão de dados fornece uma RESTful API através da qual você pode executar operações CRUD básicas em relação aos tipos de objetos suportados.

As seções a seguir fornecem informações adicionais que você precisará conhecer ou ter em mãos para fazer chamadas com êxito para a API de ingestão em lote.

Este guia exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Ingestão](./overview.md)em lote: Permite assimilar dados em Adobe Experience Platform como arquivos em lote.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

As solicitações que contêm uma carga útil (POST, PUT, PATCH) podem exigir um `Content-Type` cabeçalho adicional. Os valores aceitos específicos para cada chamada são fornecidos nos parâmetros da chamada. Os seguintes tipos de conteúdo são usados neste guia:

- Tipo de conteúdo: application/json
- Tipo de conteúdo: application/octet-stream

## Tipos

Ao assimilar dados, é importante entender como os schemas [!DNL Experience Data Model] (XDM) funcionam. Para obter mais informações sobre como os tipos de campos XDM mapeiam para diferentes formatos, leia o guia [do desenvolvedor do Registro de](../../xdm/api/getting-started.md)Schemas.

Há alguma flexibilidade ao assimilar dados - se um tipo não corresponder ao que está no schema do público alvo, os dados serão convertidos no tipo de público alvo expresso. Se não puder, o lote será reprovado com um `TypeCompatibilityException`.

Por exemplo, nem JSON nem CSV têm um tipo de data ou data e hora. Como resultado, esses valores são expressos usando strings [formatadas com](https://www.iso.org/iso-8601-date-and-time-format.html) ISO 8061 (&quot;2018-07-10T15:05:59.000-08:00&quot;) ou Unix Time formatado em milissegundos (153126395 (9000) e são convertidos no momento da ingestão para o tipo XDM do público alvo.

A tabela abaixo mostra as conversões suportadas ao assimilar dados.

| Entrada (linha) vs Público alvo (col) | String | Byte | Curto | Número inteiro | Longo | Duplo | Data | Data e hora | Objeto | Mapa |
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

## Restrições de ingestão

A ingestão de dados em lote tem algumas restrições:
- Número máximo de arquivos por lote: 1500
- Tamanho máximo do lote: 100 GB
- Número máximo de propriedades ou campos por linha: 10000
- Número máximo de lotes por minuto, por usuário: 138

## Ingest arquivos JSON

>[!NOTE]
>
>As etapas a seguir são aplicáveis a arquivos pequenos (256 MB ou menos). Se você atingir um tempo limite do gateway ou solicitar erros de tamanho do corpo, precisará alternar para upload de arquivo grande.

### Criar lote

Primeiro, você precisará criar um lote, com JSON como o formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o schema XDM vinculado ao conjunto de dados fornecido.

>[!NOTE]
>
>Os exemplos abaixo são para JSON de linha única. Para assimilar JSON de várias linhas, o sinalizador `isMultiLineJson` precisa ser definido. Para obter mais informações, leia o guia [de solução de problemas de ingestão em](./troubleshooting.md)lote.

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

### Carregar arquivos

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. É possível carregar vários arquivos no lote.

>[!NOTE]
>
>Consulte a seção de apêndice para obter um [exemplo de um arquivo](#data-transformation-for-batch-ingestion)de dados JSON devidamente formatado.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja carregar. |

**Solicitação**

>[!NOTE]
>
>A API suporta carregamento de uma única peça. Verifique se o tipo de conteúdo é application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram carregados completamente e que o lote está pronto para promoção.

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

## Ingest Parquet files

>[!NOTE]
>
>As etapas a seguir são aplicáveis a arquivos pequenos (256 MB ou menos). Se você atingir um tempo limite do gateway ou solicitar erros de tamanho do corpo, precisará alternar para upload de arquivo grande.

### Criar lote

Em primeiro lugar, será necessário criar um lote, com o Parquet como o formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o schema XDM vinculado ao conjunto de dados fornecido.

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

### Carregar arquivos

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. É possível carregar vários arquivos no lote.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja carregar. |

**Solicitação**

>[!CAUTION]
>
>Esta API suporta carregamento de uma única peça. Verifique se o tipo de conteúdo é application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram carregados completamente e que o lote está pronto para promoção.

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

## Incorporar arquivos grandes do Parquet

>[!NOTE]
>
>Esta seção detalha como carregar arquivos com mais de 256 MB. Os arquivos grandes são carregados em partes e depois suturados por um sinal de API.

### Criar lote

Em primeiro lugar, será necessário criar um lote, com o Parquet como o formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o schema XDM vinculado ao conjunto de dados fornecido.

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

Depois de criar o lote, você precisará inicializar o arquivo grande antes de fazer upload de partes para o lote.

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

### Carregar partes grandes do arquivo

Agora que o arquivo foi criado, todos os blocos subsequentes podem ser carregados fazendo solicitações PATCH repetidas, uma para cada seção do arquivo.

**Formato da API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja carregar. |

**Solicitação**

>[!CAUTION]
>
>Esta API suporta carregamento de uma única peça. Verifique se o tipo de conteúdo é application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. |


**Resposta**

```http
200 OK
```

### Arquivo grande completo

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. É possível carregar vários arquivos no lote.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Resposta**

```http
201 Created
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram carregados completamente e que o lote está pronto para promoção.

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

## Ingressar arquivos CSV

Para assimilar arquivos CSV, é necessário criar uma classe, um schema e um conjunto de dados compatível com CSV. Para obter informações detalhadas sobre como criar a classe e o schema necessários, siga as instruções fornecidas no tutorial [de criação de schemas](../../xdm/api/ad-hoc.md)ad-hoc.

>[!NOTE]
>
>As etapas a seguir são aplicáveis a arquivos pequenos (256 MB ou menos). Se você atingir um tempo limite do gateway ou solicitar erros de tamanho do corpo, precisará alternar para o carregamento de arquivo grande.

### Criar conjunto de dados

Depois de seguir as instruções acima para criar a classe e o schema necessários, você precisará criar um conjunto de dados que possa suportar CSV.

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
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{TENANT_ID}` | Essa ID é usada para garantir que os recursos criados sejam devidamente nomeados e estejam contidos em sua Organização IMS. |
| `{SCHEMA_ID}` | A ID do schema que você criou. |

Uma explicação sobre a parte diferente da seção &quot;fileDescription&quot; do corpo JSON pode ser vista abaixo:

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `format` | O formato do arquivo mestre, não o formato do arquivo de entrada. |
| `delimiters` | O caractere a ser usado como delimitador. |
| `quotes` | O caractere a ser usado para aspas. |
| `escapes` | O caractere a ser usado como o caractere de escape. |
| `header` | O arquivo carregado **deve** conter cabeçalhos. Como a validação do schema é feita, isso deve ser definido como true. Além disso, os cabeçalhos **não** podem conter espaços - se você tiver espaços no cabeçalho, substitua-os por sublinhados. |
| `charset` | Um campo opcional. Outros caracteres suportados incluem &quot;US-ASCII&quot; e &quot;ISO-8869-1&quot;. Se deixado em branco, UTF-8 é assumido por padrão. |

O conjunto de dados referenciado deve ter o bloco de descrição de arquivo listado acima e deve apontar para um schema válido no registro. Caso contrário, o arquivo não será dominado em parquet.

### Criar lote

Em seguida, será necessário criar um lote com CSV como formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o schema vinculado ao conjunto de dados fornecido.

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

### Carregar arquivos

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. Você pode carregar vários arquivos no lote.

>[!NOTE]
>
>Consulte a seção de apêndice para obter um [exemplo de um arquivo](#data-transformation-for-batch-ingestion)de dados CSV corretamente formatado.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja carregar. |

**Solicitação**

>[!CAUTION]
>
>Esta API suporta carregamento de uma única peça. Verifique se o tipo de conteúdo é application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. |


**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram carregados completamente e que o lote está pronto para promoção.

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

Durante o processamento do lote, ele ainda pode ser cancelado. No entanto, quando um lote é finalizado (como um estado bem-sucedido ou com falha), o lote não pode ser cancelado.

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

Um lote pode ser excluído executando a seguinte solicitação POST com o parâmetro de `action=REVERT` query para a ID do lote que você deseja excluir. O lote é marcado como &quot;inativo&quot;, tornando-o elegível para coleta de lixo. O lote será coletado de forma assíncrona e, nesse momento, será marcado como &quot;excluído&quot;.

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

## Reproduzir novamente um lote

Se quiser substituir um lote já ingerido, você pode fazer isso com &quot;repetição em lote&quot; - essa ação equivale a excluir o lote antigo e ingerir um novo.

### Criar lote

Primeiro, você precisará criar um lote, com JSON como o formato de entrada. Ao criar o lote, será necessário fornecer uma ID de conjunto de dados. Você também precisará garantir que todos os arquivos carregados como parte do lote estejam em conformidade com o schema XDM vinculado ao conjunto de dados fornecido. Além disso, você precisará fornecer os lotes antigos como referência na seção de repetição. No exemplo abaixo, você está reproduzindo lotes com IDs `batchIdA` e `batchIdB`.

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


### Carregar arquivos

Agora que você criou um lote, é possível usar o `batchId` de antes para fazer upload de arquivos para o lote. Você pode carregar vários arquivos no lote.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote para o qual você deseja fazer upload. |
| `{DATASET_ID}` | A ID do conjunto de dados de referência do lote. |
| `{FILE_NAME}` | O nome do arquivo que você deseja carregar. |

**Solicitação**

>[!CAUTION]
>
>Esta API suporta carregamento de uma única peça. Verifique se o tipo de conteúdo é application/octet-stream. Não use a opção curl -F, pois o padrão é a solicitação de várias partes incompatível com a API.

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
| `{FILE_PATH_AND_NAME}` | O caminho completo e o nome do arquivo que você está tentando carregar. |

**Resposta**

```http
200 OK
```

### Concluir lote

Quando terminar de fazer upload de todas as diferentes partes do arquivo, será necessário sinalizar que os dados foram carregados completamente e que o lote está pronto para promoção.

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

Para assimilar um arquivo de dados, [!DNL Experience Platform]a estrutura hierárquica do arquivo deve estar em conformidade com o schema do Modelo de Dados de [Experiência (XDM)](../../xdm/home.md) associado ao conjunto de dados para o qual o upload está sendo feito.

Informações sobre como mapear um arquivo CSV para estar em conformidade com um schema XDM podem ser encontradas no documento de transformações [de](../../etl/transformations.md) amostra, juntamente com um exemplo de um arquivo de dados JSON devidamente formatado. Arquivos de amostra fornecidos no documento podem ser encontrados aqui:

- [CRM_perfis.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_perfis.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)