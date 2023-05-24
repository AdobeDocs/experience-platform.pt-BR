---
description: Saiba como usar o Destination SDK para configurar um destino de Zona de aterrissagem de dados (DLZ) com opções de formatação de arquivo personalizadas e configuração de nome de arquivo personalizado.
title: Configure um destino de Zona de aterrissagem de dados (DLZ) com opções de formatação de arquivo personalizadas e configuração de nome de arquivo personalizado.
exl-id: 3a5c1188-c2b5-4e81-ae41-9fff797f08a6
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# Configurar um [!DNL Data Landing Zone (DLZ)] destino com opções personalizadas de formatação de arquivo e configuração personalizada de nome de arquivo

## Visão geral {#overview}

Esta página descreve como usar o Destination SDK para configurar um [!DNL Data Landing Zone] destino com personalizado [opções de formatação de arquivo](configure-file-formatting-options.md) e um personalizado [configuração do nome do arquivo](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration).

Esta página mostra todas as opções de configuração disponíveis para o [!DNL Data Landing Zone] destinos. Você pode editar as configurações mostradas nas etapas abaixo ou excluir determinadas partes das configurações, conforme necessário.

Para obter descrições detalhadas dos parâmetros usados abaixo, consulte [opções de configuração no SDK de destinos](../../functionality/configuration-options.md).

## Pré-requisitos {#prerequisites}

Antes de seguir para as etapas descritas abaixo, leia o [introdução ao Destination SDK](../../getting-started.md) página para obter informações sobre como obter as credenciais de autenticação de Adobe I/O e outros pré-requisitos necessários para trabalhar com as APIs de Destination SDK.

## Etapa 1: criar uma configuração de servidor e arquivo {#create-server-file-configuration}

Comece usando o `/destination-server` endpoint para [criar uma configuração de servidor e arquivo](../../authoring-api/destination-server/create-destination-server.md).

**Formato da API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitação**

A solicitação a seguir cria uma nova configuração do servidor de destino, configurada pelos parâmetros fornecidos na carga.
A carga abaixo inclui uma [!DNL Data Landing Zone] configuração, com personalização [Formatação de arquivo CSV](../../functionality/destination-server/file-formatting.md) parâmetros de configuração que os usuários podem definir na interface do usuário do Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
 -d '
{
   "name":"DLZ Destination Server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "fileConfigurations":{
         "compression":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.compression}}"
         },
         "fileType":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.fileType}}"
         },
         "csvOptions":{
            "sep":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.sep}}"
            },
            "encoding":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.encoding}}"
            },
            "quote":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quote}}"
            },
            "quoteAll":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quoteAll}}"
            },
            "escape":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escape}}"
            },
            "escapeQuotes":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escapeQuotes}}"
            },
            "header":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.header}}"
            },
            "ignoreLeadingWhiteSpace":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.ignoreLeadingWhiteSpace}}"
            },
            "nullValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.nullValue}}"
            },
            "dateFormat":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            },
            "charToEscapeQuoteEscaping":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.charToEscapeQuoteEscaping}}"
            },
            "emptyValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            }
         }
      }
   }
}'
```

Uma resposta bem-sucedida retorna a nova configuração do servidor de destino, incluindo o identificador exclusivo (`instanceId`) da configuração. Armazene esse valor conforme necessário na próxima etapa.

## Etapa 2: Criar configuração de destino {#create-destination-configuration}

Depois de criar o servidor de destino e a configuração de formatação de arquivo na etapa anterior, você pode usar o `/destinations` Endpoint da API para criar uma configuração de destino.

Para conectar a configuração do servidor no [etapa 1](#create-server-file-configuration) para essa configuração de destino, substitua o `destinationServerId` na solicitação de API abaixo com o valor obtido ao criar o servidor de destino no [etapa 1](#create-server-file-configuration).

**Formato da API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ Destination",
   "description":"SSD DLZ Destination",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
       
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"path",
         "title":"Folder path",
         "description":"Enter the path to your Data Landing Zone folder",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"File type",
         "description":"Select the exported file type.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.io/apis/experienceplatform.html",
      "category":"DLZ",
      "connectionType":"Server-to-server",
      "frequency":"Batch",
      "flowRunsSupported":true,
      "monitoringSupported":true
   },
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"NONE",
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "identityRequired":true,
      "segmentRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "autoSelectJoinKeyOnPartnerSchemaSelection":false,
      "joinKeyTitle":"DEDUPLICATION KEY",
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportModes":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_12_HOURS",
         "EVERY_8_HOURS",
         "ONCE",
         "EVERY_HOUR"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
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
      },
      "allowDedupKeyFieldSelection":true
   },
   "backfillHistoricalProfileData":true
}'
```

Uma resposta bem-sucedida retorna a nova configuração de destino, incluindo o identificador exclusivo (`instanceId`) da configuração. Armazene esse valor como ele é necessário se você precisar fazer mais solicitações HTTP para atualizar sua configuração de destino.

## Etapa 3: verificar a interface do usuário do Experience Platform {#verify-ui}

Com base nas configurações acima, o catálogo de Experience Platform agora exibirá um novo cartão de destino privado para você usar.

![Gravação de tela mostrando a página do catálogo de destinos com um cartão de destino selecionado.](../../assets/guides/batch/dlz-destination-card.gif)

Nas imagens e gravações abaixo, observe como as opções na variável [fluxo de trabalho de ativação para destinos baseados em arquivo](../../../ui/activate-batch-profile-destinations.md) corresponder às opções selecionadas na configuração de destino.

Ao preencher detalhes sobre o destino, observe como os campos exibidos são os campos de dados personalizados configurados na configuração do.

>[!TIP]
>
>A ordem em que você adiciona os campos de dados personalizados à configuração de destino não é refletida na interface do usuário do. Os campos de dados personalizados são sempre exibidos na ordem exibida na gravação de tela abaixo.

![preencher detalhes do destino](../../assets/guides/batch/file-configuration-options.gif)

Ao programar intervalos de exportação, observe como os campos exibidos são os campos configurados no `batchConfig` configuração.
![exportar opções de agendamento](../../assets/guides/batch/file-export-scheduling.png)

Ao visualizar as opções de configuração do nome de arquivo, observe como os campos exibidos representam os `filenameConfig` que você configura na configuração do.
![opções de configuração do nome do arquivo](../../assets/guides/batch/file-naming-options.gif)

Se quiser ajustar qualquer um dos campos mencionados acima, repita [etapas um](#create-server-file-configuration) e [dois](#create-destination-configuration) para modificar as configurações de acordo com suas necessidades.

## Etapa 4: (opcional) publicar seu destino {#publish-destination}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Após configurar seu destino, use o [API de publicação de destino](../../publishing-api/create-publishing-request.md) para enviar sua configuração ao Adobe para revisão.

## Etapa 5: (opcional) documentar seu destino {#document-destination}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Se você for um ISV (Independent Software Vendor, Fornecedor independente de software) ou um SI (System Integrator, integrador de sistemas), crie um [integração produtiva](../../overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](../../docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para seu destino na [catálogo de destinos Experience Platform](../../../catalog/overview.md).

## Próximas etapas {#next-steps}

Ao ler este artigo, agora você sabe como criar um [!DNL Data Landing Zone] destino usando Destination SDK. Em seguida, sua equipe pode usar o [fluxo de trabalho de ativação para destinos baseados em arquivo](../../../ui/activate-batch-profile-destinations.md) para exportar dados para o destino.
