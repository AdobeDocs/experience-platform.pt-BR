---
description: Esta página lista e descreve as etapas para configurar um destino baseado em arquivo usando o Destination SDK.
title: Usar o Destination SDK para configurar um destino baseado em arquivo
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# Usar o Destination SDK para configurar um destino baseado em arquivo

## Visão geral {#overview}

Esta página descreve como usar as informações em [Opções de configuração no SDK de Destinos](../functionality/configuration-options.md) e em outras funcionalidades do Destination SDK e documentos de referência de API para configurar um [destino baseado em arquivo](../../destination-types.md#file-based). As etapas são apresentadas em ordem sequencial abaixo.

## Pré-requisitos {#prerequisites}

Antes de seguir para as etapas ilustradas abaixo, leia a página [Introdução ao Destination SDK](../getting-started.md) para obter informações sobre como obter as credenciais de autenticação do Adobe I/O necessárias e outros pré-requisitos para trabalhar com as APIs do Destination SDK.

## Etapas para usar as opções de configuração no Destination SDK para definir seu destino {#steps}

![Etapas ilustradas do uso de pontos de extremidade do Destination SDK](../assets/guides/destination-sdk-steps-batch.png)

## Etapa 1: criar uma configuração de servidor e arquivo {#create-server-file-configuration}

Comece [criando uma configuração de servidor e arquivo](../authoring-api/destination-server/create-destination-server.md) usando o ponto de extremidade `/destinations-server`.

Veja abaixo um exemplo de configuração para um destino [!DNL Amazon S3]. Para obter mais detalhes sobre os campos usados na configuração e para configurar outros tipos de destinos baseados em arquivos, consulte suas [configurações de servidor](../functionality/destination-server/server-specs.md) correspondentes.

**Formato da API**

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
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

Veja abaixo um exemplo de uma configuração de destino, criada usando o ponto de extremidade da API `/destinations`.

Para conectar o servidor e a configuração de arquivo da etapa 1 a esta configuração de destino, adicione o `instance ID` da configuração de servidor e arquivo como `destinationServerId` aqui.

**Formato da API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="83"}
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
        "documentationLink": "https://www.adobe.com/go/destinations-YOURDESTINATION-en",
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
        "defaultStartTime": "00:00",
       "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      }
    },
    "backfillHistoricalProfileData": true
}
```

## Etapa 3: criar configuração de metadados de público {#create-audience-metadata-configuration}

Para alguns destinos, o Destination SDK exige a definição de uma configuração de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo no destino de forma programática. Consulte [Gerenciamento de metadados de público-alvo](../functionality/audience-metadata-management.md) para obter informações sobre quando e como definir essa configuração.

Se você usar uma configuração de metadados de público, deverá conectá-la à configuração de destino criada na etapa 2. Adicione a ID da instância da configuração de metadados de público-alvo à configuração de destino como `audienceTemplateId`.

```json {line-numbers="true" highlight="90"}
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
        "documentationLink": "http://www.adobe.com/go/destinations-YOURDESTINATION-en",
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
    "segmentMappingConfig":{
        "mapExperiencePlatformSegmentName":false,
        "mapExperiencePlatformSegmentId":false,
        "mapUserInput":false
    },
    "audienceMetadataConfig":{
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
        "defaultStartTime": "00:00",
       "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      }
    },
    "backfillHistoricalProfileData": true
}
```

## Etapa 4: configurar autenticação {#set-up-authentication}

Se você especificar `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` na configuração de destino acima, poderá configurar a autenticação para o seu destino usando o ponto de extremidade `/destination` ou `/credentials`.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` é a mais comum das duas regras de autenticação e é a que deve ser usada se você exigir que os usuários forneçam alguma forma de autenticação para o seu destino antes que eles possam configurar uma conexão e exportar dados.

* Se você selecionou `"authenticationRule": "CUSTOMER_AUTHENTICATION"` na configuração de destino, consulte as seguintes seções para obter os tipos de autenticação aceitos pelo Destination SDK para destinos baseados em arquivo:

   * [Autenticação Amazon S3](../functionality/destination-configuration/customer-authentication.md#s3)
   * [Azure Blob](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Armazenamento Azure Data Lake](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Google Cloud Storage](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [Autenticação SFTP com chave SSH](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [Autenticação SFTP com senha](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* Se você selecionou `"authenticationRule": "PLATFORM_AUTHENTICATION"`, deve criar uma [configuração de credenciais](../credentials-api/create-credential-configuration.md) e passar a ID do objeto de credencial no parâmetro `authenticationId` na configuração de [entrega de destino](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication).

## Etapa 5: testar o destino {#test-destination}

Depois de configurar seu destino usando os pontos de extremidade de configuração nas etapas anteriores, você pode usar a [ferramenta de teste de destino](../testing-api/batch-destinations/file-based-destination-testing-overview.md) para testar a integração entre o Adobe Experience Platform e seu destino.

Como parte do processo para testar o destino, é necessário usar a interface do usuário do Experience Platform para criar públicos-alvo, que você ativará para o destino. Consulte os dois recursos abaixo para obter instruções sobre como criar públicos-alvo no Experience Platform:

* [Criar um público-alvo: página de documentação](/help/segmentation/ui/audience-portal.md#create-audience)
* [Criar um público-alvo - apresentação em vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## Etapa 6: publicar seu destino {#publish-destination}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Depois de configurar e testar o destino, use a [API de publicação de destino](../publishing-api/create-publishing-request.md) para enviar a configuração à Adobe para revisão.

## Etapa 7: documentar seu destino {#document-destination}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Se você for um ISV (Fornecedor Independente de Software) ou um SI (Integrador de Sistemas) criando uma [integração de produtos](../overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](../docs-framework/documentation-instructions.md) para criar uma página de documentação de produto para seu destino no [catálogo de destinos do Experience Platform](/help/destinations/catalog/overview.md).

## Etapa 8: enviar destino para revisão da Adobe {#submit-for-review}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Por fim, antes que o destino possa ser publicado no catálogo do Experience Platform e ser visível a todos os clientes do Experience Platform, é necessário enviar oficialmente o destino para a revisão da Adobe. Encontre informações completas sobre como [enviar para revisão um destino produzido criado no Destination SDK](../guides/submit-destination.md).
