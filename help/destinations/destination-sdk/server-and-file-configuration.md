---
description: As especificações de configuração do servidor e do arquivo para destinos baseados em arquivo podem ser configuradas no Adobe Experience Platform Destination SDK por meio do endpoint /destination-servers.
title: Opções de configuração para especificações do servidor de destino baseado em arquivo
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 8%

---

# Configuração de servidor e arquivo para especificações do servidor de destino baseado em arquivo

## Visão geral {#overview}

Esta página detalha todas as opções de configuração do servidor para seus servidores de destino baseados em arquivos e mostra como definir várias opções de configuração de arquivo para usuários que exportam arquivos do Experience Platform para o seu destino.

As especificações de configuração do servidor e do arquivo para destinos baseados em arquivo podem ser configuradas no Adobe Experience Platform Destination SDK por meio de `/destination-servers` terminal. Ler [Operações de ponto de extremidade da API do servidor de destino](./destination-server-api.md) para obter uma lista completa de operações que podem ser executadas no endpoint.

As seções abaixo incluem especificações do servidor de destino específicas para cada tipo de destino de lote suportado no Destination SDK.

## Especificação do servidor de destino Amazon S3 baseada em arquivo {#s3-example}

O exemplo abaixo mostra uma configuração correta do servidor de destino para um destino Amazon S3.

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Amazon S3], defina como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | String | O nome do [!DNL Amazon S3] bucket a ser usado por esse destino. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuração da formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

{style="table-layout:auto"}

## Especificação do servidor de destino SFTP baseado em arquivo {#sftp-example}

O exemplo abaixo mostra uma configuração correta do servidor de destino para um destino SFTP.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL SFTP] destinos, defina como `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | String | O diretório raiz do armazenamento de destino. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | String | O nome do host do armazenamento de destino. |
| `port` | Número inteiro | A porta do servidor de arquivos SFTP. |
| `encryptionMode` | String | Indica se deve ser usada criptografia de arquivo. Valores compatíveis: <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | Objeto | Consulte [configuração da formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

{style="table-layout:auto"}

## Baseado em arquivo [!DNL Azure Data Lake Storage] ([!DNL ADLS]) especificação do servidor de destino {#adls-example}

O exemplo abaixo mostra uma configuração correta do servidor de destino para um [!DNL Azure Data Lake Storage] destino.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, defina como `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuração da formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

{style="table-layout:auto"}

## Baseado em arquivo [!DNL Azure Blob Storage] especificação do servidor de destino {#blob-example}

O exemplo abaixo mostra uma configuração correta do servidor de destino para um [!DNL Azure Blob Storage] destino.

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Azure Blob Storage] destinos, defina como `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | String | O nome do [!DNL Azure Blob Storage] contêiner a ser usado por este destino. |
| `fileConfigurations` | Objeto | Consulte [configuração da formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

{style="table-layout:auto"}

## Baseado em arquivo [!DNL Data Landing Zone] ([!DNL DLZ]) especificação do servidor de destino {#dlz-example}

O exemplo abaixo mostra uma configuração correta do servidor de destino para um [!DNL Data Landing Zone] ([!DNL DLZ]) destino.

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Data Landing Zone] destinos, defina como `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Obrigatório.*  Use `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuração da formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

{style="table-layout:auto"}

## Baseado em arquivo [!DNL Google Cloud Storage] especificação do servidor de destino {#gcs-example}

O exemplo abaixo mostra uma configuração correta do servidor de destino para um [!DNL Google Cloud Storage] destino.

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      // See the file formatting configuration section further below on this page
   }
}
```

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `name` | String | O nome da conexão de destino. |
| `destinationServerType` | String | Defina esse valor de acordo com sua plataforma de destino. Para [!DNL Google Cloud Storage] destinos, defina como `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Obrigatório.*  Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | O nome do [!DNL Google Cloud Storage] bucket a ser usado por esse destino. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuração da formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

{style="table-layout:auto"}

## Configuração da formatação de arquivo {#file-configuration}

Esta seção descreve as configurações de formatação de arquivo para o `CSV` arquivos. Você pode modificar várias propriedades dos arquivos exportados para corresponder aos requisitos do sistema de recebimento de arquivos do seu lado, a fim de ler e interpretar de maneira ideal os arquivos recebidos do Experience Platform.

>[!NOTE]
>
>As opções de CSV são suportadas somente ao exportar arquivos CSV. A variável `fileConfigurations` A seção não é obrigatória ao configurar um novo servidor de destino. Se você não passar nenhum valor na chamada de API para as opções de CSV, os padrões da variável [tabela de referência mais abaixo](#file-formatting-reference-and-example) serão usados.

### Configurações de arquivo com opções CSV e a variável `templatingStrategy` definir como `NONE` {#file-configuration-templating-none}

No exemplo de configuração abaixo, todas as opções de CSV são corrigidas. As configurações de exportação definidas em cada um dos `csvOptions` Os parâmetros são finais e os usuários não podem modificá-los.

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

### Configurações de arquivo com opções CSV e a variável `templatingStrategy` definir como `PEBBLE_V1` {#file-configuration-templating-pebble}

No exemplo de configuração abaixo, nenhuma das opções de CSV é fixa. A variável `value` em cada um dos `csvOptions` parâmetros é configurado em um campo de dados do cliente correspondente por meio da `/destinations` terminal (por exemplo `customerData.quote` para o `quote` opção de formatação de arquivo) e os usuários podem usar a interface do usuário do Experience Platform para selecionar entre as várias opções configuradas no campo de dados do cliente correspondente.

```json
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
```

### Referência completa e exemplos de opções de formatação de arquivo compatíveis {#file-formatting-reference-and-example}

>[!TIP]
>
>As opções de formatação de arquivo CSV descritas abaixo também estão documentadas na [Guia do Apache Spark para arquivos CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). As descrições usadas abaixo foram tiradas do guia do Apache Spark.

Abaixo está uma referência completa de todas as opções de formatação de arquivo disponíveis em Destination SDK, juntamente com exemplos de saída para cada opção.

| Campo | Obrigatório / Opcional | Descrição | Valor padrão | Exemplo de saída 1 | Exemplo de saída 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Obrigatório | Para cada opção de formatação de arquivo configurada, é necessário adicionar o parâmetro `templatingStrategy`, que pode ter dois valores: <br><ul><li>`NONE`: use esse valor se não estiver planejando permitir que os usuários selecionem entre valores diferentes para uma configuração. Consulte [esta configuração](#file-configuration-templating-none) por exemplo, onde as opções de formatação de arquivo são corrigidas.</li><li>`PEBBLE_V1`: use esse valor se quiser permitir que os usuários selecionem entre valores diferentes para uma configuração. Nesse caso, você também deve configurar um campo de dados do cliente correspondente no `/destination` Configuração do endpoint, para exibir as várias opções aos usuários na interface do usuário. Consulte [esta configuração](#file-configuration-templating-pebble) para obter um exemplo em que os usuários podem selecionar entre valores diferentes para opções de formatação de arquivo.</li></ul> | - | - | - |
| `compression.value` | Opcional | Codec de compactação a ser usado ao salvar dados no arquivo. Valores compatíveis: `none`, `bzip2`, `gzip`, `lz4`, e `snappy`. | `none` | - | - |
| `fileType.value` | Opcional | Especifica o formato do arquivo de saída. Valores compatíveis: `csv`, `parquet`, e `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um caractere único usado para sair de valores entre aspas onde o separador pode ser parte do valor. | `null` | - | - |
| `csvOptions.quoteAll.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se todos os valores devem sempre estar entre aspas. O padrão é omitir apenas valores que contenham um caractere de aspas. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um separador para cada campo e valor. Esse separador pode conter um ou mais caracteres. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um caractere único usado para fazer o escape de aspas dentro de um valor já citado. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os valores contendo aspas devem sempre estar entre aspas. O padrão é omitir todos os valores que contenham um caractere de aspas. | `true` | - | - |
| `csvOptions.header.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os nomes das colunas devem ser gravados como a primeira linha no arquivo exportado. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os espaços em branco à esquerda devem ser aparados dos valores. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se espaços em branco à direita devem ser aparados de valores. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a representação da cadeia de caracteres de um valor nulo. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica o formato de data. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a cadeia de caracteres que indica um formato de carimbo de data e hora. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um único caractere usado para escapar do escape para o caractere de citação. | `\` quando os caracteres de escape e aspas são diferentes. `\0` quando os caracteres escape e aspas são iguais. | - | - |
| `csvOptions.emptyValue.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a representação da cadeia de caracteres de um valor vazio. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}