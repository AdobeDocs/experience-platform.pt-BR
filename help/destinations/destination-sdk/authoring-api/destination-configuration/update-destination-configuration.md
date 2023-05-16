---
description: Esta página exemplifica a chamada da API usada para atualizar uma configuração de destino existente por meio do Adobe Experience Platform Destination SDK.
title: Atualizar uma configuração de destino
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 2%

---


# Atualizar uma configuração de destino

Esta página exemplifica a solicitação da API e a carga útil que você pode usar para atualizar uma configuração de destino existente, usando o `/authoring/destinations` Ponto de extremidade da API.

>[!TIP]
>
>Qualquer operação de atualização em destinos produzidos/públicos é visível somente após o uso da variável [API de publicação](../../publishing-api/create-publishing-request.md) e envie a atualização para revisão do Adobe.

Para obter uma descrição detalhada dos recursos de uma configuração de destino, leia os seguintes artigos:

* [Configuração de autenticação do cliente](../../functionality/destination-configuration/customer-authentication.md)
* [Autenticação OAuth2](../../functionality/destination-configuration/oauth2-authentication.md)
* [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md)
* [Atributos da interface do usuário](../../functionality/destination-configuration/ui-attributes.md)
* [Configuração do esquema](../../functionality/destination-configuration/schema-configuration.md)
* [Configuração do namespace de identidade](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Delivery de destino](../../functionality/destination-configuration/destination-delivery.md)
* [Configuração de metadados de público-alvo](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configuração de metadados de público-alvo](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Política de agregação](../../functionality/destination-configuration/aggregation-policy.md)
* [Configuração em lote](../../functionality/destination-configuration/batch-configuration.md)
* [Qualificações de perfil histórico](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações da API de configuração de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Atualizar uma configuração de destino {#update}

Você pode atualizar um [existente](create-destination-configuration.md) configuração de destino, fazendo uma `PUT` à `/authoring/destinations` endpoint com a carga útil atualizada.

>[!TIP]
>
>Ponto de acesso da API: `platform.adobe.io/data/core/activation/authoring/destinations`

Para obter uma configuração de destino existente e sua correspondente `{INSTANCE_ID}`, consulte o artigo sobre [recuperar uma configuração de destino](retrieve-destination-configuration.md).

**Formato da API**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de destino que você deseja atualizar. Para obter uma configuração de destino existente e sua correspondente `{INSTANCE_ID}`, consulte [Recuperar uma configuração de destino](retrieve-destination-configuration.md). |

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

## Tratamento de erros da API {#error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, agora você sabe como atualizar uma configuração de destino por meio do Destination SDK `/authoring/destinations` Ponto de extremidade da API.

Para saber mais sobre o que você pode fazer com esse terminal, consulte os seguintes artigos:

* [Criar uma configuração de destino](create-destination-configuration.md)
* [Recuperar uma configuração de destino](retrieve-destination-configuration.md)
* [Excluir uma configuração de destino](delete-destination-configuration.md)