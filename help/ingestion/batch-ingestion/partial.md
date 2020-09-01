---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;
solution: Experience Platform
title: Visão geral da ingestão parcial de lote Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 1%

---



# Ingestão parcial em lote

A ingestão parcial em lote é a capacidade de assimilar dados que contenham erros, até um certo limite. Com esse recurso, os usuários podem assimilar com êxito todos os seus dados corretos no Adobe Experience Platform enquanto todos os dados incorretos são armazenados separadamente em lote, juntamente com detalhes sobre o motivo pelo qual são inválidos.

Este documento fornece um tutorial para gerenciar a ingestão parcial em lote.

Além disso, o [apêndice](#appendix) a este tutorial fornece uma referência para tipos de erro de ingestão em lote parcial.

## Introdução

Este tutorial requer um conhecimento prático dos vários serviços da Adobe Experience Platform envolvidos com a ingestão parcial de lote. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Ingestão](./overview.md)em lote: O método que [!DNL Platform] ingere e armazena dados de arquivos de dados, como CSV e Parquet.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para [!DNL Platform] APIs.

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

## Habilitar um lote para ingestão parcial em lote na API {#enable-api}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para ingestão parcial em lote usando a API. Para obter instruções sobre como usar a interface do usuário, leia a etapa [ativar um lote para a ingestão parcial em lote na UI](#enable-ui) .

Você pode criar um novo lote com a ingestão parcial ativada.

Para criar um novo lote, siga as etapas no guia [do desenvolvedor da ingestão em](./api-overview.md)lote. Depois de atingir a etapa **[!UICONTROL Criar lote]** , adicione o seguinte campo no corpo da solicitação:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `enableErrorDiagnostics` | Um sinalizador que permite [!DNL Platform] gerar mensagens de erro detalhadas sobre o lote. |
| `partialIngestionPercentage` | A porcentagem de erros aceitáveis antes que todo o lote falhe. Assim, neste exemplo, um máximo de 5% do lote pode ser de erros, antes que falhe. |


## Habilitar um lote para ingestão parcial em lote na interface do usuário {#enable-ui}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para ingestão parcial em lote usando a interface do usuário. Se você já tiver ativado um lote para a ingestão parcial por lote usando a API, poderá pular para a próxima seção.

Para habilitar um lote para ingestão parcial por meio da [!DNL Platform] interface do usuário, você pode criar um novo lote por meio de conexões de origem, criar um novo lote em um conjunto de dados existente ou criar um novo lote por meio do &quot;Fluxo[!UICONTROL do]mapa CSV para XDM&quot;.

### Criar uma nova conexão de origem {#new-source}

Para criar uma nova conexão de origem, siga as etapas listadas na visão geral [](../../sources/home.md)Fontes. Depois de atingir a etapa de detalhes **[!UICONTROL do]** Dataflow, anote os campos de ingestão **** parcial e diagnóstico **[!UICONTROL de]** erro.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

A alternância de ingestão **** parcial permite ativar ou desativar o uso da ingestão em lote parcial.

A alternância do diagnóstico **** Error só é exibida quando a alternância de ingestão **** parcial está desativada. Esse recurso permite [!DNL Platform] gerar mensagens de erro detalhadas sobre os lotes ingeridos. Se a alternância de ingestão **** parcial estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

O limite **[!UICONTROL de]** Erro permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

### Usar um conjunto de dados existente {#existing-dataset}

Para usar um conjunto de dados existente, selecione um start selecionando um conjunto de dados. A barra lateral à direita é preenchida com informações sobre o conjunto de dados.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

A alternância de ingestão **** parcial permite ativar ou desativar o uso da ingestão em lote parcial.

A alternância do diagnóstico **** Error só é exibida quando a alternância de ingestão **** parcial está desativada. Esse recurso permite [!DNL Platform] gerar mensagens de erro detalhadas sobre os lotes ingeridos. Se a alternância de ingestão **** parcial estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

O limite **[!UICONTROL de]** Erro permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

Agora, você pode fazer upload de dados usando o botão **Adicionar dados** e eles serão ingeridos com a ingestão parcial.

### Usar o fluxo &quot;[!UICONTROL Mapear CSV para o schema]XDM&quot; {#map-flow}

Para usar o fluxo &quot;[!UICONTROL Mapear CSV para o schema]XDM&quot;, siga as etapas listadas no tutorial [](../tutorials/map-a-csv-file.md)Mapear um arquivo CSV. Depois de atingir a etapa **[!UICONTROL Adicionar dados]** , anote os campos **[!UICONTROL Inclusão]** parcial e Diagnóstico **[!UICONTROL de]** erro.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

A alternância de ingestão **** parcial permite ativar ou desativar o uso da ingestão em lote parcial.

A alternância do diagnóstico **** Error só é exibida quando a alternância de ingestão **** parcial está desativada. Esse recurso permite [!DNL Platform] gerar mensagens de erro detalhadas sobre os lotes ingeridos. Se a alternância de ingestão **** parcial estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

O limite **[!UICONTROL de]** Erro permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

## Download de metadados em nível de arquivo {#download-metadata}

A Adobe Experience Platform permite que os usuários baixem os metadados dos arquivos de entrada. Os metadados serão retidos dentro [!DNL Platform] de até 30 dias.

### arquivos de entrada de lista {#list-files}

A solicitação a seguir permitirá que você visualização uma lista de todos os arquivos fornecidos em um lote finalizado.

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retornará o status HTTP 200 com objetos JSON contendo objetos de caminho detalhando onde os metadados foram salvos.

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Recuperar metadados do arquivo de entrada {#retrieve-metadata}

Depois de recuperar uma lista de todos os arquivos de entrada diferentes, você pode recuperar os metadados do arquivo individual usando o terminal a seguir.

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retornará o status HTTP 200 com objetos JSON contendo objetos de caminho detalhando onde os metadados foram salvos.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recuperar erros de ingestão em lote parcial {#retrieve-errors}

Se os lotes contiverem falhas, será necessário recuperar informações de erro sobre essas falhas para que você possa assimilar os dados novamente.

### Verificar status {#check-status}

Para verificar o status do lote ingerido, forneça a ID do lote no caminho de uma solicitação de GET.

**Formato da API**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | O `id` valor do lote do qual você deseja verificar o status. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta sem erros**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o status do lote.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `metrics.failedRecordCount` | O número de linhas que não puderam ser processadas devido à análise, conversão ou validação. Esse valor pode ser derivado subtraindo o valor `inputRecordCount` do `outputRecordCount`. Esse valor será gerado em todos os lotes independentemente de `errorDiagnostics` estar ativado. |

**Resposta com erros**

Se o lote tiver um ou mais erros e o diagnóstico de erros estiver ativado, o status terá mais informações `success` sobre os erros fornecidos na resposta e em um arquivo de erro que pode ser baixado.

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `metrics.failedRecordCount` | O número de linhas que não puderam ser processadas devido à análise, conversão ou validação. Esse valor pode ser derivado subtraindo o valor `inputRecordCount` do `outputRecordCount`. Esse valor será gerado em todos os lotes independentemente de `errorDiagnostics` estar ativado. |
| `errors.recordCount` | O número de linhas que falharam no código de erro especificado. Esse valor **só** será gerado se `errorDiagnostics` estiver ativado. |

>[!NOTE]
>
>Se o diagnóstico de erro não estiver disponível, a seguinte mensagem de erro será exibida:
> 
```json
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## Próximas etapas {#next-steps}

Este tutorial aborda como criar ou modificar um conjunto de dados para permitir a ingestão parcial em lote. Para mais informações sobre a ingestão por lote, leia o guia [do desenvolvedor da ingestão por](./api-overview.md)lote.

## Tipos de erro de ingestão parcial em lote {#appendix}

A ingestão parcial em lote tem três tipos de erro diferentes ao assimilar dados.

- [Arquivos ilegíveis](#unreadable)
- [Schemas ou cabeçalhos inválidos](#schemas-headers)
- [Linhas não analisáveis](#unparsable)

### Arquivos ilegíveis {#unreadable}

Se o lote ingerido tiver arquivos ilegíveis, os erros do lote serão anexados ao próprio lote. Mais informações sobre como recuperar o lote com falha podem ser encontradas no guia [](../quality/retrieve-failed-batches.md)recuperar lotes com falha.

### Schemas ou cabeçalhos inválidos {#schemas-headers}

Se o lote ingerido tiver um schema inválido ou cabeçalhos inválidos, os erros do lote serão anexados ao próprio lote. Mais informações sobre como recuperar o lote com falha podem ser encontradas no guia [](../quality/retrieve-failed-batches.md)recuperar lotes com falha.

### Linhas não analisáveis {#unparsable}

Se o lote que você ingeriu tiver linhas não analisáveis, você poderá usar o terminal a seguir para visualização de uma lista de arquivos que contêm erros.

**Formato da API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | O `id` valor do lote do qual você está recuperando informações de erro. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista dos arquivos que possuem erros.

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Em seguida, você pode recuperar informações detalhadas sobre os erros usando o terminal [de recuperação de](#retrieve-metadata)metadados.

Uma amostra de resposta da recuperação do arquivo de erro pode ser vista abaixo:

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
