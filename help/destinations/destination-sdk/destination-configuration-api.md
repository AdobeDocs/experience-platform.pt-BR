---
description: Esta página lista e descreve todas as operações de API que você pode executar usando o endpoint da API `/authoring/destinations`.
title: Operações de endpoint da API de destinos
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '2539'
ht-degree: 4%

---

# Operações de API do endpoint de destinos {#destination-configuration}

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Esta página lista e descreve todas as operações de API que você pode executar usando o `/authoring/destinations` Endpoint da API. Para obter uma descrição da funcionalidade compatível com esse endpoint, leia [configuração de destino](./destination-configuration.md).

## Introdução às operações de API de destino {#get-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Criar configuração para um destino de streaming {#create}

Você pode criar uma nova configuração de destino fazendo uma solicitação POST para o `/authoring/destinations` terminal.

**Formato da API**

```http
POST /authoring/destinations
```

**Solicitação**

A solicitação a seguir cria uma nova configuração de destino de streaming, configurada pelos parâmetros fornecidos na carga. A carga abaixo inclui todos os parâmetros para destinos de transmissão aceitos pelo `/authoring/destinations` terminal. Observe que não é necessário adicionar todos os parâmetros na chamada e que o modelo é personalizável, de acordo com os requisitos da API.

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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Indica o título do destino no catálogo de Experience Platform |
| `description` | String | Forneça uma descrição que o Adobe usará no catálogo de destinos de Experience Platform para o cartão de destino. Mire não mais do que 4-5 frases. |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Uso `TEST` ao configurar seu destino pela primeira vez. |
| `customerAuthenticationConfigurations` | String | Indica a configuração usada para autenticar clientes do Experience Platform no servidor. Consulte `authType` abaixo para obter os valores aceitos. |
| `customerAuthenticationConfigurations.authType` | String | Os valores compatíveis para destinos de streaming são: <ul><li>`BASIC`</li><li>`BEARER`</li><li>`OAUTH2`</li></ul> Os valores compatíveis para destinos baseados em arquivo são: <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | String | Forneça um nome para o campo personalizado que você está introduzindo. |
| `customerDataFields.type` | String | Indica o tipo de campo personalizado que você está introduzindo. Os valores aceitos são `string`, `object`, `integer` |
| `customerDataFields.title` | String | Indica o nome do campo, como visto pelos clientes na interface do usuário do Experience Platform |
| `customerDataFields.description` | String | Forneça uma descrição para o campo personalizado. |
| `customerDataFields.isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. |
| `customerDataFields.enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `customerDataFields.pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para aplicar um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, insira `^[A-Za-z]+$` neste campo. |
| `uiAttributes.documentationLink` | String | Refere-se à página da documentação no [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para o seu destino. Uso `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `https://www.adobe.com/go/destinations-moviestar-en`. Observe que esse link funciona somente depois que o Adobe definir seu destino como ativo e a documentação for publicada. |
| `uiAttributes.category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de destino](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | String | `Server-to-server` O é a única opção disponível no momento. |
| `uiAttributes.frequency` | String | `Streaming` O é a única opção disponível no momento. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se os clientes podem mapear atributos de perfil padrão para a identidade que você está configurando. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se os clientes podem mapear identidades pertencentes a [namespaces personalizados](/help/identity-service/namespaces.md#manage-namespaces) à identidade que você está configurando. |
| `identityNamespaces.externalId.transformation` | String | _Não mostrado no exemplo de configuração_. Usado, por exemplo, quando a variável [!DNL Platform] o cliente tem endereços de email simples como um atributo e sua plataforma aceita apenas emails com hash. É aqui que você forneceria a transformação que precisa ser aplicada (por exemplo, transformar o email em minúsculas e depois em hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Indica qual [namespaces de identidade padrão](/help/identity-service/namespaces.md#standard) (por exemplo, IDFA), os clientes podem mapear para a identidade que você está configurando. <br> Quando você usa `acceptedGlobalNamespaces`, você pode usar `"requiredTransformation":"sha256(lower($))"` para endereços de email ou números de telefone em letras minúsculas e com hash. |
| `destinationDelivery.authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon no sistema por meio de um nome de usuário e senha, um token de portador ou outro método de autenticação. Por exemplo, você selecionaria essa opção se também selecionasse `authType: OAUTH2` ou `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Uso `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e a [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [Credenciais](./credentials-configuration-api.md) configuração. </li><li>Uso `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationDelivery.destinationServerId` | String | A variável `instanceId` do [modelo do servidor de destino](./destination-server-api.md) usado para este destino. |
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os segmentos são ativados para o destino. <br> <ul><li> `true`: [!DNL Platform] envia os perfis históricos do usuário que se qualificaram para o segmento antes que ele seja ativado. </li><li> `false`: [!DNL Platform] O inclui somente perfis de usuário qualificados para o segmento após a ativação do segmento. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é entrada pelo usuário. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é a ID de segmento Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é o nome do segmento Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | A variável `instanceId` do [modelo de metadados de público](./audience-metadata-api.md) usado para este destino. |
| `schemaConfig.profileFields` | Matriz | Quando você adiciona predefinidos `profileFields` conforme mostrado na configuração acima, os usuários terão a opção de mapear atributos de Experience Platform para os atributos predefinidos no lado do destino. |
| `schemaConfig.profileRequired` | Booleano | Uso `true` se os usuários precisarem mapear atributos de perfil do Experience Platform para atributos personalizados no seu destino, conforme mostrado no exemplo de configuração acima. |
| `schemaConfig.segmentRequired` | Booleano | Sempre usar `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booleano | Uso `true` se os usuários precisarem mapear namespaces de identidade do Experience Platform para o esquema desejado. |
| `aggregation.aggregationType` | - | Selecione `BEST_EFFORT` ou `CONFIGURABLE_AGGREGATION`. O exemplo de configuração acima inclui `BEST_EFFORT` agregação. Para obter um exemplo de `CONFIGURABLE_AGGREGATION`, consulte o exemplo de configuração em [configuração de destino](./destination-configuration.md#example-configuration) documento. Os parâmetros relevantes para a agregação configurável estão documentados abaixo nesta tabela. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Número inteiro | O Experience Platform pode agregar vários perfis exportados em uma única chamada HTTP. Especifique o número máximo de perfis que seu ponto de extremidade deve receber em uma única chamada HTTP. Observe que esta é uma agregação de melhor esforço. Por exemplo, se você especificar o valor 100, a Platform poderá enviar qualquer número de perfis menor que 100 em uma chamada. <br> Se o servidor não aceitar vários usuários por solicitação, defina esse valor como 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Booleano | Use esse sinalizador se a chamada para o destino precisar ser dividida pela identidade. Defina esse sinalizador como `true` se o servidor aceitar apenas uma identidade por chamada, para um determinado namespace. |
| `aggregation.configurableAggregation.splitUserById` | Booleano | Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Use esse sinalizador se a chamada para o destino precisar ser dividida pela identidade. Defina esse sinalizador como `true` se o servidor aceitar apenas uma identidade por chamada, para um determinado namespace. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Número inteiro | <ul><li>*Valor mínimo: 1800*</li><li>*Valor máximo: 3600*</li><li>Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Configure um valor entre os valores mínimo e máximo aceitos. Juntamente com `maxNumEventsInBatch`, esse parâmetro determina quanto tempo o Experience Platform deve esperar até enviar uma chamada de API para o endpoint. <br> Por exemplo, se você usar o valor máximo para ambos os parâmetros, o Experience Platform aguardará 3600 segundos OU até que haja 10 mil perfis qualificados antes de fazer a chamada de API, o que acontecer primeiro. </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Número inteiro | <ul><li>*Valor mínimo: 1000*</li><li>*Valor máximo: 10000*</li><li>Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Configure um valor entre os valores mínimo e máximo aceitos. Para obter uma descrição desse parâmetro, consulte `maxBatchAgeInSecs` logo acima.</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | Booleano | Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Permite agregar os perfis exportados mapeados para o destino com base nos parâmetros abaixo: <br> <ul><li>ID do segmento</li><li> status do segmento </li><li> namespace de identidade </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Defina isso como `true` se quiser agrupar perfis exportados para o seu destino pela ID do segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Você deve definir ambos `includeSegmentId:true` e `includeSegmentStatus:true` se quiser agrupar perfis exportados para o seu destino pela ID do segmento E pelo status do segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Booleano | Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Defina isso como `true` se quiser agrupar perfis exportados para o seu destino pelo namespace de identidade. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Use esse parâmetro para especificar se você deseja que os perfis exportados sejam agregados em grupos de uma única identidade (GAID, IDFA, números de telefone, email, etc.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | String | Consulte o parâmetro na configuração de exemplo [aqui](./destination-configuration.md#example-configuration). Crie listas de grupos de identidade se quiser agrupar perfis exportados para o seu destino por grupos de namespace de identidade. Por exemplo, você pode combinar perfis que contêm os identificadores móveis IDFA e GAID em uma chamada para o seu destino e enviar emails para outra usando a configuração no exemplo. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de destino recém-criada.

## Criar configuração para um destino baseado em arquivo {#create-file-based}

Você pode criar uma nova configuração de destino fazendo uma solicitação POST para o `/authoring/destinations` terminal.

**Formato da API**

```http
POST /authoring/destinations
```

**Solicitação**

A solicitação a seguir cria um novo [!DNL Amazon S3] configuração de destino baseada em arquivo, configurada pelos parâmetros fornecidos na carga. A carga abaixo inclui todos os parâmetros para destinos baseados em arquivo aceitos pelo `/authoring/destinations` terminal. Observe que não é necessário adicionar todos os parâmetros na chamada e que o modelo é personalizável, de acordo com os requisitos da API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
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
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
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
                "ONCE",
                "EVERY_HOUR"
            ],
            "defaultFrequency":"DAILY",
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

Para obter descrições detalhadas de todos os parâmetros acima, consulte [configuração de destino baseada em arquivo](file-based-destination-configuration.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de destino recém-criada.

## Listar configurações de destino {#retrieve-list}

Você pode recuperar uma lista de todas as configurações de destino para sua Organização IMS fazendo uma solicitação GET para o `/authoring/destinations` terminal.

**Formato da API**


```http
GET /authoring/destinations
```

**Solicitação**

A solicitação a seguir recuperará a lista de configurações de destino às quais você tem acesso com base na Organização IMS e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de configurações de destino às quais você tem acesso, com base na ID da organização IMS e no nome da sandbox usados. Um `instanceId` corresponde ao modelo para um destino. A resposta é truncada por brevidade.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
            },
            "another_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true
            }
         },
         "segmentMappingConfig":{
            "mapExperiencePlatformSegmentName":false,
            "mapExperiencePlatformSegmentId":false,
            "mapUserInput":false,
            "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
         },
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Indica o título do destino no catálogo de Experience Platform. |
| `description` | String | Forneça uma descrição que o Adobe usará no catálogo de destinos de Experience Platform para o cartão de destino. Mire não mais do que 4-5 frases. |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Uso `TEST` ao configurar seu destino pela primeira vez. |
| `customerAuthenticationConfigurations` | String | Indica a configuração usada para autenticar clientes do Experience Platform no servidor. Consulte `authType` abaixo para obter os valores aceitos. |
| `customerAuthenticationConfigurations.authType` | String | Os valores aceitos são `OAUTH2, BEARER`. |
| `customerDataFields.name` | String | Forneça um nome para o campo personalizado que você está introduzindo. |
| `customerDataFields.type` | String | Indica o tipo de campo personalizado que você está introduzindo. Os valores aceitos são `string`, `object`, `integer` |
| `customerDataFields.title` | String | Indica o nome do campo, como visto pelos clientes na interface do usuário do Experience Platform |
| `customerDataFields.description` | String | Forneça uma descrição para o campo personalizado. |
| `customerDataFields.isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. |
| `customerDataFields.enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `customerDataFields.pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para aplicar um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, insira `^[A-Za-z]+$` neste campo. |
| `uiAttributes.documentationLink` | String | Refere-se à página da documentação no [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para o seu destino. Uso `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `https://www.adobe.com/go/destinations-moviestar-en`. Observe que esse link funciona somente depois que o Adobe definir seu destino como ativo e a documentação for publicada. |
| `uiAttributes.category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de destino](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | String | `Server-to-server` O é a única opção disponível no momento. |
| `uiAttributes.frequency` | String | `Streaming` O é a única opção disponível no momento. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se os clientes podem mapear atributos de perfil padrão para a identidade que você está configurando. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se os clientes podem mapear identidades pertencentes a [namespaces personalizados](/help/identity-service/namespaces.md#manage-namespaces) à identidade que você está configurando. |
| `identityNamespaces.externalId.transformation` | String | _Não mostrado no exemplo de configuração_. Usado, por exemplo, quando a variável [!DNL Platform] o cliente tem endereços de email simples como um atributo e sua plataforma aceita apenas emails com hash. É aqui que você forneceria a transformação que precisa ser aplicada (por exemplo, transformar o email em minúsculas e depois em hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Indica qual [namespaces de identidade padrão](/help/identity-service/namespaces.md#standard) (por exemplo, IDFA), os clientes podem mapear para a identidade que você está configurando. <br> Quando você usa `acceptedGlobalNamespaces`, você pode usar `"requiredTransformation":"sha256(lower($))"` para endereços de email ou números de telefone em letras minúsculas e com hash. |
| `destinationDelivery.authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon no sistema por meio de um nome de usuário e senha, um token de portador ou outro método de autenticação. Por exemplo, você selecionaria essa opção se também selecionasse `authType: OAUTH2` ou `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Uso `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e a [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [Credenciais](./authentication-configuration.md) configuração. </li><li>Uso `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationDelivery.destinationServerId` | String | A variável `instanceId` do [modelo do servidor de destino](./destination-server-api.md) usado para este destino. |
| `destConfigId` | String | Este campo é gerado automaticamente e não requer sua entrada. |
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os segmentos são ativados para o destino. <br> <ul><li> `true`: [!DNL Platform] envia os perfis históricos do usuário que se qualificaram para o segmento antes que ele seja ativado. </li><li> `false`: [!DNL Platform] O inclui somente perfis de usuário qualificados para o segmento após a ativação do segmento. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é entrada pelo usuário. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é a ID de segmento Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é o nome do segmento Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | A variável `instanceId` do [modelo de metadados de público](./audience-metadata-management.md) usado para este destino. Para configurar um modelo de metadados de público-alvo, leia o [referência da API de metadados de público](./audience-metadata-api.md). |

{style="table-layout:auto"}

## Atualizar uma configuração de destino existente {#update}

Você pode atualizar uma configuração de destino existente fazendo uma solicitação PUT para o `/authoring/destinations` e fornecendo a ID da instância da configuração de destino que você deseja atualizar. No corpo da chamada, forneça a configuração de destino atualizada.

**Formato da API**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de destino que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza uma configuração de destino existente, configurada pelos parâmetros fornecidos na carga. No exemplo de chamada abaixo, estamos atualizando a configuração [criado anteriormente](./destination-configuration-api.md#create) para aceitar GAID, IDFA e identificadores de email com hash como namespaces de identidade.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## Recuperar uma configuração de destino específica {#get}

Você pode recuperar informações detalhadas sobre uma configuração de destino específica fazendo uma solicitação GET para o `/authoring/destinations` e fornecendo a ID da instância da configuração de destino que você deseja recuperar.

**Formato da API**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de destino que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a configuração de destino especificada.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## Excluir uma configuração de destino específica {#delete}

Você pode excluir a configuração de destino especificada fazendo uma solicitação DELETE para o `/authoring/destinations` e fornecendo a ID da configuração de destino que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | A variável `id` da configuração de destino que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com uma resposta HTTP vazia.

## Manipulação de erros de API

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como configurar o destino usando o `/authoring/destinations` Endpoint da API. Ler [como usar o Destination SDK para configurar seu destino](./configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do destino.
