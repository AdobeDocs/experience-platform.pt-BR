---
keywords: Experience Platform, baixar pontuações, atendimento ao cliente, tópicos populares, Exportar, exportar, download de ai do cliente, pontuações do atendimento ao cliente
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Fazer download de pontuações no Customer AI
topic-legacy: Downloading scores
description: O Customer AI permite baixar pontuações no formato de arquivo Parquet.
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---

# Fazer download de pontuações no Customer AI

Este documento é um guia para baixar pontuações para a API do cliente.

## Introdução

O Customer AI permite baixar pontuações no formato de arquivo Parquet. Este tutorial requer que você tenha lido e concluído o download da seção de pontuações do Customer AI no [introdução](../getting-started.md) guia.

Além disso, para acessar pontuações para o Customer AI, é necessário ter uma instância de serviço com um status de execução bem-sucedida disponível. Para criar uma nova instância de serviço, visite [Configuração de uma instância do Customer AI](./configure.md). Se você criou recentemente uma instância de serviço e ela ainda está treinando e pontuando, aguarde 24 horas para que ela termine de ser executada.

Atualmente, há duas maneiras de baixar as pontuações do Customer AI:

1. Se você quiser baixar as pontuações no nível individual e/ou não tiver o Perfil do cliente em tempo real ativado, comece navegando até [encontrar a ID do conjunto de dados](#dataset-id).
2. Se você tiver o Perfil ativado e quiser baixar segmentos configurados por meio da API do cliente, navegue até [baixar um segmento configurado com o Customer AI](#segment).

## Encontrar a ID do conjunto de dados {#dataset-id}

Na instância de serviço do Customer AI insights, clique no botão *Mais ações* lista suspensa na navegação superior direita e selecione **[!UICONTROL Pontuações de acesso]**.

![mais ações](../images/insights/more-actions.png)

Uma nova caixa de diálogo é exibida, contendo um link para a documentação de download de pontuações e a ID do conjunto de dados para sua instância atual. Copie a ID do conjunto de dados para a área de transferência e prossiga para a próxima etapa.

![ID do conjunto de dados](../images/download-scores/access-scores.png)

## Recuperar a ID do lote {#retrieve-your-batch-id}

Usando sua ID de conjunto de dados da etapa anterior, é necessário fazer uma chamada para a API de catálogo a fim de recuperar uma ID de lote. Parâmetros de consulta adicionais são usados para essa chamada de API para retornar o lote bem-sucedido mais recente em vez de uma lista de lotes pertencentes à sua organização. Para retornar lotes adicionais, aumente o número do parâmetro de consulta limite para a quantidade desejada que você deseja retornar. Para obter mais informações sobre os tipos de parâmetros de consulta disponíveis, visite o guia em [filtrar dados do catálogo usando parâmetros de consulta](../../../catalog/api/filter-data.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um objeto de ID em lote. Neste exemplo, o valor principal do objeto retornado é a ID do lote `01E5QSWCAASFQ054FNBKYV6TIQ`. Copie a ID do lote para usar na próxima chamada de API.

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

## Recupere a próxima chamada da API com a ID do lote {#retrieve-the-next-api-call-with-your-batch-id}

Depois de ter sua ID em lote, você pode fazer uma nova solicitação do GET para `/batches`. A solicitação retorna um link usado como a próxima solicitação da API.

**Formato da API**

```http
GET batches/{BATCH_ID}/files
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID de lote recuperada na etapa anterior [recuperar a ID do lote](#retrieve-your-batch-id). |

**Solicitação**

Usando sua própria ID de lote, faça a seguinte solicitação.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um `_links` objeto. No `_links` objeto é um `href` com uma nova chamada de API como seu valor. Copie esse valor para prosseguir para a próxima etapa.

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

## Recuperar arquivos {#retrieving-your-files}

Usar o `href` na etapa anterior como uma chamada de API, faça uma nova solicitação do GET para recuperar o diretório de arquivos.

**Formato da API**

```http
GET files/{DATASETFILE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASETFILE_ID}` | A ID de dataSetFile é retornada na variável `href` do [etapa anterior](#retrieve-the-next-api-call-with-your-batch-id). Também é acessível na variável `data` matriz sob o tipo de objeto `dataSetFileId`. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta contém uma matriz de dados que pode ter uma única entrada ou uma lista de arquivos pertencentes a esse diretório. O exemplo abaixo contém uma lista de arquivos e foi condensado para facilitar a leitura. Nesse cenário, é necessário seguir o URL de cada arquivo para acessar o arquivo.

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
| `_links.self.href` | O URL de solicitação do GET usado para baixar um arquivo em seu diretório. |


Copie o `href` para qualquer objeto de arquivo na `data` , em seguida, prossiga para a próxima etapa.

## Baixar os dados do arquivo

Para baixar os dados do arquivo, faça uma solicitação do GET para o `"href"` valor copiado na etapa anterior [recuperar arquivos](#retrieving-your-files).

>[!NOTE]
>
>Se você estiver fazendo essa solicitação diretamente na linha de comando, talvez seja solicitado que você adicione uma saída após os cabeçalhos da solicitação. O exemplo de solicitação a seguir usa `--output {FILENAME.FILETYPE}`.

**Formato da API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASETFILE_ID}` | A ID de dataSetFile é retornada na variável `href` valor de um [etapa anterior](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | O nome do arquivo. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Certifique-se de estar no diretório ou pasta corretos para a qual deseja salvar o arquivo antes de fazer a solicitação do GET.

**Resposta**

A resposta baixa o arquivo solicitado no diretório atual. Neste exemplo, o nome do arquivo é &quot;filename.parquet&quot;.

![Terminal](../images/download-scores/response.png)

## Baixar um segmento configurado com o Customer AI {#segment}

Uma maneira alternativa de baixar os dados de pontuação é exportar o público-alvo para um conjunto de dados. Após a conclusão bem-sucedida de um trabalho de segmentação (o valor da variável `status` é &quot;SUCCEEDED&quot;), você pode exportar seu público para um conjunto de dados, onde ele pode ser acessado e tratado. Para saber mais sobre a segmentação, visite o [visão geral da segmentação](../../../segmentation/home.md).

>[!IMPORTANT]
>
>Para utilizar esse método de exportação, o Perfil do cliente em tempo real precisa ser ativado para o conjunto de dados.

O [exportar um segmento](../../../segmentation/tutorials/evaluate-a-segment.md) A seção no guia de avaliação de segmento aborda as etapas necessárias para exportar um conjunto de dados de público-alvo. O guia descreve e fornece exemplos do seguinte:

- **Criar um conjunto de dados de destino:** Crie o conjunto de dados para manter os membros do público-alvo.
- **Gerar perfis de público-alvo no conjunto de dados:** Preencha o conjunto de dados com Perfis individuais XDM com base nos resultados de um trabalho de segmento.
- **Monitorar o progresso da exportação:** Verifique o progresso atual do processo de exportação.
- **Ler dados do público-alvo:** Recupere os perfis individuais XDM resultantes que representam os membros do seu público-alvo.

## Próximas etapas

Este documento descreve as etapas necessárias para baixar as pontuações do Customer AI. Agora você pode continuar a navegar no outro [Serviços inteligentes](../../home.md) e guias que são oferecidos.
