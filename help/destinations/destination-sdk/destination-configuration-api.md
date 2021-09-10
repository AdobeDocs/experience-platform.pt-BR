---
description: Esta página lista e descreve todas as operações da API que podem ser realizadas usando o endpoint da API `/authoring/destination`.
title: Operações de endpoint da API de destinos
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '2381'
ht-degree: 5%

---

# Operações de API do endpoint de destinos {#destination-configuration}

>[!IMPORTANT]
>
>**Ponto de extremidade** da API:  `platform.adobe.io/data/core/activation/authoring/destinations`

Esta página lista e descreve todas as operações de API que podem ser executadas usando o endpoint da API `/authoring/destinations`. Para obter uma descrição da funcionalidade suportada por este ponto de extremidade, leia [configuração de destino](./destination-configuration.md).

## Introdução às operações da API de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Criar configuração para um destino {#create}

Você pode criar uma nova configuração de destino fazendo uma solicitação POST para o endpoint `/authoring/destinations`.

**Formato da API**


```http
POST /authoring/destinations
```

**Solicitação**

A solicitação a seguir cria uma nova configuração de destino, configurada pelos parâmetros fornecidos no payload. A carga abaixo inclui todos os parâmetros aceitos pelo ponto de extremidade `/authoring/destinations`. Observe que não é necessário adicionar todos os parâmetros na chamada do e que o modelo é personalizável, de acordo com os requisitos da API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
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
| `name` | String | Indica o título do seu destino no catálogo de Experience Platform |
| `description` | String | Forneça uma descrição que o Adobe usará no catálogo de destinos do Experience Platform para o cartão de destino. Mire por não mais do que 4 a 5 frases. |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Use `TEST` ao configurar o destino pela primeira vez. |
| `customerAuthenticationConfigurations` | String | Indica a configuração usada para autenticar clientes do Experience Platform para o servidor. Consulte `authType` abaixo para obter os valores aceitos. |
| `customerAuthenticationConfigurations.authType` | String | Os valores aceitos são `OAUTH2, BEARER`. |
| `customerDataFields.name` | String | Forneça um nome para o campo personalizado que está sendo introduzido. |
| `customerDataFields.type` | String | Indica o tipo de campo personalizado que está sendo introduzido. Os valores aceitos são `string`, `object`, `integer` |
| `customerDataFields.title` | String | Indica o nome do campo, como é visto pelos clientes na interface do usuário do Experience Platform |
| `customerDataFields.description` | String | Forneça uma descrição para o campo personalizado. |
| `customerDataFields.isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. |
| `customerDataFields.enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `customerDataFields.pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para impor um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, digite `^[A-Za-z]+$` neste campo. |
| `uiAttributes.documentationLink` | String | Refere-se à página de documentação no [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para seu destino. Use `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `http://www.adobe.com/go/destinations-moviestar-en`. |
| `uiAttributes.category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de destino](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | String | `Server-to-server` no momento, é a única opção disponível. |
| `uiAttributes.frequency` | String | `Streaming` no momento, é a única opção disponível. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se o destino aceita atributos de perfil padrão. Normalmente, esses atributos são destacados na documentação de nossos parceiros. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se os clientes podem configurar namespaces personalizados no seu destino. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | String | _Não mostrado na configuração_ de exemplo. Usado, por exemplo, quando o cliente [!DNL Platform] tem endereços de email simples como um atributo e sua plataforma aceita apenas emails com hash. É aqui que você fornece a transformação que precisa ser aplicada (por exemplo, transformar o email em minúsculas e, em seguida, em hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | _Não mostrado na configuração_ de exemplo. Usado para casos em que sua plataforma aceita [namespaces de identidade padrão](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (por exemplo, IDFA), para que você possa restringir os usuários da plataforma a selecionar apenas esses namespaces de identidade. <br> Ao usar o  `acceptedGlobalNamespaces`, você pode usar  `"requiredTransformation":"sha256(lower($))"` para endereços de email em letras minúsculas e em hash ou números de telefone. Para ver como esse parâmetro é usado, visualize a configuração na seção abaixo [Atualizar uma configuração de destino](./destination-configuration-api.md#update). |
| `destinationDelivery.authenticationRule` | String | Indica como os clientes [!DNL Platform] se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Use `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon em seu sistema por meio de um nome de usuário e senha, um token portador ou outro método de autenticação. Por exemplo, você selecionaria essa opção se também selecionasse `authType: OAUTH2` ou `authType:BEARER` em `customerAuthenticationConfigurations`. </li><li> Use `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e o cliente [!DNL Platform] não precisar fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando a configuração [Credentials](./credentials-configuration.md). </li><li>Use `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationDelivery.destinationServerId` | String | O `instanceId` do [modelo de servidor de destino](./destination-server-api.md) usado para este destino. |
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os segmentos são ativados para o destino. <br> <ul><li> `true`:  [!DNL Platform] envia os perfis de usuário históricos que se qualificaram para o segmento antes que ele seja ativado. </li><li> `false`:  [!DNL Platform] inclui somente perfis de usuário qualificados para o segmento após ele ser ativado. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controla se a id de mapeamento de segmento no workflow de ativação de destino é inserida pelo usuário. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é a ID de segmento de Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controla se a id de mapeamento de segmento no fluxo de trabalho de ativação de destino é o nome do segmento de Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | O `instanceId` do [modelo de metadados de público-alvo](./audience-metadata-api.md) usado para esse destino. |
| `schemaConfig.profileFields` | Matriz | Ao adicionar `profileFields` predefinido, conforme mostrado na configuração acima, os usuários terão a opção de mapear atributos de Experience Platform para os atributos predefinidos no lado do destino. |
| `schemaConfig.profileRequired` | Booleano | Use `true` se os usuários forem capazes de mapear atributos de perfil do Experience Platform para atributos personalizados no lado do seu destino, como mostrado na configuração de exemplo acima. |
| `schemaConfig.segmentRequired` | Booleano | Sempre use `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booleano | Use `true` se os usuários puderem mapear os namespaces de identidade do Experience Platform para o esquema desejado. |
| `aggregation.aggregationType` | - | Selecione `BEST_EFFORT` ou `CONFIGURABLE_AGGREGATION`. Embora a configuração de exemplo acima inclua ambos os tipos de agregação, você só precisará selecionar um deles para o seu destino. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Número inteiro | O Experience Platform pode agregar vários perfis exportados em uma única chamada HTTP. Especifique o número máximo de perfis que seu terminal deve receber em uma única chamada HTTP. Observe que esta é a melhor agregação de esforço. Por exemplo, se você especificar o valor 100, a Platform poderá enviar qualquer número de perfis menor que 100 em uma chamada. <br> Se o servidor não aceitar vários usuários por solicitação, defina esse valor como 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Booleano | Use esse sinalizador se a chamada para o destino deve ser dividida por identidade. Defina esse sinalizador como `true` se o servidor aceitar apenas uma identidade por chamada, para um determinado namespace. |
| `aggregation.configurableAggregation.splitUserById` | Booleano | Use esse sinalizador se a chamada para o destino deve ser dividida por identidade. Defina esse sinalizador como `true` se o servidor aceitar apenas uma identidade por chamada, para um determinado namespace. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Número inteiro | *Valor máximo: 3600*. Juntamente com `maxNumEventsInBatch`, isso determina por quanto tempo o Experience Platform deve aguardar até enviar uma chamada de API para o terminal. <br> Por exemplo, se você usar o valor máximo para ambos os parâmetros, o Experience Platform aguardará 3600 segundos OU até que haja 10.000 perfis qualificados antes de fazer a chamada da API, o que ocorrer primeiro. |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Número inteiro | *Valor máximo: 10000*. Consulte `maxBatchAgeInSecs` logo acima. |
| `aggregation.configurableAggregation.aggregationKey` | Booleano | Permite agregar os perfis exportados mapeados para o destino com base nos parâmetros abaixo: <br> <ul><li>ID do segmento</li><li> status do segmento </li><li> namespace de identidade </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Defina como `true` se desejar agrupar perfis exportados para seu destino por ID de segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Você deve definir `includeSegmentId:true` e `includeSegmentStatus:true` se quiser agrupar perfis exportados para seu destino por ID de segmento E status de segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Booleano | Defina como `true` se desejar agrupar perfis exportados para seu destino pelo namespace de identidade. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Use esse parâmetro para especificar se deseja que os perfis exportados sejam agregados em grupos de uma única identidade (GAID, IDFA, números de telefone, email, etc.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | String | Crie listas de grupos de identidade se quiser agrupar perfis exportados para seu destino por grupos de namespace de identidade. Por exemplo, você pode combinar perfis que contêm os identificadores móveis IDFA e GAID em uma chamada para seu destino e emails em outra usando a configuração no exemplo. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de destino recém-criada.

## Listar configurações de destino {#retrieve-list}

Você pode recuperar uma lista de todas as configurações de destino para sua Organização IMS fazendo uma solicitação de GET para o endpoint `/authoring/destinations`.

**Formato da API**


```http
GET /authoring/destinations
```

**Solicitação**

A solicitação a seguir recuperará a lista de configurações de destino às quais você tem acesso, com base na Organização IMS e na configuração da sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta a seguir retorna o status HTTP 200 com uma lista de configurações de destino às quais você tem acesso, com base na IMS Organization ID e no nome da sandbox usados. Um `instanceId` corresponde ao modelo para um destino. A resposta é truncada por brevidade.

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
         "aggregation":{
            "aggregationType":"CONFIGURABLE_AGGREGATION",
            "configurableAggregation":{
               "splitUserById":true,
               "maxBatchAgeInSecs":0,
               "maxNumEventsInBatch":0,
               "aggregationKey":{
                  "includeSegmentId":true,
                  "includeSegmentStatus":true,
                  "includeIdentity":true,
                  "oneIdentityPerGroup":false,
                  "groups":[
                     {
                        "namespaces":[
                           "IDFA",
                           "GAID"
                        ]
                     },
                     {
                        "namespaces":[
                           "EMAIL"
                        ]
                     }
                  ]
               }
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Indica o título do destino no catálogo de Experience Platform. |
| `description` | String | Forneça uma descrição que o Adobe usará no catálogo de destinos do Experience Platform para o cartão de destino. Mire por não mais do que 4 a 5 frases. |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Use `TEST` ao configurar o destino pela primeira vez. |
| `customerAuthenticationConfigurations` | String | Indica a configuração usada para autenticar clientes do Experience Platform para o servidor. Consulte `authType` abaixo para obter os valores aceitos. |
| `customerAuthenticationConfigurations.authType` | String | Os valores aceitos são `OAUTH2, BEARER`. |
| `customerDataFields.name` | String | Forneça um nome para o campo personalizado que está sendo introduzido. |
| `customerDataFields.type` | String | Indica o tipo de campo personalizado que está sendo introduzido. Os valores aceitos são `string`, `object`, `integer` |
| `customerDataFields.title` | String | Indica o nome do campo, como é visto pelos clientes na interface do usuário do Experience Platform |
| `customerDataFields.description` | String | Forneça uma descrição para o campo personalizado. |
| `customerDataFields.isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. |
| `customerDataFields.enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `customerDataFields.pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para impor um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, digite `^[A-Za-z]+$` neste campo. |
| `uiAttributes.documentationLink` | String | Refere-se à página de documentação no [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para seu destino. Use `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `http://www.adobe.com/go/destinations-moviestar-en` |
| `uiAttributes.category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de destino](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | String | `Server-to-server` no momento, é a única opção disponível. |
| `uiAttributes.frequency` | String | `Streaming` no momento, é a única opção disponível. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se o destino aceita atributos de perfil padrão. Normalmente, esses atributos são destacados na documentação de nossos parceiros. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se os clientes podem configurar namespaces personalizados no seu destino. Leia mais sobre [namespaces personalizados](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) no Adobe Experience Platform. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | String | _Não mostrado na configuração_ de exemplo. Usado, por exemplo, quando o cliente [!DNL Platform] tem endereços de email simples como um atributo e sua plataforma aceita apenas emails com hash. É aqui que você fornece a transformação que precisa ser aplicada (por exemplo, transformar o email em minúsculas e, em seguida, em hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | _Não mostrado na configuração_ de exemplo. Usado para casos em que sua plataforma aceita [namespaces de identidade padrão](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (por exemplo, IDFA), para que você possa restringir os usuários da plataforma a selecionar apenas esses namespaces de identidade. |
| `destinationDelivery.authenticationRule` | String | Indica como os clientes [!DNL Platform] se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Use `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon em seu sistema por meio de um nome de usuário e senha, um token portador ou outro método de autenticação. Por exemplo, você selecionaria essa opção se também selecionasse `authType: OAUTH2` ou `authType:BEARER` em `customerAuthenticationConfigurations`. </li><li> Use `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e o cliente [!DNL Platform] não precisar fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando a configuração [Credentials](./credentials-configuration.md). </li><li>Use `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationDelivery.destinationServerId` | String | O `instanceId` do [modelo de servidor de destino](./destination-server-api.md) usado para este destino. |
| `inputSchemaId` | String | Este campo é gerado automaticamente e não requer sua entrada. |
| `destConfigId` | String | Este campo é gerado automaticamente e não requer sua entrada. |
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os segmentos são ativados para o destino. <br> <ul><li> `true`:  [!DNL Platform] envia os perfis de usuário históricos que se qualificaram para o segmento antes que ele seja ativado. </li><li> `false`:  [!DNL Platform] inclui somente perfis de usuário qualificados para o segmento após ele ser ativado. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controla se a id de mapeamento de segmento no workflow de ativação de destino é inserida pelo usuário. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é a ID de segmento de Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controla se a id de mapeamento de segmento no fluxo de trabalho de ativação de destino é o nome do segmento de Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | O `instanceId` do [modelo de metadados de público-alvo](./audience-metadata-management.md) usado para esse destino. Para configurar um modelo de metadados de público-alvo, leia a [referência da API de metadados de público-alvo](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Atualizar uma configuração de destino existente {#update}

Você pode atualizar uma configuração de destino existente fazendo uma solicitação de PUT para o endpoint `/authoring/destinations` e fornecendo a ID da instância da configuração de destino que deseja atualizar. No corpo da chamada , forneça a configuração de destino atualizada.

**Formato da API**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{INSTANCE_ID}` | A ID da configuração de destino que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza uma configuração de destino existente, configurada pelos parâmetros fornecidos no payload. Na chamada de exemplo abaixo, estamos atualizando a configuração [criada anteriormente](./destination-configuration-api.md#create) para agora aceitar identificadores de email com hash, GAID e IDFA como namespaces de identidade.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
   "backfillHistoricalProfileData":true
}
```

## Recuperar uma configuração de destino específica {#get}

Você pode recuperar informações detalhadas sobre uma configuração de destino específica fazendo uma solicitação de GET para o endpoint `/authoring/destinations` e fornecendo a ID da instância da configuração de destino que deseja recuperar.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
   "backfillHistoricalProfileData":true
}
```


## Excluir uma configuração de destino específica {#delete}

Você pode excluir a configuração de destino especificada, fazendo uma solicitação DELETE ao ponto de extremidade `/authoring/destinations` e fornecendo a ID da configuração de destino que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{INSTANCE_ID}` | O `id` da configuração de destino que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 junto com uma resposta HTTP vazia.

## Tratamento de erros da API

Os pontos de extremidade da API do SDK de destino seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [erros do cabeçalho da solicitação](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, você agora sabe como configurar seu destino usando o endpoint da API `/authoring/destinations`. Leia [como usar o SDK de destino para configurar seu destino](./configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
