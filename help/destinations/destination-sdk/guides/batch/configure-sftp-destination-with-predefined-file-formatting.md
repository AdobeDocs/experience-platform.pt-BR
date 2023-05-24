---
description: Saiba como usar o Destination SDK para configurar um destino SFTP com opções predefinidas de formatação de arquivo e configuração de nome de arquivo personalizado.
title: Configure um destino SFTP com opções predefinidas de formatação de arquivo e configuração de nome de arquivo personalizado.
exl-id: 6e0fe019-7fbb-48e4-9469-6cc7fc3cb6e4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 1%

---

# Configure um destino SFTP com opções predefinidas de formatação de arquivo e configuração de nome de arquivo personalizado

## Visão geral {#overview}

Esta página descreve como usar o Destination SDK para configurar um destino SFTP com conexões predefinidas [opções de formatação de arquivo](configure-file-formatting-options.md) e um personalizado [configuração do nome do arquivo](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration).

Esta página mostra todas as opções de configuração disponíveis para destinos SFTP. Você pode editar as configurações mostradas nas etapas abaixo ou excluir determinadas partes das configurações, conforme necessário.

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
A carga abaixo inclui uma configuração SFTP genérica, com configurações padrão predefinidas [Formatação de arquivo CSV](../../functionality/destination-server/file-formatting.md) parâmetros de configuração que os usuários podem definir na interface do usuário do Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "SFTP destination with predefined CSV formatting options",
    "destinationServerType": "FILE_BASED_SFTP",
    "fileBasedSFTPDestination": {
        "hostname": {
            "templatingStrategy": "NONE",
            "value": "{{customerData.hostname}}"
        },
        "rootDirectory": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.remotePath}}"
        },
        "port": 22
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
   "name":"SFTP destination with predefined CSV formatting options",
   "description":"SFTP destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      },
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"remotePath",
         "title":"Root directory",
         "description":"Enter root directory",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"hostname",
         "title":"Hostname",
         "description":"Enter hostname",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-sftp-en",
      "category":"SFTP",
      "connectionType":"SFTP",
      "monitoringSupported":true,
      "flowRunsSupported":true,
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
         "destinationServerId":"{{instanceID of your destination server}}"
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

Uma resposta bem-sucedida retorna a nova configuração de destino, incluindo o identificador exclusivo (`instanceId`) da configuração. Armazene esse valor como ele é necessário se você precisar fazer mais solicitações HTTP para atualizar sua configuração de destino.

## Etapa 3: verificar a interface do usuário do Experience Platform {#verify-ui}

Com base nas configurações acima, o catálogo de Experience Platform agora exibirá um novo cartão de destino privado para você usar.

![Gravação de tela mostrando a página do catálogo de destinos com um cartão de destino selecionado.](../../assets/guides/batch/destination-card.gif)

Nas imagens e gravações abaixo, observe como as opções na variável [fluxo de trabalho de ativação para destinos baseados em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md) corresponder às opções selecionadas na configuração de destino.

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

Após a leitura deste artigo, agora você sabe como criar um destino SFTP personalizado usando o Destination SDK. Em seguida, sua equipe pode usar o [fluxo de trabalho de ativação para destinos baseados em arquivo](../../../ui/activate-batch-profile-destinations.md) para exportar dados para o destino.
