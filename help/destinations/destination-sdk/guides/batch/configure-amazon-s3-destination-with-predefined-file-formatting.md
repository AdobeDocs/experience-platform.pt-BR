---
description: Saiba como usar o Destination SDK para configurar um destino Amazon S3 com opções predefinidas de formatação de arquivo e configuração personalizada de nome de arquivo.
title: Configure um destino Amazon S3 com opções predefinidas de formatação de arquivo e configuração personalizada de nome de arquivo.
exl-id: 0ecd3575-dcda-4e5c-af5c-247d4ea13fa1
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# Configure um [!DNL Amazon S3] destino com opções de formatação de arquivo predefinidas e configuração de nome de arquivo personalizado

## Visão geral {#overview}

>[!IMPORTANT]
>
>A funcionalidade para configurar destinos com base em arquivos usando o Adobe Experience Platform Destination SDK está atualmente em Beta. A documentação e a funcionalidade estão sujeitas a alterações.

Esta página descreve como usar o Destination SDK para configurar um destino Amazon S3 com predefinido e padrão [opções de formatação de arquivo](../../server-and-file-configuration.md#file-configuration) e um [configuração do nome do arquivo](../../file-based-destination-configuration.md#file-name-configuration).

Esta página mostra todas as opções de configuração disponíveis para [!DNL Amazon S3] destinos. Você pode editar as configurações mostradas nas etapas abaixo ou excluir determinadas partes das configurações, conforme necessário.

## Pré-requisitos {#prerequisites}

Antes de seguir para as etapas descritas abaixo, leia o [Introdução ao Destination SDK](../../getting-started.md) para obter informações sobre como obter as credenciais de autenticação do Adobe I/O e outros pré-requisitos necessários para funcionar com as APIs do Destination SDK.

## Etapa 1: Criar um servidor e uma configuração de arquivo {#create-server-file-configuration}

Comece usando o `/destination-server` endpoint para criar uma configuração de servidor e arquivo. Para obter descrições detalhadas dos parâmetros na solicitação HTTP, leia o [especificações de configuração de servidor e arquivo para destinos com base em arquivo](../../server-and-file-configuration.md#s3-example) e o [configurações de formatação de arquivo](../../server-and-file-configuration.md#file-configuration).

**Formato da API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Solicitação**

A solicitação a seguir cria uma nova configuração de servidor de destino, configurada pelos parâmetros fornecidos no payload.
A carga abaixo inclui um [!DNL Amazon S3] configuração, com predefinido, padrão [Formatação de arquivo CSV](../../server-and-file-configuration.md#file-configuration) parâmetros de configuração que os usuários podem definir na interface do usuário do Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "Amazon S3 destination server with predefined default CSV options",
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
            }
        }
    }
}'
```

Uma resposta bem-sucedida retorna a nova configuração do servidor de destino, incluindo o identificador exclusivo (`instanceId`) da configuração. Armazene esse valor conforme for necessário na próxima etapa.

## Etapa 2: Criar configuração de destino {#create-destination-configuration}

Depois de criar a configuração do servidor de destino e da formatação de arquivos na etapa anterior, agora é possível usar o `/destinations` Ponto de extremidade da API para criar uma configuração de destino.

Para conectar a configuração do servidor em [etapa 1](#create-server-file-configuration) para essa configuração de destino, substitua o `destinationServerId` na solicitação de API abaixo com a variável `instanceId` valor obtido ao criar o servidor de destino em [etapa 1](#create-server-file-configuration).

Para obter descrições detalhadas dos parâmetros usados abaixo, consulte as seguintes páginas:

* [Configuração de autenticação](../../authentication-configuration.md#s3)
* [Configuração de destino em lote](../../file-based-destination-configuration.md#batch-configuration)
* [Operações da API de configuração de destino com base em arquivo](../../destination-configuration-api.md#create-file-based)

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
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "releaseNotes":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
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
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
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
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
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
      "backfillHistoricalProfileData":true
   }
}'
```

Uma resposta bem-sucedida retorna a nova configuração de destino, incluindo o identificador exclusivo (`instanceId`) da configuração. Armazene esse valor como é necessário se você precisar fazer mais solicitações HTTP para atualizar a configuração de destino.

## Etapa 3: Verificar a interface do usuário do Experience Platform {#verify-ui}

Com base nas configurações acima, o catálogo de Experience Platform agora exibirá uma nova placa de destino privada para você usar.

![Gravação de tela mostrando a página de catálogo de destinos com um cartão de destino selecionado.](../../assets/destination-card.gif)

Nas imagens e gravações abaixo, observe como as opções no [fluxo de trabalho de ativação para destinos com base em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md) corresponda às opções selecionadas na configuração de destino.

Ao preencher os detalhes sobre o destino, observe como os campos são revelados são os campos de dados personalizados que você configurou na configuração.

>[!TIP]
>
>A ordem na qual você adiciona os campos de dados personalizados à configuração de destino não é refletida na interface do usuário. Os campos de dados do cliente são sempre exibidos na ordem exibida na gravação de tela abaixo.

![Gravação de tela mostrando os campos de dados do cliente definidos em sua configuração.](../../assets/file-configuration-options.gif)

Ao agendar intervalos de exportação, observe como os campos são revelados nos campos que você configurou na `batchConfig` configuração.
![opções de agendamento de exportação](../../assets/file-export-scheduling.png)

Ao visualizar as opções de configuração do nome de arquivo, observe como os campos surdos representam a variável `filenameConfig` opções configuradas na configuração.
![opções de configuração do nome do arquivo](../../assets/file-naming-options.gif)

Se quiser ajustar qualquer um dos campos mencionados acima, repita [passo um](#create-server-file-configuration) e [two](#create-destination-configuration) para modificar as configurações de acordo com suas necessidades.

## Etapa 4: (Opcional) Publicar o destino {#publish-destination}

>[!NOTE]
>
>Essa etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para outros clientes usarem.

Após configurar seu destino, use a variável [API de publicação de destino](../../destination-publish-api.md) para enviar sua configuração ao Adobe para revisão.

## Etapa 5: (Opcional) Documente seu destino {#document-destination}

>[!NOTE]
>
>Essa etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para outros clientes usarem.

Se você for um Fornecedor Independente de Software (ISV) ou um Integrador de Sistema (SI) criando um [integração produzida](../../overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](../../docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para seu destino no [Catálogo de destinos Experience Platform](../../../catalog/overview.md).

## Próximas etapas {#next-steps}

Ao ler este artigo, agora você sabe criar um [!DNL Amazon S3] ao usar Destination SDK. Em seguida, sua equipe pode usar o [fluxo de trabalho de ativação para destinos com base em arquivo](../../../ui/activate-batch-profile-destinations.md) para exportar dados para o destino.
