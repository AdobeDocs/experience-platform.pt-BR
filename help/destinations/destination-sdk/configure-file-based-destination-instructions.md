---
description: Esta página lista e descreve as etapas para configurar um destino baseado em arquivo usando o Destination SDK.
title: (Beta) Use o Destination SDK para configurar um destino baseado em arquivo
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# (Beta) Use o Destination SDK para configurar um destino baseado em arquivo

## Visão geral {#overview}

>[!IMPORTANT]
>
>A funcionalidade para configurar e enviar destinos baseados em arquivos usando o Adobe Experience Platform Destination SDK está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

Esta página descreve como usar as informações em [Opções de configuração no SDK de destinos](./configuration-options.md) e em outros documentos de referência de API e funcionalidade do Destination SDK para configurar um [destino baseado em arquivo](../../destinations/destination-types.md#file-based). As etapas são apresentadas na ordem sequencial abaixo.

## Pré-requisitos {#prerequisites}

Antes de avançar para as etapas ilustradas abaixo, leia o [Introdução ao Destination SDK](./getting-started.md) para obter informações sobre como obter as credenciais de autenticação do Adobe I/O e outros pré-requisitos necessários para funcionar com as APIs do Destination SDK.

## Etapas para usar as opções de configuração no Destination SDK para configurar o destino {#steps}

![Etapas ilustradas do uso de pontos de extremidade de Destination SDK](./assets/destination-sdk-steps-batch.png)

## Etapa 1: Criar um servidor e uma configuração de arquivo {#create-server-file-configuration}

Comece criando uma configuração de servidor e arquivo usando o `/destinations-server` endpoint (lido) [Referência da API](./destination-server-api.md)).

Veja abaixo um exemplo de configuração para um [!DNL Amazon S3] destino. Para configurar outros tipos de destinos com base em arquivos, consulte os [configurações do servidor](server-and-file-configuration.md).

**Formato da API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

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
        }
    }
}
```

## Etapa 2: Criar configuração de destino {#create-destination-configuration}

Veja abaixo um exemplo de uma configuração de destino, criada usando o `/destinations` Ponto de extremidade da API. Para obter mais informações sobre essa configuração, consulte [Configuração de destino](./file-based-destination-configuration.md).

Para conectar a configuração do servidor e do arquivo na etapa 1 a essa configuração de destino, adicione a ID da instância da configuração do servidor e do modelo como `destinationServerId` aqui.

**Formato da API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "releaseNotes": "Test",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucket",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[A-Za-z]+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
        "category": "S3",
        "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## Etapa 3: Criar configuração de metadados de público-alvo {#create-audience-metadata-configuration}

Para alguns destinos, o Destination SDK requer a configuração de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo de forma programática no destino. Consulte [Gerenciamento de metadados do público-alvo](./audience-metadata-management.md) para obter informações sobre quando você precisa configurar essa configuração e como fazer isso.

Se você usar uma configuração de metadados de público-alvo, é necessário conectá-los à configuração de destino criada na etapa 2. Adicione a ID da instância da configuração de metadados do público-alvo à configuração de destino como `audienceTemplateId`.

## Etapa 4: Configurar autenticação {#set-up-authentication}

Dependendo de você especificar `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` na configuração de destino acima, você pode configurar a autenticação para seu destino usando o `/destination` ou `/credentials` endpoint .

* Se você selecionou `"authenticationRule": "CUSTOMER_AUTHENTICATION"` na configuração de destino, consulte as seguintes seções para os tipos de autenticação suportados pelo Destination SDK para destinos baseados em arquivos:

   * [Autenticação Amazon S3](authentication-configuration.md#s3)
   * [Cadeia de conexão do Azure](authentication-configuration.md#blob)
   * [Principal do Serviço Azure](authentication-configuration.md#adls)
   * [Autenticação SFTP com chave SSH](authentication-configuration.md#sftp-ssh)
   * [Autenticação SFTP com senha](authentication-configuration.md#sftp-password)

* Se você selecionou `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulte o [Configuração de autenticação](./authentication-configuration.md#when-to-use).


<!-- ## Step 5: Test your destination {#test-destination}

After setting up your destination using the configuration endpoints in the previous steps, you can use the [destination testing tool](./create-template.md) to test the integration between Adobe Experience Platform and your destination.

As part of the process to test your destination, you must use the Experience Platform UI to create segments, which you will activate to your destination. Refer to the two resources below for instructions how to create segments in Experience Platform:

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Create a segment video walkthrough](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) -->

## Etapa 5: Publicar o destino {#publish-destination}

Após configurar e testar seu destino, use o [API de publicação de destino](./destination-publish-api.md) para enviar sua configuração ao Adobe para revisão.

## Etapa 6: Documente seu destino {#document-destination}

Se você for um Fornecedor Independente de Software (ISV) ou um Integrador de Sistema (SI) criando um [integração produzida](./overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](./docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para seu destino no [Catálogo de destinos Experience Platform](/help/destinations/catalog/overview.md).
