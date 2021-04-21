---
keywords: Experience Platform, atribuição ai, pontuações de acesso, tópicos populares, pontuações de download, pontuações de atribuição ai, exportar, exportar
solution: Experience Platform, Intelligent Services
title: Fazer download das pontuações no Attribution AI
topic-legacy: Downloading scores
description: Este documento serve como um guia para baixar pontuações para o Attribution AI.
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 2%

---

# Fazer download de pontuações no Attribution AI

Este documento serve como um guia para baixar pontuações para o Attribution AI.

## Introdução

O Attribution AI permite baixar pontuações no formato de arquivo Parquet. Este tutorial requer que você tenha lido e concluído a seção de download de pontuações do Attribution AI no guia [introdução](./getting-started.md).

Além disso, para acessar pontuações para o Attribution AI, é necessário ter uma instância de serviço com um status de execução bem-sucedida disponível. Para criar uma nova instância de serviço, visite o [guia do usuário do Attribution AI](./user-guide.md). Se você criou recentemente uma instância de serviço e ela ainda está treinando e pontuando, aguarde 24 horas para que ela termine de ser executada.

## Encontrar a ID do conjunto de dados {#dataset-id}

Na instância de serviço do Attribution AI insights, clique na lista suspensa *Mais ações* na navegação superior direita e selecione **[!UICONTROL Access scores]**.

![mais ações](./images/download-scores/more-actions.png)

Uma nova caixa de diálogo é exibida, contendo um link para a documentação de download de pontuações e a ID do conjunto de dados para sua instância atual. Copie a ID do conjunto de dados para a área de transferência e prossiga para a próxima etapa.

![ID do conjunto de dados](../customer-ai/images/download-scores/access-scores.png)

## Recuperar a ID do lote {#retrieve-your-batch-id}

Usando sua ID de conjunto de dados da etapa anterior, é necessário fazer uma chamada para a API de catálogo a fim de recuperar uma ID de lote. Parâmetros de consulta adicionais são usados para essa chamada de API para retornar o lote bem-sucedido mais recente em vez de uma lista de lotes pertencentes à sua organização. Para retornar lotes adicionais, aumente o número do parâmetro de consulta `limit` para a quantidade desejada que você deseja retornar. Para obter mais informações sobre os tipos de parâmetros de consulta disponíveis, visite o guia sobre [filtragem de dados do catálogo usando parâmetros de consulta](../../catalog/api/filter-data.md).

**Formato da API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID do conjunto de dados disponível na caixa de diálogo &quot;Pontuações de acesso&quot;. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um objeto de ID em lote. Neste exemplo, o valor Chave para o objeto retornado é a ID do lote `01E5QSWCAASFQ054FNBKYV6TIQ`. Copie a ID do lote para usar na próxima chamada de API.

>[!NOTE]
>
> A resposta a seguir teve o objeto `tags` reformado para facilitar a leitura.

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
                "id": "5e8f81cf7a4ecb28a8d85b22"
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

Depois de ter sua ID de lote, você pode fazer uma nova solicitação de GET para `/batches`. A solicitação retorna um link usado como a próxima solicitação da API.

**Formato da API**

```http
GET batches/{BATCH_ID}/files
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A ID do lote que foi recuperada na etapa anterior [recupere a ID do lote](#retrieve-your-batch-id). |

**Solicitação**

Usando sua própria ID de lote, faça a seguinte solicitação.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo um objeto `_links`. No objeto `_links` há um `href` com uma nova chamada de API como seu valor. Copie esse valor para prosseguir para a próxima etapa.

```json
{
    "data": [
        {
            "dataSetFileId": "01E5QSWCAASFQ054FNBKYV6TIQ-1",
            "dataSetViewId": "5e8f81cf7a4ecb28a8d85b22",
            "version": "1.0.0",
            "created": "1586715582571",
            "updated": "1586715582571",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1"
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

## Recupere seus arquivos {#retrieving-your-files}

Usando o valor `href` obtido na etapa anterior como uma chamada de API, faça uma nova solicitação do GET para recuperar o diretório de arquivos.

**Formato da API**

```http
GET files/{DATASETFILE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASETFILE_ID}` | A ID dataSetFile é retornada no valor `href` da [etapa anterior](#retrieve-the-next-api-call-with-your-batch-id). Também é acessível na matriz `data` sob o tipo de objeto `dataSetFileId`. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta contém uma matriz de dados que pode ter uma única entrada ou uma lista de arquivos pertencentes a esse diretório. O exemplo abaixo contém uma lista de arquivos e foi condensado para facilitar a leitura. Nesse cenário, é necessário seguir o URL de cada arquivo para acessar o arquivo.

```json
{
    "data": [
        {
            "name": "part-00000-tid-5614147572541837832-908bd66a-d856-47fe-b7da-c8e7d22a4097-1370467-1.c000.snappy.parquet",
            "length": "2380211",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet"
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

| Parâmetro | Descrição |
| --------- | ----------- |
| `_links.self.href` | O URL de solicitação do GET usado para baixar um arquivo em seu diretório. |


Copie o valor `href` para qualquer objeto de arquivo na matriz `data` e prossiga para a próxima etapa.

## Baixar os dados do arquivo

Para baixar os dados do arquivo, faça uma solicitação GET para o valor `"href"` copiado na etapa anterior [recuperar os arquivos](#retrieving-your-files).

>[!NOTE]
>
>Se você estiver fazendo essa solicitação diretamente na linha de comando, talvez seja solicitado que você adicione uma saída após os cabeçalhos da solicitação. O exemplo de solicitação a seguir usa `--output {FILENAME.FILETYPE}`.

**Formato da API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASETFILE_ID}` | A ID dataSetFile é retornada no valor `href` de uma [etapa anterior](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | O nome do arquivo. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Certifique-se de estar no diretório ou pasta corretos para a qual deseja salvar o arquivo antes de fazer a solicitação do GET.

**Resposta**

A resposta baixa o arquivo solicitado no diretório atual. Neste exemplo, o nome do arquivo é &quot;file.parquet&quot;.

![Terminal](./images/download-scores/terminal-output.png)

As pontuações baixadas estarão no formato Parquet e precisarão de um [!DNL Spark]-shell ou leitor Parquet para visualizar as pontuações. Para visualização de pontuação bruta, você pode usar [Ferramentas do Apache Parquet](https://github.com/apache/parquet-mr/tree/master/parquet-tools). As ferramentas do Parquet podem analisar os dados com [!DNL Spark].

## Próximas etapas

Este documento descreve as etapas necessárias para o download das pontuações do Attribution AI. Para obter mais informações sobre os resultados da pontuação, visite a documentação [Attribution AI input and output](./input-output.md).

## Acessar pontuações usando o Snowflake

>[!IMPORTANT]
>
>Entre em contato com attributionai-support@adobe.com para obter mais detalhes sobre como acessar pontuações usando o Snowflake.

Você pode acessar pontuações de Attribution AI agregadas por meio do Snowflake. Atualmente, você precisa enviar o suporte ao Adobe por email para attributionai-support@adobe.com para configurar e receber as credenciais da conta de leitor para o Snowflake.

Depois que o suporte ao Adobe processar sua solicitação, você receberá um URL para a conta do leitor no Snowflake e as credenciais correspondentes abaixo:

- Snowflake URL
- Nome do usuário
- Senha

>[!NOTE]
>
>A conta do leitor é para consultar os dados usando clientes sql, planilha e soluções BI que oferecem suporte ao conector JDBC.

Depois de ter suas credenciais e URL, você pode consultar as tabelas do modelo, agregadas por data do ponto de contato ou data de conversão.

### Encontrar o esquema no Snowflake

Usando as credenciais fornecidas, faça logon no Snowflake. Clique na guia **Planilhas** no canto superior esquerdo da navegação principal e navegue até o diretório do banco de dados no painel esquerdo.

![Planilhas e navegação](./images/download-scores/edited_snowflake_1.png)

Em seguida, clique em **Selecionar Esquema** no canto superior direito da tela. Na janela exibida, confirme se o banco de dados correto está selecionado. Em seguida, clique na lista suspensa *Schema* e selecione um dos seus esquemas listados. Você pode consultar diretamente das tabelas de pontuação listadas no schema selecionado.

![localizar um esquema](./images/download-scores/edited_snowflake_2.png)

## Conexão do Power BI ao Snowflake (opcional)

Suas credenciais do Snowflake podem ser usadas para configurar uma conexão entre os bancos de dados do Power BI Desktop e do Snowflake.

Primeiro, na caixa *Servidor*, digite o URL do Snowflake. Em seguida, em *Warehouse*, digite &quot;XSMALL&quot;. Em seguida, digite seu nome de usuário e senha.

![exemplo do POWERBI](./images/download-scores/powerbi-snowflake.png)

Depois que a conexão for estabelecida, selecione o banco de dados do Snowflake e selecione o schema apropriado. Agora você pode carregar todas as tabelas.
