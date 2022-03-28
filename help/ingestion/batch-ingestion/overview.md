---
keywords: Experience Platform, home, tópicos populares, assimilação de dados, lote, lote, ativar conjunto de dados, visão geral da assimilação em lote, visão geral, visão geral da ingestão em lote;
solution: Experience Platform
title: Visão geral da API de assimilação em lote
topic-legacy: overview
description: A API de assimilação de dados do Adobe Experience Platform permite assimilar dados na Platform como arquivos em lote. Os dados que estão sendo assimilados podem ser os dados do perfil de um arquivo simples em um sistema CRM (como um arquivo Parquet) ou dados que estão em conformidade com um esquema conhecido no registro do Experience Data Model (XDM).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 75426b1ddc16af39eb6c423027fac7d4d0e21c6a
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 6%

---

# Visão geral da API de assimilação em lote

A API de assimilação de dados do Adobe Experience Platform permite assimilar dados na Platform como arquivos em lote. Os dados que estão sendo assimilados podem ser dados de perfil de um arquivo simples (como um arquivo Parquet) ou dados que estão em conformidade com um esquema conhecido na [!DNL Experience Data Model] Registro (XDM).

O [Referência da API da assimilação de dados](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) O fornece informações adicionais sobre essas chamadas de API.

O diagrama a seguir descreve o processo de ingestão em lote:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Introdução

Os endpoints de API usados neste guia fazem parte do [API de assimilação de dados](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Antes de continuar, reveja o [guia de introdução](getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

### [!DNL Data Ingestion] pré-requisitos

- Os dados para fazer upload devem estar nos formatos Parquet ou JSON.
- Um conjunto de dados criado na [[!DNL Catalog services]](../../catalog/home.md).
- O conteúdo do arquivo Parquet deve corresponder a um subconjunto do esquema do conjunto de dados no qual o upload está sendo feito.
- Ter seu Token de acesso exclusivo após a autenticação.

### Práticas recomendadas de assimilação de lote

- O tamanho de lote recomendado é entre 256 MB e 100 GB.
- Cada lote deve conter no máximo 1500 arquivos.

### Restrições de assimilação em lote

A assimilação de dados em lote tem algumas restrições:

- Número máximo de arquivos por lote: 1500
- Tamanho máximo do lote: 100 GB
- Número máximo de propriedades ou campos por linha: 10000
- Número máximo de lotes por minuto, por usuário: 138

>[!NOTE]
>
>Para carregar um arquivo com mais de 512 MB, o arquivo precisará ser dividido em partes menores. Instruções para carregar um arquivo grande podem ser encontradas no [seção de upload de arquivo grande deste documento](#large-file-upload---create-file).

### Tipos

Ao assimilar dados, é importante entender como [!DNL Experience Data Model] Os esquemas (XDM) funcionam. Para obter mais informações sobre como os tipos de campos XDM mapeiam para diferentes formatos, leia o [Guia do desenvolvedor do Registro de Schema](../../xdm/api/getting-started.md).

Há alguma flexibilidade na assimilação de dados - se um tipo não corresponder ao que está no schema de target, os dados serão convertidos para o tipo de target expresso. Se não puder, ocorrerá uma falha no lote com um `TypeCompatibilityException`.

Por exemplo, nem JSON nem CSV têm um `date` ou `date-time` tipo . Como resultado, esses valores são expressos usando [Strings formatadas ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) ou Tempo Unix formatado em milissegundos (1531263959000) e são convertidos no momento da assimilação para o tipo XDM de destino.

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

## Uso da API

O [!DNL Data Ingestion] A API permite assimilar dados como lotes (uma unidade de dados que consiste em um ou mais arquivos a serem assimilados como uma única unidade) em [!DNL Experience Platform] em três etapas básicas:

1. Crie um novo lote.
2. Faça upload de arquivos para um conjunto de dados especificado que corresponda ao esquema XDM dos dados.
3. Sinaliza o fim do lote.

## Criar um lote

Antes que os dados possam ser adicionados a um conjunto de dados, eles devem ser vinculados a um lote, que será carregado posteriormente em um conjunto de dados especificado.

```http
POST /batches
```

**Solicitação**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `datasetId` | A ID do conjunto de dados no qual os arquivos serão carregados. |

**Resposta**

```JSON
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

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | A ID do lote que acabou de ser criado (usada em solicitações subsequentes). |
| `relatedObjects.id` | A ID do conjunto de dados no qual os arquivos serão carregados. |

## Upload de arquivo

Depois de criar com êxito um novo lote para upload, os arquivos podem ser carregados em um conjunto de dados específico.

Você pode fazer upload de arquivos usando a API de upload de arquivo pequeno. No entanto, se os arquivos forem muito grandes e o limite do gateway for excedido (como tempos limite estendidos, solicitações para o tamanho do corpo excedido e outras restrições), você poderá alternar para a API de upload de arquivo grande. Essa API faz o upload do arquivo em blocos e une os dados usando a chamada de API de Upload de Arquivo Grande Concluído.

>[!NOTE]
>
>A assimilação em lote pode ser usada para atualizar gradualmente os dados na Loja de perfis. Para obter mais informações, consulte a seção em [atualização de um lote](#patch-a-batch) no [guia do desenvolvedor de ingestão em lote](api-overview.md).

>[!INFO]
>
>Os exemplos abaixo usam a variável [Apache Parquet](https://parquet.apache.org/docs/) formato de arquivo. Um exemplo que usa o formato de arquivo JSON pode ser encontrado no [guia do desenvolvedor de ingestão em lote](api-overview.md).

### Upload de arquivo pequeno

Depois que um lote é criado, os dados podem ser carregados em um conjunto de dados preexistente.  O arquivo que está sendo carregado deve corresponder ao esquema XDM referenciado.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote. |
| `{DATASET_ID}` | A ID do conjunto de dados para fazer upload de arquivos. |
| `{FILE_NAME}` | O nome do arquivo como será visto no conjunto de dados. |

**Solicitação**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
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

Para carregar um arquivo grande, o arquivo deve ser dividido em partes menores e carregado um de cada vez.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote. |
| `{DATASET_ID}` | A ID do conjunto de dados que assimila os arquivos. |
| `{FILE_NAME}` | O nome do arquivo como será visto no conjunto de dados. |

**Solicitação**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta**

```JSON
#Status 201 CREATED, with empty response body
```

### Carregamento de arquivo grande - carregue as partes subsequentes

Após a criação do arquivo, todos os fragmentos subsequentes podem ser carregados fazendo solicitações PATCH repetidas, uma para cada seção do arquivo.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote. |
| `{DATASET_ID}` | A ID do conjunto de dados no qual os arquivos serão carregados. |
| `{FILE_NAME}` | Nome do arquivo como será visto no conjunto de dados. |

**Solicitação**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
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

## Conclusão do lote de sinais

Depois que todos os arquivos tiverem sido carregados no lote, o lote poderá ser sinalizado para conclusão. Ao fazer isso, a variável [!DNL Catalog] As entradas DataSetFile são criadas para os arquivos concluídos e associadas ao lote gerado acima. O [!DNL Catalog] em seguida, o lote é marcado como bem-sucedido, o que aciona os fluxos downstream para assimilar os dados disponíveis.

**Solicitação**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote a ser carregado no conjunto de dados. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Resposta**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
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

O `"status"` é o que mostra o status atual do lote solicitado. Os lotes podem ter um dos seguintes estados:

## Status de assimilação em lote

| Status | Descrição |
| ------ | ----------- |
| Abandonado | O lote não foi concluído no período de tempo esperado. |
| Abortado | Uma operação abort tem **explicitamente** foi chamado (por meio da API de assimilação de lote) para o lote especificado. Quando o lote estiver em um estado &quot;Carregado&quot;, ele não poderá ser anulado. |
| Ativo | O lote foi promovido com êxito e está disponível para consumo downstream. Esse status pode ser usado alternadamente com &quot;Sucesso&quot;. |
| Excluído | Os dados do lote foram completamente removidos. |
| Falha | Um estado de terminal que resulta de uma configuração incorreta e/ou dados incorretos. Os dados de um lote com falha serão **not** aparecer. Esse status pode ser usado alternadamente com &quot;Falha&quot;. |
| Inativo | O lote foi promovido com êxito, mas foi revertido ou expirou. O lote não está mais disponível para consumo downstream. |
| Carregado | Os dados do lote estão completos e o lote está pronto para promoção. |
| Carregamento | Os dados deste lote estão sendo carregados e o lote está no momento **not** pronto para ser promovido. |
| Tentando novamente | Os dados desse lote estão sendo processados. No entanto, devido a um erro transitório ou de sistema, o lote falhou - como resultado, esse lote está sendo repetido. |
| Preparado | A fase de preparo do processo de promoção para um lote está concluída e o trabalho de assimilação foi executado. |
| Armazenamento temporário | Os dados do lote estão sendo processados. |
| Paralisado | Os dados do lote estão sendo processados. No entanto, a promoção em lote parou após várias tentativas. |
