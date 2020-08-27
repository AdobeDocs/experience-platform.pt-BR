---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: Download de pontuações na IA do cliente
topic: Downloading scores
description: A IA do cliente permite baixar pontuações no formato de arquivo de parâmetro.
translation-type: tm+mt
source-git-commit: c30bbaead775e68f869b080e24e18d4a23cda973
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 2%

---


# Download de pontuações na IA do cliente

Este documento serve como um guia para o download das pontuações para a IA do cliente.

## Introdução

A IA do cliente permite baixar pontuações no formato de arquivo de parâmetro. Este tutorial requer que você tenha lido e concluído o download da seção de pontuações da AI do cliente no guia de [introdução](../getting-started.md) .

Além disso, para acessar as pontuações da API do cliente, é necessário ter uma instância de serviço com um status de execução bem-sucedida disponível. Para criar uma nova instância de serviço, visite [Configuração de uma instância](./configure.md)do AI do cliente. Se você criou recentemente uma instância de serviço e ela ainda está treinando e marcando, aguarde 24 horas para que ela termine de ser executada.

Atualmente, existem duas maneiras de baixar as pontuações do AI do cliente:

1. Se você quiser baixar as pontuações no nível individual e/ou não tiver o Perfil do cliente em tempo real ativado, navegue para [encontrar a ID](#dataset-id)do conjunto de dados.
2. Se você tiver o Perfil ativado e quiser baixar segmentos configurados usando a API do cliente, navegue para [baixar um segmento configurado com a IA](#segment)do cliente.

## Find your dataset ID {#dataset-id}

Em sua instância de serviço para insights de IA do cliente, clique na lista suspensa *Mais ações* na navegação superior direita e selecione Pontuações **[!UICONTROL de]** acesso.

![mais ações](../images/insights/more-actions.png)

Uma nova caixa de diálogo é exibida, contendo um link para a documentação das pontuações de download e a ID do conjunto de dados da sua instância atual. Copie a ID do conjunto de dados para a área de transferência e prossiga para a próxima etapa.

![ID do conjunto de dados](../images/download-scores/access-scores.png)

## Recuperar a ID do lote {#retrieve-your-batch-id}

Usando a ID do conjunto de dados da etapa anterior, é necessário fazer uma chamada para a API de catálogo para recuperar uma ID de lote. Parâmetros de query adicionais são usados para esta chamada de API a fim de retornar o lote bem-sucedido mais recente em vez de uma lista de lotes pertencentes à sua organização. Para retornar lotes adicionais, aumente o número do parâmetro de query de limite para a quantia desejada que você deseja que seja retornada. Para obter mais informações sobre os tipos de parâmetros de query disponíveis, visite o guia sobre como [filtrar dados do catálogo usando parâmetros](../../../catalog/api/filter-data.md)de query.

**Formato da API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID do conjunto de dados disponível na caixa de diálogo &quot;Pontuações de acesso&quot;. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um objeto de ID de lote. Neste exemplo, o valor chave para o objeto retornado é a ID do lote `01E5QSWCAASFQ054FNBKYV6TIQ`. Copie a ID do lote para usar na próxima chamada da API.

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## Recuperar a próxima chamada de API com sua ID de lote {#retrieve-the-next-api-call-with-your-batch-id}

Depois de ter a ID do lote, você poderá fazer uma nova solicitação de GET para `/batches`. A solicitação retorna um link usado como a próxima solicitação de API.

**Formato da API**

```http
GET batches/{BATCH_ID}/files
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID de lote recuperada na etapa anterior [recupera a ID](#retrieve-your-batch-id)de lote. |

**Solicitação**

Usando sua própria ID de lote, faça a seguinte solicitação.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga que contém um `_links` objeto. Dentro do `_links` objeto há uma nova chamada de API `href` com seu valor. Copie esse valor para prosseguir para a próxima etapa.

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## Recuperar seus arquivos {#retrieving-your-files}

Usando o `href` valor obtido na etapa anterior como uma chamada de API, faça uma nova solicitação de GET para recuperar seu diretório de arquivos.

**Formato da API**

```http
GET files/{DATASETFILE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASETFILE_ID}` | A ID dataSetFile é retornada no `href` valor da etapa [](#retrieve-the-next-api-call-with-your-batch-id)anterior. Ele também pode ser acessado na `data` matriz sob o tipo de objeto `dataSetFileId`. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta contém uma matriz de dados que pode ter uma única entrada ou uma lista de arquivos pertencentes a esse diretório. O exemplo abaixo contém uma lista de arquivos e foi condensado para leitura. Nesse cenário, é necessário seguir o URL de cada arquivo para acessar o arquivo.

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `_links.self.href` | O URL de solicitação de GET usado para baixar um arquivo em seu diretório. |


Copie o `href` valor para qualquer objeto de arquivo na `data` matriz e prossiga para a próxima etapa.

## Baixar seus dados de arquivo

Para baixar os dados do arquivo, faça uma solicitação de GET para o `"href"` valor copiado na etapa anterior [que recupera os arquivos](#retrieving-your-files).

>[!NOTE]
>
>Se você estiver fazendo essa solicitação diretamente na linha de comando, talvez seja solicitado que você adicione uma saída após os cabeçalhos da solicitação. O exemplo de solicitação a seguir usa `--output {FILENAME.FILETYPE}`.

**Formato da API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASETFILE_ID}` | A ID dataSetFile é retornada no `href` valor de uma etapa [](#retrieve-the-next-api-call-with-your-batch-id)anterior. |
| `{FILE_NAME}` | O nome do arquivo. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Verifique se você está no diretório ou pasta corretos na qual deseja salvar o arquivo antes de fazer a solicitação de GET.

**Resposta**

A resposta baixa o arquivo solicitado no diretório atual. Neste exemplo, o nome do arquivo é &quot;filename.parquet&quot;.

![Terminal](../images/download-scores/response.png)

## Baixar um segmento configurado com a API do cliente {#segment}

Uma maneira alternativa de baixar seus dados de pontuação é exportar sua audiência para um conjunto de dados. Depois que um trabalho de segmentação for concluído com êxito (o valor do `status` atributo é &quot;SUCEDIDO&quot;), você poderá exportar sua audiência para um conjunto de dados no qual ele possa ser acessado e executado. Para saber mais sobre a segmentação, visite a visão geral [da](../../../segmentation/home.md)segmentação.

>[!IMPORTANT]
>
>Para utilizar esse método de exportação, o Perfil do cliente em tempo real precisa ser habilitado para o conjunto de dados.

A seção [Exportar um segmento](../../../segmentation/tutorials/evaluate-a-segment.md) no guia de avaliação de segmento cobre as etapas necessárias para exportar um conjunto de dados de audiência. O guia descreve e fornece exemplos do seguinte:

- **Criar um conjunto de dados de público alvo:** Crie o conjunto de dados para manter membros da audiência.
- **Gerar perfis de audiência no conjunto de dados:** Preencha o conjunto de dados com Perfis individuais XDM com base nos resultados de um trabalho de segmento.
- **Monitorar progresso de exportação:** Verifique o andamento atual do processo de exportação.
- **Ler dados de audiência:** Recupere os Perfis individuais XDM resultantes que representam os membros de sua audiência.

## Próximas etapas

Este documento descreveu as etapas necessárias para baixar as pontuações da AI do cliente. Agora você pode continuar navegando pelos outros serviços [e guias](../../home.md) inteligentes oferecidos.
