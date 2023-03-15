---
description: Essa configuração permite indicar informações essenciais para o destino baseado em arquivo, como nome de destino, categoria, descrição e muito mais. As configurações nessa configuração também determinam como os usuários do Experience Platform se autenticam no seu destino, como ele aparece na interface do usuário do Experience Platform e as identidades que podem ser exportadas para o seu destino.
title: Opções de configuração de destino baseadas em arquivo para o Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 74f617afe8a0f678d43fb7b949d43cef25e78b9d
workflow-type: tm+mt
source-wordcount: '2982'
ht-degree: 4%

---

# Configuração de destino baseada em arquivo {#destination-configuration}

## Visão geral {#overview}

Essa configuração permite indicar informações essenciais para o destino baseado em arquivo, como nome de destino, categoria, descrição e muito mais. As configurações nessa configuração também determinam como os usuários do Experience Platform se autenticam no seu destino, como ele aparece na interface do usuário do Experience Platform e as identidades que podem ser exportadas para o seu destino. Você também pode usar essa configuração para exibir opções relacionadas ao tipo de arquivo, formato de arquivo ou configurações de compactação dos arquivos exportados.

Essa configuração também conecta as outras configurações necessárias para que seu destino funcione, como servidor de destino e metadados de público-alvo, a esta. Leia como você pode fazer referência às duas configurações em um [mais abaixo](./file-based-destination-configuration.md#connecting-all-configurations).

Você pode configurar a funcionalidade descrita neste documento usando o `/authoring/destinations` Endpoint da API. Ler [Operações de endpoint da API de destinos](./destination-configuration-api.md) para obter uma lista completa de operações que podem ser executadas no endpoint.

## Exemplo de configuração de destino do Amazon S3 {#batch-example-configuration}

Veja abaixo um exemplo de um destino Amazon S3 personalizado privado criado por meio do `/destinations` terminal de configuração.

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
         "name":"bucketName",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
| `description` | String | Forneça uma descrição para o cartão de destino no catálogo de destinos do Experience Platform. Mire não mais do que 4-5 frases. |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Uso `TEST` ao configurar seu destino pela primeira vez. |
| `maxProfileAttributes` | String | Indica o número máximo de atributos de perfil que os clientes podem exportar para o destino. O valor padrão é `2000`. |
| `maxIdentityAttributes` | String | Indica o número máximo de namespaces de identidade que os clientes podem exportar para o destino. O valor padrão é `10`. |

{style="table-layout:auto"}

## Configurações de autenticação do cliente {#customer-authentication-configurations}

Essa seção na configuração de destinos gera a variável [Configurar novo destino](/help/destinations/ui/connect-destination.md) página na interface do usuário do Experience Platform, onde os usuários conectam o Experience Platform às contas que têm com seu destino.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

Dependendo de qual [opção de autenticação](authentication-configuration.md##supported-authentication-types) você indica na `authType` , a página Experience Platform é gerada para os usuários da seguinte maneira:

### Autenticação Amazon S3 {#s3}

Ao configurar o tipo de autenticação do Amazon S3, os usuários precisam inserir as credenciais do S3.

![Renderização da interface do usuário com autenticação S3](assets/s3-authentication-ui.png)

### Autenticação do Azure Blob  {#blob}

Ao configurar o tipo de autenticação Blob do Azure, os usuários são solicitados a inserir a cadeia de conexão.

![Renderização da interface do usuário com autenticação Blob](assets/blob-authentication-ui.png)

### SFTP com autenticação de senha

Ao configurar o SFTP com tipo de autenticação de senha, os usuários devem inserir o nome de usuário e a senha do SFTP, bem como o domínio e a porta SFTP (a porta padrão é 22).

![Renderização da interface do usuário com SFTP com autenticação de senha](assets/sftp-password-authentication-ui.png)

### SFTP com autenticação de chave SSH

Ao configurar o SFTP com tipo de autenticação de chave SSH, os usuários precisam inserir o nome de usuário SFTP e a chave SSH, bem como o domínio e a porta SFTP (a porta padrão é 22).

![Renderização da interface com SFTP com autenticação de chave SSH](assets/sftp-key-authentication-ui.png)

## Campos de dados do cliente {#customer-data-fields}

Use esta seção para solicitar que os usuários preencham campos personalizados, específicos para seu destino, ao se conectarem ao destino na interface do usuário do Experience Platform.

No exemplo abaixo, `customerDataFields` exige que os usuários insiram um nome para o destino e forneçam um [!DNL Amazon S3] nome do bucket e caminho de pasta, bem como um tipo de compactação, formato de arquivo e várias outras opções de formatação de arquivo.

Você pode acessar e usar as entradas do cliente dos campos de dados do cliente na modelagem. Usar a macro `{{customerData.exampleName}}`. Por exemplo, se você pedir aos usuários para inserir um campo bucket do Amazon S3, com o nome `bucket`, é possível acessá-lo na modelagem usando a macro `{{customerData.bucket}}`. Veja um exemplo de como um campo de dados do cliente é usado na [configuração do servidor de destino](/help/destinations/destination-sdk/server-and-file-configuration.md#s3-example).

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

>[!TIP]
>
>Todas as configurações de formatação de arquivo listadas no exemplo acima estão descritas detalhadamente na [configuração da formatação de arquivo](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) seção.

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Forneça um nome para o campo personalizado que você está introduzindo. |
| `title` | String | Indica o nome do campo, como visto pelos clientes na interface do usuário do Experience Platform. |
| `description` | String | Forneça uma descrição para o campo personalizado. |
| `type` | String | Indica o tipo de campo personalizado que você está introduzindo. Os valores aceitos são `string`, `object`, `integer`. |
| `isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. |
| `pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para aplicar um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, insira `^[A-Za-z]+$` neste campo. |
| `enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `default` | String | Define o valor padrão a partir de um `enum` lista. |

{style="table-layout:auto"}

## Atributos da interface {#ui-attributes}

Esta seção se refere aos elementos da interface na configuração acima que o Adobe deve usar para seu destino na interface do usuário do Adobe Experience Platform.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `documentationLink` | String | Refere-se à página da documentação no [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para o seu destino. Uso `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `http://www.adobe.com/go/destinations-moviestar-en`. Observe que esse link funciona somente depois que o Adobe definir seu destino como ativo e a documentação for publicada. |
| `category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | String | O URL no qual você hospedou o ícone a ser exibido no cartão do catálogo de destinos. Para integrações personalizadas privadas, isso não é necessário. Para configurações produzidas, é necessário compartilhar um ícone com a equipe do Adobe ao [enviar o destino para revisão](/help/destinations/destination-sdk/submit-destination.md#logo). |
| `connectionType` | String | O tipo de conexão, dependendo do destino. Valores compatíveis: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Booleano | Indica se a conexão de destino está incluída na variável [fluxo executa a IU](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Ao definir como `true`: <ul><li>A variável **[!UICONTROL Data da última execução do fluxo de dados]** e **[!UICONTROL Status da última execução do fluxo de dados]** são exibidos na página de navegação de destino.</li><li>A variável **[!UICONTROL O fluxo de dados é executado]** e **[!UICONTROL Dados de ativação]** as guias são exibidas na página de exibição de destino.</li></ul> |
| `monitoringSupported` | Booleano | Indica se a conexão de destino está incluída na variável [interface de monitoramento](../ui/destinations-workspace.md#browse). Ao definir como `true`, o **[!UICONTROL Exibir no monitoramento]** será exibida na página de navegação de destino. |
| `frequency` | String | Refere-se ao tipo de exportação de dados compatível com o destino. Defina como `Batch` para destinos baseados em arquivo. |

{style="table-layout:auto"}

## Entrega de destino {#destination-delivery}

A seção delivery de destino indica para onde vão exatamente os dados exportados e qual regra de autenticação é usada no local onde os dados serão direcionados. É necessário especificar um ou mais `destinationServerId`s onde os dados serão entregues e e regra de autenticação. Na maioria dos casos, a regra de autenticação que você deve usar é `CUSTOMER_AUTHENTICATION`.

A variável `deliveryMatchers` é opcional e pode ser usada se estiver especificando várias `destinationServerId`s. Se for esse o caso, a autoridade `deliveryMatchers` indica como os dados exportados devem ser divididos entre os vários servidores de destino.

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
| `authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon no sistema por meio de qualquer um dos seguintes métodos: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Uso `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e a [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [Credenciais](./credentials-configuration-api.md) configuração. </li><li>Uso `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationServerId` | String | A variável `instanceId` do [configuração do servidor de destino](./server-and-file-configuration.md) que você [criado](/help/destinations/destination-sdk/destination-server-api.md#create-file-based) para este destino. |

{style="table-layout:auto"}

## Configuração do mapeamento de segmentos {#segment-mapping}

Esta seção da configuração de destino está relacionada a como os metadados de segmento, como nomes de segmentos ou IDs, devem ser compartilhados entre o Experience Platform e o destino.

Por meio da `audienceTemplateId`, esta seção também vincula essa configuração com o [configuração de metadados de público](./audience-metadata-management.md).

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
| `mapExperiencePlatformSegmentName` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é o nome do segmento Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é a ID de segmento Experience Platform. |
| `mapUserInput` | Booleano | Controla se a ID de mapeamento de segmento no fluxo de trabalho de ativação de destino é entrada pelo usuário. |
| `audienceTemplateId` | Booleano | A variável `instanceId` do [modelo de metadados de público](./audience-metadata-management.md) usado para este destino. Para configurar um modelo de metadados de público-alvo, leia o [referência da API de metadados de público](./audience-metadata-api.md). |

## Configuração de esquema na etapa de mapeamento {#schema-configuration}

O Adobe Experience Platform Destination SDK suporta esquemas definidos por parceiros. Um esquema definido pelo parceiro permite que os usuários mapeiem atributos de perfil e identidades para esquemas personalizados definidos por parceiros de destino, semelhantes ao [destinos de transmissão](destination-configuration.md#schema-configuration) fluxo de trabalho.

Use os parâmetros em `schemaConfig` para habilitar a etapa de mapeamento do workflow de ativação de destino. Usando os parâmetros descritos abaixo, você pode determinar se os usuários do Experience Platform podem mapear atributos de perfil e/ou identidades para o seu destino baseado em arquivo.

Você pode criar campos de esquema estáticos e codificados ou especificar um esquema dinâmico ao qual o Experience Platform deve se conectar para recuperar e preencher campos dinamicamente no esquema de destino do workflow de mapeamento. O schema de destino é mostrado na captura de tela abaixo.

![Captura de tela destacando os campos de esquema de destino na etapa de mapeamento do fluxo de trabalho de ativação.](/help/destinations/destination-sdk/assets/target-schema-fields.png)

### Configuração estática de campo de esquema codificado

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
| `profileFields` | Matriz | Quando você adiciona predefinidos `profileFields`, os usuários do Experience Platform têm a opção de mapear atributos da Platform para os atributos predefinidos em seu destino. |
| `profileRequired` | Booleano | Uso `true` se os usuários precisarem mapear atributos de perfil do Experience Platform para atributos personalizados no seu destino, conforme mostrado no exemplo de configuração acima. |
| `segmentRequired` | Booleano | Sempre usar `segmentRequired:true`. |
| `identityRequired` | Booleano | Uso `true` se os usuários puderem mapear namespaces de identidade do Experience Platform para o esquema desejado. |

{style="table-layout:auto"}

### Configuração do esquema dinâmico na etapa de mapeamento {#dynamic-schema-configuration}

Use os parâmetros em  `dynamicSchemaConfig` para recuperar dinamicamente seu próprio esquema, ao qual os atributos e/ou identidades do perfil da Platform podem ser mapeados.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"2aa8a809-c4ae-4f66-bb02-12df2e0a2279",
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
| `profileRequired` | Booleano | Uso `true` se os usuários precisarem mapear atributos de perfil do Experience Platform para atributos personalizados no seu destino, conforme mostrado no exemplo de configuração acima. |
| `segmentRequired` | Booleano | Sempre usar `segmentRequired:true`. |
| `identityRequired` | Booleano | Uso `true` se os usuários puderem mapear namespaces de identidade do Experience Platform para o esquema desejado. |
| `destinationServerId` | String | A variável `instanceId` do [configuração do servidor de destino](./destination-server-api.md) que você criou para o esquema dinâmico. Esse servidor de destino inclui o endpoint HTTP que o Experience Platform chamará para recuperar o esquema dinâmico usado para preencher campos de destino. |
| `authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon no sistema por meio de qualquer um dos seguintes métodos: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Uso `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e a [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [Credenciais](./credentials-configuration-api.md) configuração. </li><li>Uso `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `value` | String | O nome do schema a ser exibido na interface do usuário do Experience Platform, na etapa de mapeamento. |
| `responseFormat` | String | Sempre definida como `SCHEMA` ao definir um esquema personalizado. |

{style="table-layout:auto"}

### Mapeamentos necessários {#required-mappings}

Na configuração do esquema, você tem a opção de adicionar mapeamentos necessários (ou predefinidos). Esses são mapeamentos que os usuários podem visualizar, mas não modificar, ao configurar uma conexão com o seu destino. Por exemplo, é possível impor que o campo de endereço de email sempre seja enviado ao destino nos arquivos exportados. Veja abaixo dois exemplos de uma configuração de esquema com mapeamentos necessários e como eles se parecem na etapa de mapeamento do [ativar dados para fluxo de trabalho de destinos em lote](/help/destinations/ui/activate-batch-profile-destinations.md).

```json
    "requiredMappingsOnly": true, // when this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID", //if only the destination field is specified, then the user is able to select a source field to map to the destination.
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
```

![Imagem dos mapeamentos necessários no fluxo de ativação da interface do usuário.](/help/destinations/destination-sdk/assets/required-mappings-1.png)

```json
    "requiredMappingsOnly": true, // when this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address" //when both source and destination fields are specified as required mappings, then the user can not select or edit any of the two fields and can only view the selection.
      }
    ] 
```

![Imagem dos mapeamentos necessários no fluxo de ativação da interface do usuário.](/help/destinations/destination-sdk/assets/required-mappings-2.png)

>[!NOTE]
>
>As combinações de mapeamentos necessários compatíveis no momento são:
>* Você pode configurar um campo de origem e um campo de destino obrigatórios. Nesse caso, os usuários não podem editar ou selecionar nenhum dos dois campos e só podem visualizar a seleção.
>* Você pode configurar apenas um campo de destino obrigatório. Nesse caso, os usuários poderão selecionar um campo de origem para mapear para o destino.
>
> No momento, está configurando apenas um campo de origem obrigatório *não* compatível.

Use os parâmetros descritos na tabela abaixo se quiser adicionar os mapeamentos necessários no fluxo de trabalho de ativação do seu destino.

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `requiredMappingsOnly` | Booleano | Indica se os usuários poderão mapear outros atributos e identidades no fluxo de ativação, *além de* os mapeamentos necessários definidos por você. |
| `requiredMappings.mandatoryRequired` | Booleano | Defina como verdadeiro se este campo deve ser um atributo obrigatório que deve estar sempre presente nas exportações do arquivo para o seu destino. Leia mais sobre [atributos obrigatórios](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `requiredMappings.primaryKeyRequired` | Booleano | Defina como true se esse campo precisar ser usado como uma chave de desduplicação em exportações de arquivo para o seu destino. Leia mais sobre [chaves de desduplicação](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `requiredMappings.sourceType` | String | Usado quando você configura um campo de origem conforme necessário. Uso `"text/x.schema-path"`, que indica que o campo de origem é um atributo XDM predefinido |
| `requiredMappings.source` | String | Indica qual deve ser o campo de origem obrigatório. |
| `requiredMappings.destination` | String | Indica qual deve ser o campo de destino obrigatório. |

{style="table-layout:auto"}

## Identidades e atributos {#identities-and-attributes}

Os parâmetros nesta seção determinam quais identidades seu destino aceita. Essa configuração também preenche as identidades e os atributos do público-alvo na [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) da interface do usuário do Experience Platform, em que os usuários mapeiam identidades e atributos de seus esquemas XDM para o esquema em seu destino.


```json
"identityNamespaces": {
        "crm_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

Você deve indicar qual [!DNL Platform] identidades que os clientes podem exportar para o seu destino. Alguns exemplos são [!DNL Experience Cloud ID], email com hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Esses valores são [!DNL Platform] namespaces de identidade que os clientes podem mapear para namespaces de identidade do seu destino. Você também pode indicar se os clientes podem mapear namespaces personalizados para identidades compatíveis com seu destino (`acceptsCustomNamespaces: true`) e se os clientes puderem mapear atributos XDM padrão para identidades compatíveis com seu destino (`acceptsAttributes: true`).

Os namespaces de identidade não exigem uma correspondência de 1 para 1 entre [!DNL Platform] e seu destino.
Por exemplo, os clientes podem mapear um [!DNL Platform] [!DNL IDFA] namespace para um [!DNL IDFA] namespace do seu destino ou eles podem mapear o mesmo [!DNL Platform] [!DNL IDFA] namespace para um [!DNL Customer ID] namespace no seu destino.

Leia mais sobre identidades na [Visão geral do namespace de identidade](/help/identity-service/namespaces.md).


## Configuração em lote - Nomeação de arquivos e agendamento de exportação {#batch-configuration}

Esta seção se refere às configurações de nomenclatura de arquivo e agendamento de exportação que serão exibidas para seu destino na interface do usuário do Adobe Experience Platform. Os valores configurados aqui são exibidos na variável [Agendar exportação de segmento](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) etapa do fluxo de trabalho de ativação dos destinos baseados em arquivo.

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
| `defaultExportMode` | Enum | Define o modo de exportação de arquivo padrão. Valores compatíveis:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> O valor padrão é `DAILY_FULL_EXPORT`. Consulte a [documentação de ativação em lote](../ui/activate-batch-profile-destinations.md#scheduling) para obter detalhes sobre o agendamento de exportações de arquivos. |
| `allowedExportModes` | Lista | Define os modos de exportação de arquivo disponíveis para clientes. Valores compatíveis:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Define a frequência de exportação de arquivos disponível para os clientes. Valores compatíveis:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Define a frequência de exportação de arquivo padrão. Valores compatíveis:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> O valor padrão é `DAILY`. |
| `defaultStartTime` | String | Define a hora de início padrão da exportação de arquivos. Usa o formato de arquivo de 24 horas. O valor padrão é &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | String | *Obrigatório*. Lista de macros de nome de arquivo disponíveis para os usuários escolherem. Isso determina quais itens são anexados a nomes de arquivo exportados (ID de segmento, nome da organização, data e hora da exportação e outros). Ao definir `defaultFilename`, evite a duplicação de macros. <br><br>Valores compatíveis: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Independentemente da ordem em que você define as macros, a interface do Experience Platform sempre as exibirá na ordem apresentada aqui. <br><br> Se `defaultFilename` estiver vazio, a variável `allowedFilenameAppendOptions` a lista deve conter pelo menos uma macro. |
| `filenameConfig.defaultFilenameAppendOptions` | String | *Obrigatório*. Macros de nome de arquivo padrão pré-selecionadas que os usuários podem desmarcar.<br><br> As macros desta lista são um subconjunto das definidas em `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | String | *Opcional*. Define as macros de nome de arquivo padrão para os arquivos exportados. Eles não podem ser substituídos por usuários. <br><br>Qualquer macro definida por `allowedFilenameAppendOptions` será anexado após a variável `defaultFilename` macros. <br><br>Se `defaultFilename` estiver vazio, você deve definir pelo menos uma macro em `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

### Configuração do nome do arquivo {#file-name-configuration}

Use macros de configuração de nome de arquivo para definir o que os nomes de arquivo exportados devem incluir. As macros na tabela abaixo descrevem os elementos encontrados na interface do usuário do [configuração do nome do arquivo](../ui/activate-batch-profile-destinations.md#file-names) tela.


>[!TIP]
> 
>Como prática recomendada, inclua sempre a variável `SEGMENT_ID` em seus nomes de arquivo exportados. As IDs de segmento são exclusivas, portanto, incluí-las no nome do arquivo é a melhor maneira de garantir que os nomes de arquivo também sejam exclusivos.

| Macro | Rótulo da interface | Descrição | Exemplo |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destino] | Nome do destino na interface do usuário. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID do segmento] | ID de segmento exclusiva gerada pela Platform | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nome do segmento] | Nome de segmento definido pelo usuário | Assinante do VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID de destino] | ID exclusiva gerada pela Platform da instância de destino | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nome do destino] | Nome definido pelo usuário da instância de destino. | Meu destino de publicidade de 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nome da Organização] | Nome da organização do cliente no Adobe Experience Platform. | Nome da Minha Organização |
| `SANDBOX_NAME` | [!UICONTROL Nome da sandbox] | Nome da sandbox usada pelo cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Data e hora] | `DATETIME` e `TIMESTAMP` ambos definem quando o arquivo foi gerado, mas em formatos diferentes. <br><br><ul><li>`DATETIME` O usa o seguinte formato: AAAAMMDD_HHMMSS.</li><li>`TIMESTAMP` O usa o formato Unix de 10 dígitos. </li></ul> `DATETIME` e `TIMESTAMP` são mutuamente exclusivas e não podem ser usadas simultaneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texto personalizado] | Texto personalizado definido pelo usuário a ser incluído no nome do arquivo. Não pode ser usado em `defaultFilename`. | Meu_Texto_Personalizado |
| `TIMESTAMP` | [!UICONTROL Data e hora] | Carimbo de data e hora de 10 dígitos da hora em que o arquivo foi gerado, no formato Unix. | 1652131584 |

{style="table-layout:auto"}

![Imagem da interface do usuário mostrando a tela de configuração de nome de arquivo com macros pré-selecionadas](assets/file-name-configuration.png)

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


## Qualificações do perfil histórico {#profile-backfill}

Você pode usar o `backfillHistoricalProfileData` na configuração de destinos para determinar se as qualificações de perfil históricas devem ser exportadas para o seu destino.

```json
   "backfillHistoricalProfileData":true
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os segmentos são ativados para o destino. <br> <ul><li> `true`: [!DNL Platform] envia os perfis históricos do usuário que se qualificaram para o segmento antes que ele seja ativado. </li><li> `false`: [!DNL Platform] O inclui somente perfis de usuário qualificados para o segmento após a ativação do segmento. </li></ul> |

{style="table-layout:auto"}

## Como essa configuração conecta todas as informações necessárias ao seu destino {#connecting-all-configurations}

Algumas das configurações de destino devem ser definidas por meio do [servidor de destino](./server-and-file-configuration.md) ou o [configuração de metadados de público](./audience-metadata-management.md) pontos finais. A configuração de destino descrita aqui conecta todas essas configurações fazendo referência às duas outras configurações da seguinte maneira:

* Use o `destinationServerId` para referenciar o servidor de destino e a configuração do modelo de arquivo configurados para o seu destino.
* Use o `audienceMetadataId` para referenciar a configuração de metadados de público-alvo configurada para o seu destino.
