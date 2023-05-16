---
description: Esta página lista e descreve as etapas para configurar um destino baseado em arquivo usando o Destination SDK.
title: Use o Destination SDK para configurar um destino baseado em arquivo
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# Use o Destination SDK para configurar um destino baseado em arquivo

## Visão geral {#overview}

Esta página descreve como usar as informações em [Opções de configuração no SDK de destinos](../functionality/configuration-options.md) e em outros documentos de referência de API e funcionalidade do Destination SDK para configurar um [destino baseado em arquivo](../../destination-types.md#file-based). As etapas são apresentadas na ordem sequencial abaixo.

## Pré-requisitos {#prerequisites}

Antes de avançar para as etapas ilustradas abaixo, leia o [Introdução ao Destination SDK](../getting-started.md) para obter informações sobre como obter as credenciais de autenticação do Adobe I/O e outros pré-requisitos necessários para funcionar com as APIs do Destination SDK.

## Etapas para usar as opções de configuração no Destination SDK para configurar o destino {#steps}

![Etapas ilustradas do uso de pontos de extremidade de Destination SDK](../assets/guides/destination-sdk-steps-batch.png)

## Etapa 1: Criar um servidor e uma configuração de arquivo {#create-server-file-configuration}

Comece por [criação de uma configuração de servidor e arquivo](../authoring-api/destination-server/create-destination-server.md) usando o `/destinations-server` endpoint .

Veja abaixo um exemplo de configuração para um [!DNL Amazon S3] destino. Para configurar outros tipos de destinos com base em arquivos, consulte os [configurações do servidor](../functionality/destination-server/server-specs.md).

**Formato da API**

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucketName": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
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
            }
        }
    }
}
```

## Etapa 2: Criar configuração de destino {#create-destination-configuration}

Veja abaixo um exemplo de uma configuração de destino, criada usando o `/destinations` Ponto de extremidade da API.

Para conectar a configuração do servidor e do arquivo na etapa 1 a essa configuração de destino, adicione a ID da instância da configuração do servidor e do modelo como `destinationServerId` aqui.

**Formato da API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="84"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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

Para alguns destinos, o Destination SDK requer a configuração de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo de forma programática no destino. Consulte [Gerenciamento de metadados do público-alvo](../functionality/audience-metadata-management.md) para obter informações sobre quando você precisa configurar essa configuração e como fazer isso.

Se você usar uma configuração de metadados de público-alvo, é necessário conectá-los à configuração de destino criada na etapa 2. Adicione a ID da instância da configuração de metadados do público-alvo à configuração de destino como `audienceTemplateId`.

```json {line-numbers="true" highlight="91"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
    "audienceMetadataConfig":{
    "mapExperiencePlatformSegmentName":false,
    "mapExperiencePlatformSegmentId":false,
    "mapUserInput":false,
    "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
    },   
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

## Etapa 4: Configurar autenticação {#set-up-authentication}

Dependendo de você especificar `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` na configuração de destino acima, você pode configurar a autenticação para seu destino usando o `/destination` ou `/credentials` endpoint .

* Se você selecionou `"authenticationRule": "CUSTOMER_AUTHENTICATION"` na configuração de destino, consulte as seguintes seções para os tipos de autenticação suportados pelo Destination SDK para destinos baseados em arquivos:

   * [Autenticação Amazon S3](../functionality/destination-configuration/customer-authentication.md#s3)
   * [Azure Blob](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Armazenamento Azure Data Lake](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Armazenamento em nuvem Google](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [Autenticação SFTP com chave SSH](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [Autenticação SFTP com senha](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* Se você selecionou `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulte o [documentação da API da configuração de credenciais](../credentials-api/create-credential-configuration.md#when-to-use).


## Etapa 5: Teste seu destino {#test-destination}

Depois de configurar seu destino usando os endpoints de configuração nas etapas anteriores, você pode usar a variável [ferramenta de teste de destino](../testing-api/batch-destinations/file-based-destination-testing-overview.md) para testar a integração entre o Adobe Experience Platform e seu destino.

Como parte do processo para testar seu destino, você deve usar a interface do usuário do Experience Platform para criar segmentos, que você ativará no seu destino. Consulte os dois recursos abaixo para obter instruções sobre como criar segmentos no Experience Platform:

* [Criar uma página de documentação do segmento](/help/segmentation/ui/overview.md#create-segment)
* [Criar uma apresentação de vídeo de segmento](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Etapa 6: Publicar o destino {#publish-destination}

>[!NOTE]
>
>Essa etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para outros clientes usarem.

Após configurar e testar seu destino, use o [API de publicação de destino](../publishing-api/create-publishing-request.md) para enviar sua configuração ao Adobe para revisão.

## Etapa 7: Documente seu destino {#document-destination}

>[!NOTE]
>
>Essa etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para outros clientes usarem.

Se você for um Fornecedor Independente de Software (ISV) ou um Integrador de Sistema (SI) criando um [integração produzida](../overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](../docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para seu destino no [Catálogo de destinos Experience Platform](/help/destinations/catalog/overview.md).

## Etapa 8: Enviar destino para revisão do Adobe {#submit-for-review}

>[!NOTE]
>
>Essa etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para outros clientes usarem.

Finalmente, o destino pode ser publicado no catálogo de Experience Platform e visível para todos os clientes do Experience Platform, é necessário enviar oficialmente o destino para revisão do Adobe. Encontre informações completas sobre como [enviar para análise um destino produzido criado no Destination SDK](../guides/submit-destination.md).
