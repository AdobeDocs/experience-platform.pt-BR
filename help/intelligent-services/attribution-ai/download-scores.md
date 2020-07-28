---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: Acessar pontuações no Attribution AI
topic: Accessing scores
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 2%

---


# Download de pontuações no Attribution AI

Este documento serve como guia para o download das pontuações do Attribution AI.

## Introdução

O Attribution AI permite baixar pontuações no formato de arquivo de parquet. Este tutorial requer que você tenha lido e concluído o download da seção de pontuações do Attribution AI no guia de [introdução](./getting-started.md) .

Além disso, para acessar as pontuações do Attribution AI, é necessário ter uma instância de serviço com um status de execução bem-sucedida disponível. Para criar uma nova instância de serviço, visite o guia [do usuário do](./user-guide.md)Attribution AI. Se você criou recentemente uma instância de serviço e ela ainda está treinando e marcando, aguarde 24 horas para terminar a execução.

## Find your dataset ID {#dataset-id}

Na instância de serviço para obter insights de Attribution AI, clique na lista suspensa *Mais ações* na navegação superior direita e selecione Pontuações **[!UICONTROL de]** acesso.

![mais ações](./images/download-scores/more-actions.png)

Uma nova caixa de diálogo é exibida, contendo um link para a documentação das pontuações de download e a ID do conjunto de dados da sua instância atual. Copie a ID do conjunto de dados para a área de transferência e prossiga para a próxima etapa.

![ID do conjunto de dados](../customer-ai/images/download-scores/access-scores.png)

## Recuperar a ID do lote {#retrieve-your-batch-id}

Usando a ID do conjunto de dados da etapa anterior, é necessário fazer uma chamada para a API de catálogo para recuperar uma ID de lote. Parâmetros de query adicionais são usados para esta chamada de API a fim de retornar o lote bem-sucedido mais recente em vez de uma lista de lotes pertencentes à sua organização. Para retornar lotes adicionais, aumente o número do parâmetro do `limit` query para a quantia desejada que você deseja que seja retornada. Para obter mais informações sobre os tipos de parâmetros de query disponíveis, visite o guia sobre como [filtrar dados do catálogo usando parâmetros](../../catalog/api/filter-data.md)de query.

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

Uma resposta bem-sucedida retorna uma carga contendo um objeto de ID de lote. Neste exemplo, o valor Chave para o objeto retornado é a ID do lote `01E5QSWCAASFQ054FNBKYV6TIQ`. Copie a ID do lote para usar na próxima chamada da API.

>[!NOTE]
> A resposta a seguir fez com que o `tags` objeto fosse reformado para leitura.

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
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
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
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
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
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Verifique se você está no diretório ou pasta corretos na qual deseja salvar o arquivo antes de fazer a solicitação de GET.

**Resposta**

A resposta baixa o arquivo solicitado no diretório atual. Neste exemplo, o nome do arquivo é &quot;file.parquet&quot;.

![Terminal](./images/download-scores/terminal-output.png)

## Próximas etapas

Este documento descreveu as etapas necessárias para o download das pontuações dos Attribution AI. Agora você pode continuar navegando pelos outros serviços [e guias](../home.md) inteligentes oferecidos.

## Acessar pontuações usando o Snowflake

>[!IMPORTANT]
>
>Entre em contato com attributionai-support@adobe.com para obter mais detalhes sobre como acessar as pontuações usando o Snowflake.

Você pode acessar as pontuações de Attribution AI agregadas através do Snowflake. Atualmente, você precisa enviar o suporte para o Adobe por email em attributionai-support@adobe.com para configurar e receber as credenciais da sua conta de leitor para o Snowflake.

Depois que o suporte ao Adobe tiver processado sua solicitação, você receberá um URL para a conta do leitor como Snowflake e as credenciais correspondentes abaixo:

- Snowflake URL
- Nome do usuário
- Password

>[!NOTE]
>
>A conta do leitor é para consultar os dados usando clientes sql, planilhas e soluções BI que suportam o conector JDBC.

Depois de ter suas credenciais e URL, você pode query as tabelas de modelo, agregadas por data do ponto de contato ou data de conversão.

### Encontrar seu schema no Snowflake

Usando as credenciais fornecidas, faça logon no Snowflake. Clique na guia **Planilhas** na navegação principal superior esquerda e navegue até o diretório do banco de dados no painel esquerdo.

![Planilhas e navegação](./images/download-scores/edited_snowflake_1.png)

Em seguida, clique em **Selecionar Schema** no canto superior direito da tela. Na janela que aparece, confirme se você tem o banco de dados certo selecionado. Em seguida, clique na lista suspensa *Schema* e selecione um dos schemas listados. Você pode query diretamente das tabelas de pontuação listadas abaixo do schema selecionado.

![localizar um schema](./images/download-scores/edited_snowflake_2.png)

## Conectando o PowerBI ao Snowflake (opcional)

Suas credenciais de Snowflake podem ser usadas para configurar uma conexão entre os bancos de dados PowerBI Desktop e Snowflake.

Primeiro, na caixa *Servidor* , digite o URL do Snowflake. Em seguida, em *Warehouse*, digite &quot;XSMALL&quot;. Em seguida, digite seu nome de usuário e senha.

![exemplo de POWERBI](./images/download-scores/powerbi-snowflake.png)

Depois que a conexão for estabelecida, selecione seu banco de dados de Snowflake e, em seguida, selecione o schema apropriado. Agora você pode carregar todas as tabelas.
