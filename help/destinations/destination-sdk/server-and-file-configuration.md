---
description: As especificações de configuração do servidor e do arquivo para destinos com base em arquivo podem ser configuradas no Adobe Experience Platform Destination SDK por meio do endpoint /destination-servers.
title: (Beta) Opções de configuração para especificações do servidor de destino baseado em arquivo
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 3c8ad296ab9f0ce62743466ca8823b13c4545a9d
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 10%

---

# (Beta) Configuração de servidor e arquivo para especificações do servidor de destino baseado em arquivo

## Visão geral {#overview}

>[!IMPORTANT]
>
>A funcionalidade para configurar e enviar destinos baseados em arquivos usando o Adobe Experience Platform Destination SDK está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

Esta página detalha todas as opções de configuração do servidor para seus servidores de destino baseados em arquivos e instrui como configurar várias opções de configuração de arquivo para os usuários que exportam arquivos do Experience Platform para seu destino.

As especificações de configuração do servidor e do arquivo para destinos com base em arquivo podem ser configuradas no Adobe Experience Platform Destination SDK por meio do `/destination-servers` endpoint . Ler [Operações de endpoint da API do servidor de destino](./destination-server-api.md) para obter uma lista completa de operações que podem ser realizadas no ponto de extremidade.

## Especificação do servidor de destino Amazon S3 baseado em arquivo {#s3-example}

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
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Amazon S3], defina como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | String | O nome do [!DNL Amazon S3] bucket a ser usado por este destino. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuração de formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

## Especificação do servidor de destino SFTP baseado em arquivo {#sftp-example}

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
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL SFTP] destinos, defina como `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | String | O diretório raiz do armazenamento de destino. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | String | O nome do host do armazenamento de destino. |
| `port` | Número inteiro | A porta do servidor de arquivos SFTP. |
| `encryptionMode` | String | Indica se deve ser utilizada a encriptação de ficheiros. Valores compatíveis: <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | Objeto | Consulte [configuração de formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

## Baseado em arquivo [!DNL Azure Data Lake Storage] ([!DNL ADLS]) especificação do servidor de destino {#adls-example}

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
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, defina como `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuração de formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

## Baseado em arquivo [!DNL Azure Blob Storage] especificação do servidor de destino {#blob-example}

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
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Azure Blob Storage] destinos, defina como `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | String | O nome do [!DNL Azure Blob Storage] contêiner a ser usado por este destino. |
| `fileConfigurations` | Objeto | Consulte [configuração de formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

## Baseado em arquivo [!DNL Data Landing Zone] ([!DNL DLZ]) especificação do servidor de destino {#dlz-example}

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
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Data Landing Zone] destinos, defina como `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Obrigatório.*  Use `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuração de formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

## Baseado em arquivo [!DNL Google Cloud Storage] especificação do servidor de destino {#gcs-example}

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
| `destinationServerType` | String | Defina esse valor de acordo com a plataforma de destino. Para [!DNL Google Cloud Storage] destinos, defina como `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Obrigatório.*  Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | O nome do [!DNL Google Cloud Storage] bucket a ser usado por este destino. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Obrigatório.* Use `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | O caminho para a pasta de destino que hospedará os arquivos exportados. |
| `fileConfigurations` | Objeto | Consulte [configuração de formatação de arquivo](#file-configuration) para obter explicações detalhadas sobre esta seção. |

## Configuração de formatação de arquivo {#file-configuration}

Esta seção descreve as configurações de formatação de arquivo para o arquivo exportado `CSV` arquivos. Você pode modificar várias propriedades dos arquivos exportados para corresponder aos requisitos do sistema de recepção de arquivos no seu lado, a fim de ler e interpretar de maneira ideal os arquivos recebidos do Experience Platform.

>[!NOTE]
>
>As opções CSV só são compatíveis ao exportar arquivos CSV. O `fileConfigurations` não é obrigatória ao configurar um novo servidor de destino. Se você não passar nenhum valor na chamada da API para as opções CSV, os valores padrão da tabela abaixo serão usados.

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
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        },
        "maxFileRowCount":5000000
    }
```

| Campo | Obrigatório / Opcional | Descrição | Valor padrão |
|---|---|---|---|
| `compression.value` | Opcional | Codec de compactação a ser usado ao salvar dados no arquivo. Valores compatíveis: `none`, `bzip2`, `gzip`, `lz4`e `snappy`. | `none` |
| `fileType.value` | Opcional | Especifica o formato do arquivo de saída. Valores compatíveis: `csv`, `parquet`e `json`. | `csv` |
| `csvOptions.quote.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um caractere único usado para escapar de valores entre aspas, onde o separador pode fazer parte do valor. | `null` |
| `csvOptions.quoteAll.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se todos os valores devem ser sempre entre aspas. O padrão é apenas valores de escape contendo um caractere de aspas. | `false` |
| `csvOptions.escape.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um caractere único usado para evitar aspas dentro de um valor já citado. | `\` |
| `csvOptions.escapeQuotes.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os valores que contêm aspas devem sempre ser entre aspas. O padrão é omitir todos os valores que contenham um caractere de aspas. | `true` |
| `csvOptions.header.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os nomes das colunas devem ser gravados como a primeira linha. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os espaços em branco à esquerda devem ser aparados a partir de valores. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica se os espaços em branco à direita devem ser aparados dos valores. | `true` |
| `csvOptions.nullValue.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a representação da string de um valor nulo. | `""` |
| `csvOptions.dateFormat.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Indica o formato de data. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a string que indica um formato de carimbo de data e hora. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define um único caractere usado para escapar do escape para o caractere de aspas. | `\` quando os caracteres de escape e aspas são diferentes. `\0` quando o caractere escape e aspas são iguais. |
| `csvOptions.emptyValue.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define a representação da string de um valor vazio. | `""` |
| `csvOptions.lineSep.value` | Opcional | *Somente para`"fileType.value": "csv"`*. Define o separador de linha que deve ser usado para gravação. O comprimento máximo é de 1 caractere. | `\n` |
| `maxFileRowCount` | Opcional | Número máximo de linhas que o arquivo exportado pode conter. Configure isso com base nos requisitos de tamanho do arquivo da plataforma de destino. | N/D |
