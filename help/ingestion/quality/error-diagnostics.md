---
keywords: Experience Platform;página inicial;tópicos populares;assimilação em lote;Assimilação em lote;Assimilação parcial;Assimilação parcial;Recuperar erro;recuperar erro;Assimilação parcial em lote;Assimilação parcial em lote;assimilação parcial;Assimilação;diagnóstico de erro;recuperar diagnóstico de erro;obter diagnóstico de erro;obter erro;obter erros;recuperar erros;
solution: Experience Platform
title: Recuperação de diagnóstico de erro de assimilação de dados
description: Este documento fornece informações sobre monitoramento da assimilação em lote, gerenciamento de erros parciais de assimilação em lote, bem como uma referência para tipos parciais de assimilação em lote.
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 3%

---

# Recuperando diagnóstico de erro de assimilação de dados

O Adobe Experience Platform fornece dois métodos para fazer upload e assimilar dados. Você pode usar a assimilação em lote, que permite inserir dados usando vários tipos de arquivos (como CSVs), ou a assimilação por streaming, que permite inserir os dados no [!DNL Platform] usar endpoints de transmissão em tempo real.

Este documento fornece informações sobre monitoramento da assimilação em lote, gerenciamento de erros parciais de assimilação em lote, bem como uma referência para tipos parciais de assimilação em lote.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): os métodos pelos quais os dados podem ser enviados para o [!DNL Experience Platform].

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo as que pertencem à [!DNL Schema Registry], são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Baixando diagnóstico de erro {#download-diagnostics}

O Adobe Experience Platform permite que os usuários baixem os diagnósticos de erro dos arquivos de entrada. Os diagnósticos serão retidos em [!DNL Platform] por até 30 dias.

### Listar arquivos de entrada {#list-files}

A solicitação a seguir recupera uma lista de todos os arquivos fornecidos em um lote finalizado.

**Formato da API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você está procurando. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

### Recuperar diagnósticos do arquivo de entrada {#retrieve-diagnostics}

Depois de recuperar uma lista de todos os diferentes arquivos de entrada, você pode recuperar o diagnóstico do arquivo individual usando a solicitação a seguir.

**Formato da API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você está procurando. |
| `{FILE}` | O nome do arquivo que você está acessando. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retornará objetos JSON que contêm `path` objetos detalhando onde os diagnósticos foram salvos. A resposta retornará a mensagem `path` objetos em [Linhas JSON](https://jsonlines.readthedocs.io/en/latest/) formato.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recuperar erros de assimilação em lote {#retrieve-errors}

Se os lotes contiverem falhas, você deverá recuperar as informações de erro sobre essas falhas para poder assimilar os dados novamente.

### Verificar status {#check-status}

Para verificar o status do lote assimilado, você deve fornecer a ID do lote no caminho de uma solicitação GET. Para saber mais sobre como usar esta chamada de API, leia o [guia de endpoint de catálogo](../../catalog/api/list-objects.md).

**Formato da API**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A variável `id` valor do lote do qual você deseja verificar o status. |
| `{FILTER}` | Um parâmetro de consulta usado para filtrar os resultados retornados na resposta. Vários parâmetros são separados por &quot;E&quot; comercial (`&`). Para obter mais informações, leia o guia em [filtragem de dados do catálogo](../../catalog/api/filter-data.md). |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta sem erros**

Uma resposta bem-sucedida é retornada com informações detalhadas sobre o status do lote.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | O número de linhas que não puderam ser processadas devido a análise, conversão ou validação. Esse valor pode ser derivado subtraindo o `inputRecordCount` do `outputRecordCount`. Esse valor é gerado em todos os lotes, independentemente se `errorDiagnostics` está ativado. |

**Resposta com erros**

Se o lote tiver um ou mais erros e tiver o diagnóstico de erros ativado, a resposta retornará mais informações sobre os erros, tanto na própria carga quanto em um arquivo de erros que pode ser baixado. Observe que o status de um lote que contém erros ainda pode ter um status de sucesso.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | O número de linhas que não puderam ser processadas devido a análise, conversão ou validação. Esse valor pode ser derivado subtraindo o `inputRecordCount` do `outputRecordCount`. Esse valor é gerado em todos os lotes, independentemente se `errorDiagnostics` está ativado. |
| `errors.recordCount` | O número de linhas que falharam para o código de erro especificado. Este valor é **somente** gerado se `errorDiagnostics` está ativado. |

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
>```

## Próximas etapas {#next-steps}

Este tutorial abordou como monitorar erros de assimilação parcial de lotes. Para obter mais informações sobre assimilação em lote, leia a [guia do desenvolvedor de assimilação em lote](../batch-ingestion/api-overview.md).

## Apêndice {#appendix}

Esta seção fornece informações adicionais sobre tipos de erro de assimilação.

### Tipos de erro de assimilação parcial de lote {#partial-ingestion-types}

A assimilação parcial de lotes tem três tipos de erro diferentes ao assimilar dados:

- [Arquivos ilegíveis](#unreadable)
- [Esquemas ou cabeçalhos inválidos](#schemas-headers)
- [Linhas não analisáveis](#unparsable)

### Arquivos ilegíveis {#unreadable}

Se o lote assimilado tiver arquivos ilegíveis, os erros do lote serão anexados ao próprio lote. Mais informações sobre como recuperar o lote com falha podem ser encontradas no [guia de recuperação de lotes com falha](../quality/retrieve-failed-batches.md).

### Esquemas ou cabeçalhos inválidos {#schemas-headers}

Se o lote assimilado tiver um esquema inválido ou cabeçalhos inválidos, os erros do lote serão anexados ao próprio lote. Mais informações sobre como recuperar o lote com falha podem ser encontradas no [guia de recuperação de lotes com falha](../quality/retrieve-failed-batches.md).

### Linhas não analisáveis {#unparsable}

Se o lote assimilado tiver linhas não analisáveis, você poderá usar a solicitação a seguir para exibir uma lista de arquivos que contêm erros.

**Formato da API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | A variável `id` valor do lote do qual você está recuperando informações de erro. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista dos arquivos com erros.

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

Você pode recuperar informações detalhadas sobre os erros usando o [endpoint de recuperação de diagnóstico](#retrieve-diagnostics).

Uma resposta de amostra da recuperação do arquivo de erro pode ser vista abaixo:

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
