---
description: Esta página exemplifica a chamada à API usada para atualizar uma configuração de destino existente por meio do Adobe Experience Platform Destination SDK.
title: Atualizar uma configuração de destino
exl-id: d7f18689-9806-4f73-a63a-fa112569819c
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 3%

---

# Atualizar uma configuração de destino

Esta página exemplifica a solicitação de API e a carga que você pode usar para atualizar uma configuração de destino existente, usando o `/authoring/destinations` Endpoint da API.

>[!TIP]
>
>Qualquer operação de atualização em destinos de produção/públicos estará visível somente após o uso do [API de publicação](../../publishing-api/create-publishing-request.md) e envie a atualização para revisão do Adobe.

Para obter uma descrição detalhada dos recursos de uma configuração de destino, leia os seguintes artigos:

* [Configuração de autenticação do cliente](../../functionality/destination-configuration/customer-authentication.md)
* [Autorização OAuth2](../../functionality/destination-configuration/oauth2-authorization.md)
* [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md)
* [Atributos da interface](../../functionality/destination-configuration/ui-attributes.md)
* [Configuração do esquema](../../functionality/destination-configuration/schema-configuration.md)
* [Configuração do namespace de identidade](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Entrega de destino](../../functionality/destination-configuration/destination-delivery.md)
* [Configuração de metadados de público](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configuração de metadados de público](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Política de agregação](../../functionality/destination-configuration/aggregation-policy.md)
* [Configuração em lote](../../functionality/destination-configuration/batch-configuration.md)
* [Qualificações do perfil histórico](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API de configuração de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Atualizar uma configuração de destino {#update}

Você pode atualizar um [existente](create-destination-configuration.md) configuração de destino fazendo uma `PUT` solicitação à `/authoring/destinations` terminal com a carga atualizada.

>[!TIP]
>
>Ponto de acesso da API: `platform.adobe.io/data/core/activation/authoring/destinations`

Para obter uma configuração de destino existente e suas configurações `{INSTANCE_ID}`, consulte o artigo sobre [recuperação de uma configuração de destino](retrieve-destination-configuration.md).

**Formato da API**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de destino que você deseja atualizar. Para obter uma configuração de destino existente e suas configurações `{INSTANCE_ID}`, consulte [Recuperar uma configuração de destino](retrieve-destination-configuration.md). |

+++Solicitação

A solicitação a seguir atualiza o destino que criamos em [este exemplo](create-destination-configuration.md#create) com diferentes `filenameConfig` opções.

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com os detalhes da configuração de destino atualizada.

+++

## Manipulação de erros de API {#error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como atualizar uma configuração de destino por meio do Destination SDK `/authoring/destinations` Endpoint da API.

Para saber mais sobre o que você pode fazer com esse endpoint, consulte os seguintes artigos:

* [Criar uma configuração de destino](create-destination-configuration.md)
* [Recuperar uma configuração de destino](retrieve-destination-configuration.md)
* [Excluir uma configuração de destino](delete-destination-configuration.md)
