---
keywords: Experience Platform;página inicial;tópicos populares;assimilação de dados;lote;Lote;habilitar conjunto de dados;Visão geral da assimilação em lote;visão geral da assimilação em lote;
solution: Experience Platform
title: Visão geral da API de assimilação em lote
description: A API de assimilação em lote do Adobe Experience Platform permite assimilar dados na Experience Platform como arquivos em lote. Os dados assimilados podem ser os dados do perfil de um arquivo simples em um sistema CRM (como um arquivo Parquet) ou dados que estejam em conformidade com um esquema conhecido no registro do Experience Data Model (XDM).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: dace7bc2f7940748422628b62f0f57854036ad3f
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 7%

---

# Visão geral da API de assimilação em lote

A API de assimilação em lote do Adobe Experience Platform permite assimilar dados na Experience Platform como arquivos em lote. Os dados assimilados podem ser dados de perfil de um arquivo simples (como um arquivo Parquet) ou dados que estejam em conformidade com um esquema conhecido no registro [!DNL Experience Data Model] (XDM).

A [Referência da API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) fornece informações adicionais sobre essas chamadas de API.

O diagrama a seguir descreve o processo de assimilação em lote:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Introdução

Os pontos de extremidade de API usados neste guia fazem parte da [API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

### [!DNL Data Ingestion] pré-requisitos

- Os dados para upload devem estar nos formatos Parquet ou JSON.
- Um conjunto de dados criado no [[!DNL Catalog services]](../../catalog/home.md).
- O conteúdo do arquivo Parquet deve corresponder a um subconjunto do esquema do conjunto de dados que está sendo carregado no.
- Tenha seu token de acesso exclusivo após a autenticação.

### Práticas recomendadas de assimilação em lote

- O tamanho de lote recomendado é entre 256 MB e 100 GB.
- Cada lote deve conter no máximo 1500 arquivos.

### Restrições de assimilação em lote

A assimilação de dados em lote tem algumas restrições:

- Número máximo de arquivos por lote: 1500
- Tamanho máximo do lote: 100 GB
- Número máximo de propriedades ou campos por linha: 10000
- Número máximo de lotes no data lake por minuto, por usuário: 2000

>[!NOTE]
>
>Para carregar um arquivo com mais de 512 MB, ele precisará ser dividido em partes menores. As instruções para carregar um arquivo grande podem ser encontradas na [seção de carregamento de arquivo grande deste documento](#large-file-upload---create-file).

### Tipos

Ao assimilar dados, é importante entender como os esquemas do [!DNL Experience Data Model] (XDM) funcionam. Para obter mais informações sobre como os tipos de campo XDM são mapeados para formatos diferentes, leia o [guia do desenvolvedor do Registro de Esquemas](../../xdm/api/getting-started.md).

Há alguma flexibilidade ao assimilar dados - se um tipo não corresponder ao que está no esquema do público-alvo, os dados serão convertidos no tipo de público-alvo expresso. Se não puder, haverá falha no lote com um `TypeCompatibilityException`.

Por exemplo, nem JSON nem CSV têm um tipo `date` ou `date-time`. Como resultado, esses valores são expressos usando [cadeias de caracteres formatadas em ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) ou Tempo Unix formatados em milissegundos (1531263959000) e são convertidos no momento da assimilação para o tipo XDM de destino.

A tabela abaixo mostra as conversões compatíveis ao assimilar dados.

| Entrada (linha) vs. Destino (coluna) | String | Byte | Curto | Número inteiro | Longo | Duplo | Data | Data e hora | Objeto | Mapa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| String | X | X | X | X | X | X | X | X |   |   |
| Byte | X | X | X | X | X | X |   |   |   |   |
| Curto | X | X | X | X | X | X |   |   |   |   |
| Número inteiro | X | X | X | X | X | X |   |   |   |   |
| Longo | X | X | X | X | X | X | X | X |   |   |
| Duplo | X | X | X | X | X | X |   |   |   |   |
| Data |   |   |   |   |   |   | X |   |   |   |
| Data e hora |   |   |   |   |   |   |   | X |   |   |
| Objeto |   |   |   |   |   |   |   |   | X | X |
| Mapa |   |   |   |   |   |   |   |   | X | X |

>[!NOTE]
>
>Booleanos e matrizes não podem ser convertidos em outros tipos.

## Uso da API

A API [!DNL Data Ingestion] permite assimilar dados como lotes (uma unidade de dados que consiste em um ou mais arquivos a serem assimilados como uma única unidade) no [!DNL Experience Platform] em três etapas básicas:

1. Crie um novo lote.
2. Faça upload de arquivos para um conjunto de dados especificado que corresponda ao esquema XDM dos dados.
3. Sinalizar o final do lote.

## Criar um lote

Para que os dados possam ser adicionados a um conjunto de dados, eles devem estar vinculados a um lote, que será carregado posteriormente em um conjunto de dados especificado.

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `datasetId` | A ID do conjunto de dados para onde carregar os arquivos. |

**Resposta**

```JSON
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

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | A ID do lote que acabou de ser criado (usada em solicitações subsequentes). |
| `relatedObjects.id` | A ID do conjunto de dados para onde carregar os arquivos. |

## Upload de arquivo

Depois de criar um novo lote para upload com sucesso, os arquivos podem ser carregados para um conjunto de dados específico.

É possível fazer upload de arquivos usando a API de upload de arquivo pequeno. No entanto, se os arquivos forem muito grandes e o limite do gateway for excedido (como tempos limite estendidos, solicitações de tamanho do corpo excedido e outras restrições), você poderá alternar para a API de upload de arquivo grande. Essa API faz upload do arquivo em partes e compila os dados usando a chamada de API Upload de arquivo grande concluído.

>[!NOTE]
>
>A assimilação em lote pode ser usada para atualizar dados de forma incremental no armazenamento de perfis. Para obter mais informações, consulte a seção sobre [atualização de um lote](#patch-a-batch) no [guia do desenvolvedor de assimilação em lote](api-overview.md).

>[!INFO]
>
>Os exemplos abaixo usam o formato de arquivo [Apache Parquet](https://parquet.apache.org/docs/). Um exemplo que usa o formato de arquivo JSON pode ser encontrado no [guia do desenvolvedor de assimilação em lote](api-overview.md).

### Upload de arquivo pequeno

Após a criação de um lote, os dados podem ser carregados em um conjunto de dados preexistente.  O arquivo que está sendo carregado deve corresponder ao esquema XDM referenciado.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote. |
| `{DATASET_ID}` | A ID do conjunto de dados para carregar arquivos. |
| `{FILE_NAME}` | O nome do arquivo como ele será visto no conjunto de dados. |

**Solicitação**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho e o nome do arquivo a ser carregado no conjunto de dados. |

**Resposta**

```JSON
#Status 200 OK, with empty response body
```

### Upload de arquivo grande - criar arquivo

Para carregar um arquivo grande, ele deve ser dividido em partes menores e carregado uma de cada vez.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote. |
| `{DATASET_ID}` | A ID do conjunto de dados que assimila os arquivos. |
| `{FILE_NAME}` | O nome do arquivo como ele será visto no conjunto de dados. |

**Solicitação**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta**

```JSON
#Status 201 CREATED, with empty response body
```

### Upload de arquivo grande - carregar partes subsequentes

Após a criação do arquivo, é possível fazer upload de todas as partes subsequentes fazendo solicitações repetidas do PATCH, uma para cada seção do arquivo.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote. |
| `{DATASET_ID}` | A ID do conjunto de dados para onde carregar os arquivos. |
| `{FILE_NAME}` | Nome do arquivo como ele será visto no conjunto de dados. |

**Solicitação**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho e o nome do arquivo a ser carregado no conjunto de dados. |

**Resposta**

```JSON
#Status 200 OK, with empty response
```

## Sinal de conclusão de lote

Depois que todos os arquivos tiverem sido carregados no lote, o lote poderá ser marcado para conclusão. Ao fazer isso, as [!DNL Catalog] entradas de DataSetFile são criadas para os arquivos concluídos e associadas ao lote gerado acima. O lote [!DNL Catalog] é marcado como bem-sucedido, o que aciona fluxos downstream para assimilar os dados disponíveis.

**Solicitação**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote a ser carregado no conjunto de dados. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**Resposta**

```JSON
#Status 200 OK, with empty response
```

## Verificar status do lote

Enquanto aguarda os arquivos serem carregados no lote, o status do lote pode ser verificado para ver seu progresso.

**Formato da API**

```http
GET /batch/{BATCH_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que está sendo verificado. |

**Solicitação**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{USER_ID}` | A ID do usuário que criou ou atualizou o lote. |

O campo `"status"` é o que mostra o status atual do lote solicitado. Os lotes podem ter um dos seguintes estados:

## Status de assimilação em lote

| Status | Descrição |
| ------ | ----------- |
| Abandonado | O lote não foi concluído no prazo esperado. |
| Anulado | Uma operação de anulação foi **explicitamente** chamada (por meio da API de assimilação em lote) para o lote especificado. Quando o lote estiver no estado &quot;Carregado&quot;, ele não poderá ser abortado. |
| Ativo | O lote foi promovido com sucesso e está disponível para consumo downstream. Esse status pode ser usado alternadamente com &quot;Sucesso&quot;. |
| Excluído | Os dados do lote foram completamente removidos. |
| Com falha | Um estado terminal que resulta de uma configuração incorreta e/ou de dados incorretos. Os dados de um lote com falha **não** serão exibidos. Esse status pode ser usado alternadamente com &quot;Falha&quot;. |
| Inativo | O lote foi promovido com sucesso, mas foi revertido ou expirou. O lote não está mais disponível para consumo downstream. |
| Carregado | Os dados do lote estão concluídos e o lote está pronto para promoção. |
| Carregando | Os dados deste lote estão sendo carregados e o lote atualmente **não** está pronto para ser promovido. |
| Repetindo | Os dados desse lote estão sendo processados. No entanto, devido a um erro de sistema ou transitório, o lote falhou; como resultado, esse lote está sendo repetido. |
| Preparado | A fase de preparo do processo de promoção de um lote está concluída e o trabalho de assimilação foi executado. |
| Armazenamento temporário | Os dados do lote estão sendo processados. |
| Paralisado | Os dados do lote estão sendo processados. No entanto, a promoção em lote foi interrompida após várias tentativas. |
