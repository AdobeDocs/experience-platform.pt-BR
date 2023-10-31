---
description: Saiba como estruturar uma chamada de API para criar uma configuração de destino por meio do Adobe Experience Platform Destination SDK.
title: Criar uma configuração de destino
exl-id: aae4aaa8-1dd0-4041-a86c-5c86f04d7d13
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---

# Criar uma configuração de destino

Esta página exemplifica a solicitação de API e a carga que você pode usar para criar sua própria configuração de destino usando o `/authoring/destinations` Endpoint da API.

Para obter uma descrição detalhada dos recursos que você pode configurar por meio desse endpoint, leia os seguintes artigos:

* [Configuração de autenticação do cliente](../../functionality/destination-configuration/customer-authentication.md)
* [Autenticação OAuth2](../../functionality/destination-configuration/oauth2-authentication.md)
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

## Criar uma configuração de destino {#create}

Você pode criar uma nova configuração de destino fazendo uma solicitação POST para o `/authoring/destinations` terminal.

>[!TIP]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/destinations`

**Formato da API**

```http
POST /authoring/destinations
```

A solicitação a seguir cria um novo [!DNL Amazon S3] configuração de destino, configurada pelos parâmetros fornecidos na carga. A carga abaixo inclui todos os parâmetros para destinos baseados em arquivo aceitos pelo `/authoring/destinations` terminal.

Observe que não é necessário adicionar todos os parâmetros à chamada de API e que a carga é personalizável, de acordo com os requisitos da API.

+++Solicitação

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
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
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
         "title":"Select a fileType",
         "description":"Select fileType",
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

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Indica o título do destino no catálogo de Experience Platform. |
| `description` | String | Forneça uma descrição que o Adobe usará no catálogo de destinos de Experience Platform para o cartão de destino. Mire não mais do que 4-5 frases. ![Imagem da interface do usuário da Platform mostrando a descrição do destino.](../../assets/authoring-api/destination-configuration/destination-description.png "Descrição do destino"){width="100" zoomable="yes"} |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Uso `TEST` ao configurar seu destino pela primeira vez. |
| `customerAuthenticationConfigurations.authType` | String | Indica a configuração usada para autenticar clientes do Experience Platform no servidor de destino. Consulte [configuração de autenticação do cliente](../../functionality/destination-configuration/customer-authentication.md) para obter informações detalhadas sobre os tipos de autenticação compatíveis. |
| `customerDataFields.name` | String | Forneça um nome para o campo personalizado que você está introduzindo. <br/><br/> Consulte [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) para obter informações detalhadas sobre essas configurações. ![Imagem da interface do usuário da Platform mostrando campos de dados do cliente.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "Campo de dados do cliente"){width="100" zoomable="yes"} |
| `customerDataFields.type` | String | Indica o tipo de campo personalizado que você está introduzindo. Os valores aceitos são `string`, `object`, `integer`. <br/><br/> Consulte [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) para obter informações detalhadas sobre essas configurações. |
| `customerDataFields.title` | String | Indica o nome do campo, como visto pelos clientes na interface do usuário do Experience Platform. <br/><br/> Consulte [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) para obter informações detalhadas sobre essas configurações. |
| `customerDataFields.description` | String | Forneça uma descrição para o campo personalizado. Consulte [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) para obter informações detalhadas sobre essas configurações. |
| `customerDataFields.isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. <br/><br/> Consulte [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) para obter informações detalhadas sobre essas configurações. |
| `customerDataFields.enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. <br/><br/> Consulte [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) para obter informações detalhadas sobre essas configurações. |
| `customerDataFields.default` | String | Define o valor padrão a partir de um `enum` lista. |
| `customerDataFields.pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para aplicar um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, insira `^[A-Za-z]+$` neste campo. <br/><br/> Consulte [Campos de dados do cliente](../../functionality/destination-configuration/customer-data-fields.md) para obter informações detalhadas sobre essas configurações. |
| `uiAttributes.documentationLink` | String | Refere-se à página da documentação no [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para o seu destino. Uso `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `https://www.adobe.com/go/destinations-moviestar-en`. Observe que esse link funciona somente depois que o Adobe definir seu destino como ativo e a documentação for publicada. <br/><br/> Consulte [Atributos da interface](../../functionality/destination-configuration/ui-attributes.md) para obter informações detalhadas sobre essas configurações. ![Imagem da interface do usuário da Platform mostrando o link da documentação.](../../assets/authoring-api/destination-configuration/documentation-url.png "URL da documentação"){width="100" zoomable="yes"} |
| `uiAttributes.category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de destino](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> Consulte [Atributos da interface](../../functionality/destination-configuration/ui-attributes.md) para obter informações detalhadas sobre essas configurações. |
| `uiAttributes.connectionType` | String | O tipo de conexão, dependendo do destino. Valores compatíveis: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | String | Refere-se ao tipo de exportação de dados compatível com o destino. Defina como `Streaming` para integrações baseadas em API, ou `Batch` ao exportar arquivos para seus destinos. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica se os clientes podem mapear atributos de perfil padrão para a identidade que você está configurando. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica se os clientes podem mapear identidades pertencentes a [namespaces personalizados](/help/identity-service/namespaces.md#manage-namespaces) à identidade que você está configurando. |
| `identityNamespaces.externalId.transformation` | String | _Não mostrado no exemplo de configuração_. Usado, por exemplo, quando a variável [!DNL Platform] o cliente tem endereços de email simples como um atributo e sua plataforma aceita apenas emails com hash. É aqui que você forneceria a transformação que precisa ser aplicada (por exemplo, transformar o email em minúsculas e depois em hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Indica qual [namespaces de identidade padrão](/help/identity-service/namespaces.md#standard) (por exemplo, IDFA), os clientes podem mapear para a identidade que você está configurando. <br> Quando você usa `acceptedGlobalNamespaces`, você pode usar `"requiredTransformation":"sha256(lower($))"` para endereços de email ou números de telefone em letras minúsculas e com hash. |
| `destinationDelivery.authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon no sistema por meio de um nome de usuário e senha, um token de portador ou outro método de autenticação. Por exemplo, você selecionaria essa opção se também selecionasse `authType: OAUTH2` ou `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Uso `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e a [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [API de credenciais](../../credentials-api/create-credential-configuration.md) configuração. </li><li>Uso `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationDelivery.destinationServerId` | String | A variável `instanceId` do [modelo do servidor de destino](../destination-server/create-destination-server.md) usado para este destino. |
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os públicos são ativados para o destino. Sempre definir como `true`. |
| `segmentMappingConfig.mapUserInput` | Booleano | Controla se a ID do mapeamento de público no fluxo de trabalho de ativação de destino é entrada pelo usuário. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controla se a ID de mapeamento de público-alvo no fluxo de trabalho de ativação de destino é a ID de público-alvo Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controla se a ID de mapeamento de público no fluxo de trabalho de ativação de destino é o nome do público-alvo Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | A variável `instanceId` do [modelo de metadados de público](../../metadata-api/create-audience-template.md) usado para este destino. |
| `schemaConfig.profileFields` | Matriz | Quando você adiciona predefinidos `profileFields` conforme mostrado na configuração acima, os usuários terão a opção de mapear atributos de Experience Platform para os atributos predefinidos no lado do destino. |
| `schemaConfig.profileRequired` | Booleano | Uso `true` se os usuários precisarem mapear atributos de perfil do Experience Platform para atributos personalizados no seu destino, conforme mostrado no exemplo de configuração acima. |
| `schemaConfig.segmentRequired` | Booleano | Sempre usar `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booleano | Uso `true` se os usuários precisarem mapear namespaces de identidade do Experience Platform para o esquema desejado. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da configuração de destino recém-criada.

+++

## Manipulação de erros de API

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, você sabe como criar uma nova configuração de destino por meio do Destination SDK `/authoring/destinations` Endpoint da API.

Para saber mais sobre o que você pode fazer com esse endpoint, consulte os seguintes artigos:

* [Recuperar uma configuração de destino](retrieve-destination-configuration.md)
* [Atualizar uma configuração de destino](update-destination-configuration.md)
* [Excluir uma configuração de destino](delete-destination-configuration.md)

Para entender onde esse endpoint se encaixa no processo de criação de destino, consulte os seguintes artigos:

* [Usar o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
