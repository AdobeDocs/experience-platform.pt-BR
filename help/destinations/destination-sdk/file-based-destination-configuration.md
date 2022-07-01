---
description: Essa configuração permite indicar informações básicas, como nome de destino, categoria, descrição, logotipo e muito mais. As configurações nessa configuração também determinam como os usuários do Experience Platform se autenticam para o seu destino, como ele aparece na interface do usuário do Experience Platform e as identidades que podem ser exportadas para o seu destino.
title: (Beta) Opções de configuração de destino baseadas em arquivo para o Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 301cef53644e813c3fd43e7f2dbaf730c9e5fc11
workflow-type: tm+mt
source-wordcount: '2330'
ht-degree: 6%

---

# (Beta) Configuração de destino baseada em arquivo {#destination-configuration}

## Visão geral {#overview}

>[!IMPORTANT]
>
>No momento, o suporte ao destino baseado em arquivo no Adobe Experience Platform Destination SDK está na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

Essa configuração permite indicar informações essenciais para seu destino baseado em arquivo, como nome de destino, categoria, descrição e muito mais. As configurações nessa configuração também determinam como os usuários do Experience Platform se autenticam para o seu destino, como ele aparece na interface do usuário do Experience Platform e as identidades que podem ser exportadas para o seu destino.

Essa configuração também conecta as outras configurações necessárias para que o destino funcione - servidor de destino e metadados de público-alvo - a essa configuração. Leia como você pode fazer referência às duas configurações em uma [seção mais abaixo](./destination-configuration.md#connecting-all-configurations).

Você pode configurar a funcionalidade descrita neste documento usando o `/authoring/destinations` Ponto de extremidade da API. Ler [Operações de endpoint da API de destinos](./destination-configuration-api.md) para obter uma lista completa de operações que podem ser realizadas no ponto de extremidade.

## Exemplo de configuração de destino do Amazon S3 {#batch-example-configuration}

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes":"2000",
   "maxIdentityAttributes":"10",
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
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
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
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
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
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
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
         "title":"header",
         "description":"Writes the names of columns as the first line.",
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
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
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
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
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
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"phoneNo",
            "title":"phoneNo",
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
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Indica o título do destino no catálogo de Experience Platform. |
| `description` | String | Forneça uma descrição para o cartão de destino no catálogo de destinos do Experience Platform. Mire por não mais do que 4 a 5 frases. |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Use `TEST` ao configurar o destino pela primeira vez. |
| `maxProfileAttributes` | String | Indica o número máximo de atributos de perfil que os clientes podem exportar para o destino. O valor padrão é `2000`. |
| `maxIdentityAttributes` | String | Indica o número máximo de namespaces de identidade que os clientes podem exportar para o destino. O valor padrão é `10`. |

{style=&quot;table-layout:auto&quot;}

## Configurações de autenticação do cliente {#customer-authentication-configurations}

Essa seção na configuração de destinos gera a variável [Configurar novo destino](/help/destinations/ui/connect-destination.md) na interface do usuário do Experience Platform, onde os usuários conectam o Experience Platform às contas que têm com seu destino.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

Dependendo de qual [opção de autenticação](authentication-configuration.md##supported-authentication-types) você indica no `authType` , a Experience Platform é gerada para os usuários da seguinte maneira:

### Autenticação Amazon S3 {#s3}

Ao configurar o tipo de autenticação do Amazon S3, os usuários são solicitados a inserir as credenciais do S3.

![Renderização da interface do usuário com autenticação S3](assets/s3-authentication-ui.png)

### Autenticação do Azure Blob  {#blob}

Ao configurar o tipo de autenticação Azure Blob, os usuários são solicitados a inserir a string de conexão.

![Renderização da interface do usuário com autenticação de Blob](assets/blob-authentication-ui.png)

### SFTP com autenticação de senha

Ao configurar o SFTP com o tipo de autenticação por senha, os usuários são solicitados a inserir o nome de usuário e a senha do SFTP, bem como o domínio e a porta do SFTP (a porta padrão é 22).

![Renderização da interface com o SFTP com autenticação de senha](assets/sftp-password-authentication-ui.png)

### SFTP com autenticação de chave SSH

Ao configurar o SFTP com o tipo de autenticação de chave SSH, os usuários são solicitados a inserir o nome de usuário e a chave SSH SFTP, bem como o domínio e a porta SFTP (a porta padrão é 22).

![Renderização da interface com o SFTP com autenticação de chave SSH](assets/sftp-key-authentication-ui.png)

## Campos de dados do cliente {#customer-data-fields}

Use esta seção para solicitar que os usuários preencham campos personalizados, específicos para seu destino, ao se conectar ao destino na interface do usuário do Experience Platform.

No exemplo abaixo, `customerDataFields` exige que os usuários insiram um nome para seu destino e forneçam um [!DNL Amazon S3] nome do bucket e caminho da pasta, bem como tipo de compactação, formato de arquivo e várias outras opções de exportação de arquivo.

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
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
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
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
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
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
         "title":"header",
         "description":"Writes the names of columns as the first line.",
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
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
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
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Forneça um nome para o campo personalizado que está sendo introduzido. |
| `title` | String | Indica o nome do campo, como é visto pelos clientes na interface do usuário do Experience Platform. |
| `description` | String | Forneça uma descrição para o campo personalizado. |
| `type` | String | Indica o tipo de campo personalizado que está sendo introduzido. Os valores aceitos são `string`, `object`, `integer`. |
| `isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. |
| `pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para impor um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, insira `^[A-Za-z]+$` neste campo. |
| `enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `default` | String | Define o valor padrão de um `enum` lista. |

{style=&quot;table-layout:auto&quot;}

## Atributos da interface do usuário {#ui-attributes}

Esta seção se refere aos elementos da interface do usuário na configuração acima que o Adobe deve usar para seu destino na interface do usuário do Adobe Experience Platform.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `documentationLink` | String | Refere-se à página de documentação na [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para o seu destino. Use `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `http://www.adobe.com/go/destinations-moviestar-en`. Observe que esse link funciona somente após o Adobe definir seu destino live e a documentação ser publicada. |
| `category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de Destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | String | O URL no qual você hospedou o ícone a ser exibido no cartão do catálogo de destinos. |
| `connectionType` | String | O tipo de conexão, dependendo do destino. Valores compatíveis: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Booleano | Indica se a conexão de destino está incluída no [interface do usuário de execuções de fluxo](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Ao definir para `true`: <ul><li>O **[!UICONTROL Data da última execução do fluxo de dados]** e **[!UICONTROL Status de execução do último fluxo de dados]** são exibidos na página de navegação de destino.</li><li>O **[!UICONTROL Execuções do fluxo de dados]** e **[!UICONTROL Dados de ativação]** as guias são exibidas na página de exibição de destino.</li></ul> |
| `monitoringSupported` | Booleano | Indica se a conexão de destino está incluída no [interface do usuário de monitoramento](../ui/destinations-workspace.md#browse). Ao definir para `true`, o **[!UICONTROL Exibir no monitoramento]** é exibida na página de navegação de destino. |
| `frequency` | String | Refere-se ao tipo de exportação de dados suportado pelo destino. Defina como `Batch` para destinos com base em arquivo. |

{style=&quot;table-layout:auto&quot;}

## Delivery de destino {#destination-delivery}

```json
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
   ]
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Use `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon em seu sistema por meio de um dos seguintes métodos: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Use `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e o [!DNL Platform] o cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [Credenciais](./credentials-configuration-api.md) configuração. </li><li>Use `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationServerId` | String | O `instanceId` do [configuração do servidor de destino](./destination-server-api.md) usado para este destino. |

{style=&quot;table-layout:auto&quot;}

## Configuração do mapeamento de segmento {#segment-mapping}

Esta seção da configuração de destino está relacionada a como os metadados do segmento, como nomes de segmento ou IDs, devem ser compartilhados entre o Experience Platform e seu destino.

Por meio da `audienceTemplateId`, esta seção também vincula essa configuração ao [configuração de metadados do público-alvo](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booleano | Controla se a id de mapeamento de segmento no fluxo de trabalho de ativação de destino é o nome do segmento de Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é a ID de segmento de Experience Platform. |
| `mapUserInput` | Booleano | Controla se a id de mapeamento de segmento no workflow de ativação de destino é inserida pelo usuário. |
| `audienceTemplateId` | Booleano | O `instanceId` do [modelo de metadados de público-alvo](./audience-metadata-management.md) usado para este destino. Para configurar um modelo de metadados de público-alvo, leia a [referência da API de metadados do público-alvo](./audience-metadata-api.md). |

## Configuração de esquema na etapa de mapeamento {#schema-configuration}

Use os parâmetros em `schemaConfig` para habilitar a etapa de mapeamento do workflow de ativação de destino. Ao usar os parâmetros descritos abaixo, você pode determinar se os usuários do Experience Platform podem mapear atributos e/ou identidades de perfil para o destino baseado em arquivo.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
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
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `profileFields` | Matriz | Ao adicionar predefinido `profileFields`, os usuários do Experience Platform têm a opção de mapear atributos da plataforma para os atributos predefinidos no seu destino. |
| `profileRequired` | Booleano | Use `true` se os usuários forem capazes de mapear atributos de perfil do Experience Platform para atributos personalizados no lado do seu destino, como mostrado na configuração de exemplo acima. |
| `segmentRequired` | Booleano | Sempre use `segmentRequired:true`. |
| `identityRequired` | Booleano | Use `true` se os usuários forem capazes de mapear os namespaces de identidade do Experience Platform para o esquema desejado. |

{style=&quot;table-layout:auto&quot;}

### Configuração dinâmica do schema na etapa de mapeamento {#dynamic-schema-configuration}

O Adobe Experience Platform Destination SDK suporta esquemas definidos pelo parceiro. Um esquema definido pelo parceiro permite que os usuários mapeiem os atributos e identidades do perfil para esquemas personalizados definidos pelos parceiros de destino, semelhantes ao [destinos de transmissão](destination-configuration.md#schema-configuration) fluxo de trabalho.

Use os parâmetros em  `dynamicSchemaConfig` para definir seu próprio esquema, os atributos e/ou identidades do perfil da Platform podem ser mapeadas.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `profileRequired` | Booleano | Use `true` se os usuários forem capazes de mapear atributos de perfil do Experience Platform para atributos personalizados no lado do seu destino, como mostrado na configuração de exemplo acima. |
| `segmentRequired` | Booleano | Sempre use `segmentRequired:true`. |
| `identityRequired` | Booleano | Use `true` se os usuários forem capazes de mapear os namespaces de identidade do Experience Platform para o esquema desejado. |
| `destinationServerId` | String | O `instanceId` do [configuração do servidor de destino](./destination-server-api.md) usado para este destino. |
| `authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Use `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon em seu sistema por meio de um dos seguintes métodos: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Use `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e o [!DNL Platform] o cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [Credenciais](./credentials-configuration-api.md) configuração. </li><li>Use `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `value` | String | O nome do schema a ser exibido na interface do usuário do Experience Platform, na etapa de mapeamento. |
| `responseFormat` | String | Sempre defina como `SCHEMA` ao definir um schema personalizado. |

{style=&quot;table-layout:auto&quot;}

## Identidades e atributos {#identities-and-attributes}

Os parâmetros desta seção determinam quais identidades seu destino aceita. Essa configuração também preenche as identidades e os atributos de direcionamento no [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) da interface do usuário do Experience Platform, onde os usuários mapeiam identidades e atributos de seus esquemas XDM para o esquema no seu destino.


```json
"identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

Você deve indicar qual [!DNL Platform] identidades que os clientes podem exportar para o seu destino. Alguns exemplos são [!DNL Experience Cloud ID], email com hash, ID do dispositivo ([!DNL IDFA], [!DNL GAID]). Esses valores são [!DNL Platform] namespaces de identidade que os clientes podem mapear para namespaces de identidade a partir do seu destino. Você também pode indicar se os clientes podem mapear namespaces personalizados para identidades suportadas pelo seu destino.

Os namespaces de identidade não exigem uma correspondência de 1 para 1 entre [!DNL Platform] e seu destino.
Por exemplo, os clientes podem mapear uma [!DNL Platform] [!DNL IDFA] namespace para um [!DNL IDFA] namespace do seu destino ou podem mapear o mesmo [!DNL Platform] [!DNL IDFA] namespace para um [!DNL Customer ID] namespace no seu destino.

## Configuração em lote {#batch-configuration}

Esta seção se refere às configurações de exportação de arquivos na configuração acima que o Adobe deve usar para seu destino na interface do usuário do Adobe Experience Platform.

```json
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
   }
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booleano | Defina como `true` para permitir que os clientes especifiquem quais atributos de perfil são obrigatórios. O valor padrão é `false`. Consulte [Atributos obrigatórios](../ui/activate-batch-profile-destinations.md#mandatory-attributes) para obter mais informações. |
| `allowDedupeKeyFieldSelection` | Booleano | Defina como `true` para permitir que os clientes especifiquem chaves de desduplicação. O valor padrão é `false`.  Consulte [Chaves de desduplicação](../ui/activate-batch-profile-destinations.md#deduplication-keys) para obter mais informações. |
| `defaultExportMode` | Enum | Define o modo padrão de exportação de arquivos. Valores compatíveis:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> O valor padrão é `DAILY_FULL_EXPORT`. Consulte a [documentação de ativação em lote](../ui/activate-batch-profile-destinations.md#scheduling) para obter detalhes sobre a programação de exportações de arquivos. |
| `allowedExportModes` | Lista | Define os modos de exportação de arquivos disponíveis para os clientes do . Valores compatíveis:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Define a frequência de exportação de arquivos disponível para os clientes. Valores compatíveis:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Define a frequência padrão de exportação de arquivos.Valores suportados:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> O valor padrão é `DAILY`. |
| `defaultStartTime` | String | Define a hora de início padrão para a exportação de arquivos. Usa o formato de arquivo de 24 horas. O valor padrão é &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | String | *Obrigatório*. Lista de macros de nome de arquivo disponíveis para os usuários escolherem. Isso determina quais itens são anexados aos nomes de arquivo exportados (ID do segmento, nome da organização, data e hora da exportação e outros). Ao definir `defaultFilename`, evite a duplicação de macros. <br><br>Valores compatíveis: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Independentemente da ordem em que você define as macros, a interface do usuário do Experience Platform sempre as exibirá na ordem apresentada aqui. <br><br> If `defaultFilename` está vazio, a variável `allowedFilenameAppendOptions` deve conter pelo menos uma macro. |
| `filenameConfig.defaultFilenameAppendOptions` | String | *Obrigatório*. Macros de nome de arquivo padrão pré-selecionadas que os usuários podem desmarcar.<br><br> As macros nesta lista são um subconjunto das definidas em `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | String | *Opcional*. Define as macros de nome de arquivo padrão para os arquivos exportados. Eles não podem ser substituídos pelos usuários. <br><br>Qualquer macro definida por `allowedFilenameAppendOptions` será anexada após a variável `defaultFilename` macros. <br><br>If `defaultFilename` estiver vazia, você deve definir pelo menos uma macro em `allowedFilenameAppendOptions`. |

{style=&quot;table-layout:auto&quot;}

### Configuração do nome do arquivo {#file-name-configuration}

Use macros de configuração de nome de arquivo para definir o que os nomes de arquivo exportados devem incluir. As macros na tabela abaixo descrevem os elementos encontrados na interface do usuário no [configuração do nome do arquivo](../ui/activate-batch-profile-destinations.md#file-names) tela.

Como prática recomendada, você sempre deve incluir a variável `SEGMENT_ID` em seus nomes de arquivo exportados. As IDs de segmento são exclusivas, portanto, incluí-las no nome do arquivo é a melhor maneira de garantir que os nomes de arquivo também sejam exclusivos.

| Macro | Rótulo da interface do usuário | Descrição | Exemplo |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destino] | Nome do destino na interface do usuário. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID do segmento] | ID exclusiva de segmento gerado por plataforma | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nome do segmento] | Nome de segmento definido pelo usuário | Assinante de VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID de destino] | ID exclusiva, gerada pela plataforma da instância de destino | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nome do destino] | Nome definido pelo usuário da instância de destino. | Meu destino de publicidade 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nome da Organização] | Nome da organização do cliente no Adobe Experience Platform. | Meu nome da organização |
| `SANDBOX_NAME` | [!UICONTROL Nome da sandbox] | Nome da sandbox usada pelo cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Data e hora] | `DATETIME` e `TIMESTAMP` ambos definem quando o arquivo foi gerado, mas em formatos diferentes. <br><br><ul><li>`DATETIME` O usa o seguinte formato: AAAMMDD_HHMMSS.</li><li>`TIMESTAMP` O usa o formato Unix de 10 dígitos. </li></ul> `DATETIME` e `TIMESTAMP` são mutuamente exclusivas e não podem ser usadas simultaneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texto personalizado] | Texto personalizado definido pelo usuário a ser incluído no nome do arquivo. Não pode ser usado em `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Data e hora] | Carimbo de data e hora de 10 dígitos da hora em que o arquivo foi gerado, no formato Unix. | 1652131584 |

{style=&quot;table-layout:auto&quot;}

![Imagem da interface do usuário que mostra a tela de configuração do nome do arquivo com macros pré-selecionadas](assets/file-name-configuration.png)

O exemplo mostrado na imagem acima usa a seguinte configuração de macro de nome de arquivo:

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```


## Qualificações de perfil histórico {#profile-backfill}

Você pode usar o `backfillHistoricalProfileData` na configuração de destinos para determinar se as qualificações de perfil histórico devem ser exportadas para o seu destino.

```json
   "backfillHistoricalProfileData":true
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os segmentos são ativados para o destino. <br> <ul><li> `true`: [!DNL Platform] envia os perfis de usuário históricos que se qualificaram para o segmento antes que ele seja ativado. </li><li> `false`: [!DNL Platform] inclui somente perfis de usuário qualificados para o segmento após ele ser ativado. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Como essa configuração conecta todas as informações necessárias ao seu destino {#connecting-all-configurations}

Algumas de suas configurações de destino devem ser configuradas por meio do [servidor de destino](./server-and-file-configuration.md) ou [configuração de metadados do público-alvo](./audience-metadata-management.md). A configuração de destino descrita aqui conecta todas essas configurações fazendo referência às duas outras configurações da seguinte maneira:

* Use o `destinationServerId` para fazer referência ao servidor de destino e à configuração do modelo configurada para o seu destino.
* Use o `audienceMetadataId` para fazer referência à configuração de metadados do público-alvo configurada para o seu destino.
