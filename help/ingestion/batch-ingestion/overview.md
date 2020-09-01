---
keywords: Experience Platform;home;popular topics;data ingestion;batch;Batch;enable dataset;Batch ingestion overview;overview;batch ingestion overview;
solution: Experience Platform
title: Visão geral da ingestão em lote do Adobe Experience Platform
topic: overview
description: A API de ingestão em lote permite que você ingira dados no Adobe Experience Platform como arquivos em lote. Os dados sendo ingeridos podem ser os dados do perfil de um arquivo simples em um sistema CRM (como um arquivo parquet) ou dados que estejam em conformidade com um schema conhecido no registro do Modelo de Dados de Experiência (XDM).
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---


# [!DNL Batch Ingestion]visão geral

A [!DNL Batch Ingestion] API permite que você ingira dados no Adobe Experience Platform como arquivos em lote. Os dados que estão sendo ingeridos podem ser os dados do perfil de um arquivo simples em um sistema CRM (como um arquivo parquet) ou dados que estão em conformidade com um schema conhecido no registro [!DNL Experience Data Model] (XDM).

A referência [da API de ingestão de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) dados fornece informações adicionais sobre essas chamadas de API.

O diagrama a seguir descreve o processo de ingestão em lote:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Uso da API

A [!DNL Data Ingestion] API permite que você ingira dados como lotes (uma unidade de dados que consiste em um ou mais arquivos para serem ingeridos como uma única unidade) [!DNL Experience Platform] em três etapas básicas:

1. Crie um novo lote.
2. Faça upload de arquivos para um conjunto de dados especificado que corresponda ao schema XDM dos dados.
3. Sinal da extremidade do lote.


### [!DNL Data Ingestion] pré-requisitos

- Os dados a serem carregados devem estar nos formatos Parquet ou JSON.
- Um conjunto de dados criado no [[!DNL Catalog services]](../../catalog/home.md).
- O conteúdo do arquivo parquet deve corresponder a um subconjunto do schema do conjunto de dados para o qual está sendo feito upload.
- Tenha seu Token de acesso exclusivo após a autenticação.

### Práticas recomendadas de ingestão em lote

- O tamanho de lote recomendado é entre 256 MB e 100 GB.
- Cada lote deve conter no máximo 1500 arquivos.

Para carregar um arquivo maior que 512 MB, o arquivo precisará ser dividido em partes menores. As instruções para carregar um arquivo grande podem ser encontradas [aqui](#large-file-upload---create-file).

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

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

### Criar um lote

Antes que os dados possam ser adicionados a um conjunto de dados, eles devem estar vinculados a um lote, que será carregado posteriormente em um conjunto de dados especificado.

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
  -H "x-api-key : {API_KEY}"
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

## Carregamento de arquivo

Depois de criar com êxito um novo lote para upload, os arquivos podem ser carregados em um conjunto de dados específico.

Você pode fazer upload de arquivos usando a **Small File Upload API**. No entanto, se os arquivos forem muito grandes e o limite do gateway for excedido (como tempos limite estendidos, solicitações de tamanho de corpo excedido e outras restrições), você poderá alternar para a API **de upload de arquivo** grande. Essa API carrega o arquivo em blocos e une os dados usando a chamada **Large File Upload Complete API** .

>[!NOTE]
>
>Os exemplos abaixo usam o formato de arquivo [parquet](https://parquet.apache.org/documentation/latest/) . Um exemplo que usa o formato de arquivo JSON pode ser encontrado no guia [do desenvolvedor de ingestão em](./api-overview.md)lote.

### Upload de arquivo pequeno

Depois que um lote é criado, os dados podem ser carregados em um conjunto de dados preexistente.  O arquivo que está sendo carregado deve corresponder ao schema XDM referenciado.

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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | O caminho e o nome do arquivo a ser carregado no conjunto de dados. |

**Resposta**

```JSON
#Status 200 OK, with empty response body
```

### Carregamento de arquivo grande - criar arquivo

Para carregar um arquivo grande, o arquivo deve ser dividido em partes menores e carregado um de cada vez.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote. |
| `{DATASET_ID}` | A ID do conjunto de dados que está assimilando os arquivos. |
| `{FILE_NAME}` | O nome do arquivo como ele será visto no conjunto de dados. |

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

### Carregamento de arquivos grandes - carregue as partes subsequentes

Depois que o arquivo é criado, todos os blocos subsequentes podem ser carregados fazendo solicitações PATCH repetidas, uma para cada seção do arquivo.

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

Depois que todos os arquivos forem carregados no lote, o lote poderá ser sinalizado para conclusão. Ao fazer isso, as entradas [!DNL Catalog] DataSetFile **** são criadas para os arquivos concluídos e associadas ao lote gerado acima. O [!DNL Catalog] lote é marcado como bem-sucedido, o que aciona os fluxos downstream para assimilar os dados disponíveis.

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
-H "x-api-key : {API_KEY}"
```

**Resposta**

```JSON
#Status 200 OK, with empty response
```

## Verificar status do lote

Enquanto espera que os arquivos sejam carregados para o lote, o status do lote pode ser verificado para ver seu progresso.

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

O `"status"` campo é o que mostra o status atual do lote solicitado. Os lotes podem ter um dos seguintes estados:

## Status de ingestão em lote

| Status | Descrição |
| ------ | ----------- |
| Abandonado | O lote não foi concluído no período de tempo esperado. |
| Abortado | Uma operação abort foi chamada **explicitamente** (por meio da API de assimilação em lote) para o lote especificado. Quando o lote estiver em um estado **Carregado** , ele não poderá ser abortado. |
| Ativo | O lote foi promovido com êxito e está disponível para consumo a jusante. Esse status pode ser usado alternadamente com o **Success**. |
| Excluído | Os dados do lote foram completamente removidos. |
| Falha | Um estado de terminal que resulta de uma configuração incorreta e/ou de dados inválidos. Os dados de um lote com falha **não** serão exibidos. Esse status pode ser usado alternadamente com a **Falha**. |
| Inativo | O lote foi promovido com êxito, mas foi revertido ou expirou. O lote não está mais disponível para consumo a jusante. |
| Carregado | Os dados do lote estão completos e o lote está pronto para promoção. |
| Carregando | Os dados para este lote estão sendo carregados e o lote **não** está pronto para ser promovido no momento. |
| Tentando novamente | Os dados deste lote estão sendo processados. No entanto, devido a um erro transitório ou do sistema, o lote falhou - como resultado, esse lote está sendo repetido. |
| Preparado | A fase de preparo do processo de promoção para um lote está concluída e o trabalho de ingestão foi executado. |
| Armazenamento temporário | Os dados do lote estão sendo processados. |
| Parado | Os dados do lote estão sendo processados. No entanto, a promoção em lote parou após várias tentativas. |