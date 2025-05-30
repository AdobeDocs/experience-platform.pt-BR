---
description: Saiba como configurar o tipo de público-alvo para seus destinos criados com o Destination SDK.
title: Configurar tipo de dados do público
exl-id: c56fb0f9-adb2-4fb2-ab06-c0398d828600
source-git-commit: 5d84ea1baa96c288d9d37606122e0a41880478b9
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 2%

---

# Configurar tipo de dados do público

Ao criar um conector de destino com o Destination SDK, você pode definir o tipo de público-alvo que será exportado para o seu destino. A configuração do tipo de dados de público correto garante que seu destino receba os dados certos para o caso de uso pretendido, seja para campanhas de marketing, estratégias baseadas em conta ou análise de dados.

Revise os tipos de dados de público abaixo para saber mais sobre as diferenças entre eles e identificar o tipo necessário para sua integração. Em seguida, leia as seções mais abaixo na página para saber como configurar seu destino para exportar diferentes tipos de público-alvo.

| Tipo de dados de público | Descrição | Casos de uso |
|---------|----------|---------|
| [Públicos-alvo](../../../../segmentation/types/people-audiences.md) | Com base nos perfis de clientes, permitindo direcionar grupos específicos de pessoas para campanhas de marketing. | Compradores frequentes, abandonadores de carrinho |
| [Públicos-alvo da conta](../../../../segmentation/types/account-audiences.md) | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](../../../../segmentation/types/prospect-audiences.md) | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](../../../../catalog/datasets/overview.md) | Coleções de dados estruturados armazenados no Data Lake do Adobe Experience Platform. | Relatórios, fluxos de trabalho de ciência de dados |

O tipo de dados de público-alvo compatível depende do tipo de destino que você cria.
Consulte a tabela abaixo para entender quais tipos de destino suportam quais tipos de dados de público-alvo.

| Tipo de destino | Públicos-alvo de pessoas | Públicos-alvo da conta | Públicos-alvo em potencial | Conjuntos de dados |
|---------|----------|---------|---------|---------|
| Transmissão | ✓ | ✓ | X | X |
| Baseado em arquivo | ✓ | ✓ | ✓ | ✓ |

{style="table-layout:auto"}

## A matriz `sources` {#sources}

A matriz `sources` especifica o tipo de dados de público-alvo ao qual o destino dá suporte. É necessário para públicos-alvo da conta, públicos-alvo potenciais e exportações de conjunto de dados, mas não é necessário para públicos-alvo de pessoas, pois são compatíveis por padrão.

```json
"sources":[
   "ACCOUNTS" // Specifies that this destination supports account audiences
]
```

A matriz `sources` aceita os seguintes valores:

* `"ACCOUNTS"`: especifica que seu destino dá suporte à exportação de públicos-alvo de conta.
* `"UNIFIED_PROFILE_PROSPECTS"`: especifica que seu destino dá suporte à exportação de públicos-alvo potenciais.
* `"DATASETS"`: especifica que seu destino dá suporte à exportação de conjuntos de dados.

Dependendo do tipo de público-alvo que você deseja exportar para seu destino, consulte as seções abaixo para obter exemplos de configuração de destino.

## Exportar públicos de pessoas {#people-audiences}

Por padrão, os públicos-alvo de pessoas têm suporte para todos os tipos de destino e não precisam de um valor `sources` específico. Para criar um destino que ofereça suporte a públicos-alvo de pessoas, você não precisa mais usar a matriz `sources`, pois esse é o comportamento padrão.

+++ Exemplo de configuração de destino de streaming com suporte a públicos-alvo de pessoas

Este é um exemplo de um destino de transmissão que exporta públicos de pessoas. Observe como não há matriz `sources` na configuração.&quot;

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

+++

## Exportar públicos-alvo da conta {#account}

Considere adicionar suporte de público-alvo da conta ao seu destino quando quiser configurar um destino [!DNL B2B] para marketing baseado em conta. Por exemplo, você pode usar públicos baseados em conta para recuperar registros de todas as contas que não tenham informações de contato para pessoas com o título [!DNL Chief Operating Officer (COO)] ou [!DNL Chief Marketing Officer (CMO)].

Para criar um destino compatível com a exportação de públicos-alvo de conta, adicione o trecho de configuração abaixo à sua [configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md).

```json
"sources":[
   "ACCOUNTS" // Specifies that this destination supports account audiences
] 
```

+++ Exemplo de configuração de destino de streaming com suporte a públicos-alvo de conta

```shell {line-numbers="true" highlight="12-14"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "sources":[
      "ACCOUNTS"
   ],
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

+++

## Exportar públicos-alvo de clientes potenciais {#prospect}

Considere adicionar suporte de público-alvo em potencial ao seu destino quando quiser direcionar indivíduos que ainda não são clientes, mas que compartilham características com seu público-alvo. Com perfis de prospecto, você pode complementar seus perfis de clientes com atributos de parceiros de terceiros confiáveis. Consulte este [caso de uso de prospecção](../../../../rtcdp/partner-data/prospecting.md) para obter mais informações.

Para criar um destino que ofereça suporte à exportação de públicos-alvo potenciais, adicione o trecho de configuração abaixo à sua [configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md).


```json
"sources":[
   "UNIFIED_PROFILE_PROSPECTS" // Specifies that this destination supports prospect audiences
] 
```

+++ Exemplo de configuração de destino de transmissão com suporte a públicos-alvo potenciais

```shell {line-numbers="true" highlight="12-14"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "sources":[
      "UNIFIED_PROFILE_PROSPECTS"
   ],
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
            "GZIP",
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
            "json",
            "parquet"
         ],
         "default":"parquet"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

+++

## Exportar conjuntos de dados {#datasets}

Considere adicionar o suporte à exportação do conjunto de dados ao seu destino quando estiver procurando exportar conjuntos de dados brutos, que não são agrupados ou estruturados por interesses ou qualificações de público-alvo. Você pode usar esses dados para relatórios, fluxos de trabalho de ciência de dados e muitos outros casos de uso. Por exemplo, como administrador, engenheiro de dados ou analista, você pode exportar dados da Experience Platform para sincronizar com o data warehouse, usar as ferramentas de análise do [!DNL BI], as ferramentas da nuvem externa [!DNL ML] ou armazenar no sistema para necessidades de armazenamento de longo prazo.

Para criar um destino compatível com a exportação de conjuntos de dados, adicione o trecho de configuração abaixo à sua [configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md).

```json
"sources":[
   "DATASETS" // Specifies that this destination supports dataset exports
]
```

+++ Exemplo de configuração de destino baseada em arquivo com suporte à exportação de conjunto de dados

```shell {line-numbers="true" highlight="12-14"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with dataset export capability",
   "description":"Amazon S3 destination with dataset export capability",
   "status":"TEST",
   "sources":[
      "DATASETS"
   ],
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
            "GZIP",
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
            "json",
            "parquet"
         ],
         "default":"parquet"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-dataset-export-en",
      "category":"cloudStorage",
      "frequency":"Batch",
      "monitoringSupported":true,
      "flowRunsSupported":true
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"19c8fc89-9b73-4e0f-893e-549410b23f39"
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT"
   },
   "destinationDelivery":[
      {
         "authenticationRule":"PLATFORM_AUTHENTICATION",
         "authenticationId":"2fff57e1-6603-4927-8a9c-147c90839bdb",
         "destinationServerId":"e59de90a-6df6-471a-bd55-11f7bdb52fae"
      }
   ],
   "inputSchemaId":"70d0bd4734cc49c98d48c4b162e9a1b7",
   "schemaConfig":{
      "useCustomerSchemaForAttributeMapping":false,
      "requiredMappingsOnly":false,
      "profileRequired":false,
      "segmentRequired":false,
      "identityRequired":false
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":false,
      "autoSelectJoinKeyOnPartnerSchemaSelection":false,
      "joinKeyTitle":"DEDUPLICATION KEY",
      "defaultExportMode":"FIRST_FULL_THEN_INCREMENTAL",
      "allowedExportModes":[
         
      ],
      "allowedScheduleFrequency":[
         
      ],
      "defaultFrequency":"EVERY_HOUR",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            
         ],
         "defaultFilenameAppendOptions":[
            
         ],
         "defaultFilename":""
      },
      "datasetBatchConfig":{
         "allowedFoldernameAppendOptions":[
            "DESTINATION",
            "DATASET_ID",
            "DATASET_NAME",
            "EXPORT_TIME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFoldernameAppendOptions":[
            "DATASET_ID",
            "EXPORT_TIME"
         ],
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
            "ONCE"
         ]
      },
      "allowDedupKeyFieldSelection":false
   },
   "maxProfileAttributes":9000,
   "maxIdentityAttributes":1000,
   "destConfigId":"069280b7-40fc-490c-85c4-3bcae17b5441",
   "backfillHistoricalProfileData":true
}
```

+++

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve entender melhor como configurar o tipo de dados do público-alvo para o seu destino.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Configuração de autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
