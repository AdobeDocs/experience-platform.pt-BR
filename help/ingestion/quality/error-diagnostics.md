---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;error diagnostics;retrieve error diagnostics;get error diagnostics;get error;get errors;retrieve errors;
solution: Experience Platform
title: Visão geral da ingestão parcial de lote Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: a345efca3c38c3077c89b47271f54b924d58db45
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 2%

---


# Recuperando diagnósticos de erro

A Adobe Experience Platform fornece dois métodos para fazer upload e ingestão de dados. Você pode usar a ingestão em lote, que permite inserir dados usando vários tipos de arquivos (como CSVs), ou a assimilação em streaming, que permite inserir seus dados para [!DNL Platform] usar pontos de extremidade de streaming em tempo real.

Este documento fornece informações sobre como monitorar a ingestão em lote, gerenciar erros de ingestão em lote parcial, bem como uma referência para tipos de ingestão em lote parcial.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

- [Sistema do [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!Ingestão de Dados Adobe Experience Platform DNL]](../home.md): Os métodos pelos quais os dados podem ser enviados [!DNL Experience Platform].

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos no [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Schema Registry], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

## Download do diagnóstico de erros {#download-diagnostics}

A Adobe Experience Platform permite que os usuários baixem o diagnóstico de erro dos arquivos de entrada. O diagnóstico será retido dentro de 30 dias [!DNL Platform] no máximo.

### arquivos de entrada de lista {#list-files}

A solicitação a seguir recupera uma lista de todos os arquivos fornecidos em um lote finalizado.

**Formato da API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você está pesquisando. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retornará objetos JSON detalhando onde os diagnósticos foram salvos.

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Recuperar diagnósticos de arquivos de entrada {#retrieve-diagnostics}

Depois de recuperar uma lista de todos os arquivos de entrada diferentes, você pode recuperar o diagnóstico do arquivo individual usando a solicitação a seguir.

**Formato da API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você está pesquisando. |
| `{FILE}` | O nome do arquivo que você está acessando. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retornará objetos JSON que contêm `path` objetos detalhando onde os diagnósticos foram salvos. A resposta retornará os `path` objetos no formato Linhas [](https://jsonlines.org/) JSON.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recuperar erros de ingestão em lote {#retrieve-errors}

Se os lotes contiverem falhas, você deverá recuperar informações de erro sobre essas falhas para que possa assimilar os dados novamente.

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
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta sem erros**

Uma resposta bem-sucedida retorna com informações detalhadas sobre o status do lote.

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
| `metrics.failedRecordCount` | O número de linhas que não puderam ser processadas devido à análise, conversão ou validação. Esse valor pode ser derivado subtraindo o valor `inputRecordCount` do `outputRecordCount`. Esse valor é gerado em todos os lotes, independentemente de `errorDiagnostics` estar ativado. |

**Resposta com erros**

Se o lote tiver um ou mais erros e o diagnóstico de erros estiver ativado, a resposta retornará mais informações sobre os erros, tanto na própria carga quanto em um arquivo de erro que pode ser baixado. Observe que o status de um lote que contém erros pode ainda ter um status de sucesso.

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
| `metrics.failedRecordCount` | O número de linhas que não puderam ser processadas devido à análise, conversão ou validação. Esse valor pode ser derivado subtraindo o valor `inputRecordCount` do `outputRecordCount`. Esse valor é gerado em todos os lotes, independentemente de `errorDiagnostics` estar ativado. |
| `errors.recordCount` | O número de linhas que falharam no código de erro especificado. Esse valor **só** será gerado se `errorDiagnostics` estiver ativado. |

>[!NOTE]
>
>Se o diagnóstico de erro não estiver disponível, a seguinte mensagem de erro será exibida:
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
> ```

## Tipos de erro de ingestão parcial em lote {#appendix}

A ingestão parcial em lote tem três tipos de erro diferentes ao assimilar dados:

- [Arquivos ilegíveis](#unreadable)
- [Schemas ou cabeçalhos inválidos](#schemas-headers)
- [Linhas não analisáveis](#unparsable)

### Arquivos ilegíveis {#unreadable}

Se o lote ingerido tiver arquivos ilegíveis, os erros do lote serão anexados ao próprio lote. Mais informações sobre como recuperar o lote com falha podem ser encontradas no guia [](../quality/retrieve-failed-batches.md)recuperar lotes com falha.

### Schemas ou cabeçalhos inválidos {#schemas-headers}

Se o lote ingerido tiver um schema inválido ou cabeçalhos inválidos, os erros do lote serão anexados ao próprio lote. Mais informações sobre como recuperar o lote com falha podem ser encontradas no guia [](../quality/retrieve-failed-batches.md)recuperar lotes com falha.

### Linhas não analisáveis {#unparsable}

Se o lote que você ingeriu tiver linhas não analisáveis, você poderá usar a seguinte solicitação para visualização de uma lista de arquivos que contêm erros.

**Formato da API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | O `id` valor do lote do qual você está recuperando informações de erro. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista dos arquivos que possuem erros.

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

Em seguida, você pode recuperar informações detalhadas sobre os erros usando o terminal [de recuperação de](#retrieve-diagnostics)diagnósticos.

Uma amostra de resposta da recuperação do arquivo de erro pode ser vista abaixo:

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```

## Próximas etapas {#next-steps}

Este tutorial aborda como monitorar erros de ingestão em lote parcial. Para mais informações sobre a ingestão por lote, leia o guia [do desenvolvedor da ingestão por](../batch-ingestion/api-overview.md)lote.