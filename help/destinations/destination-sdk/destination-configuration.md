---
description: Essa configuração permite indicar informações básicas como nome de destino, categoria, descrição, logotipo e muito mais. As configurações nessa configuração também determinam como os usuários do Experience Platform se autenticam no seu destino, como ele aparece na interface do usuário do Experience Platform e as identidades que podem ser exportadas para o seu destino.
title: Opções de configuração de destino de transmissão para Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 3%

---

# Configuração de destino de transmissão {#destination-configuration}

## Visão geral {#overview}

Essa configuração permite indicar informações essenciais para o destino de streaming, como nome de destino, categoria, descrição e muito mais. As configurações nessa configuração também determinam como os usuários do Experience Platform se autenticam no seu destino, como ele aparece na interface do usuário do Experience Platform e as identidades que podem ser exportadas para o seu destino.

Essa configuração também conecta as outras configurações necessárias para que seu destino funcione, como servidor de destino e metadados de público-alvo, a esta. Leia como você pode fazer referência às duas configurações em um [mais abaixo](./destination-configuration.md#connecting-all-configurations).

Você pode configurar a funcionalidade descrita neste documento usando o `/authoring/destinations` Endpoint da API. Ler [Operações de endpoint da API de destinos](./destination-configuration-api.md) para obter uma lista completa de operações que podem ser executadas no endpoint.

## Exemplo de configuração de transmissão {#example-configuration}

Esta é uma configuração de exemplo de um destino de transmissão fictício, Moviestar, que tem pontos de extremidade em quatro locais no globo. O destino pertence à categoria destinos móveis.

```json
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
         "name":"endpointRegion",
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
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
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
   "backfillHistoricalProfileData":true
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Indica o título do destino no catálogo de Experience Platform. |
| `description` | String | Forneça uma descrição para o cartão de destino no catálogo de destinos do Experience Platform. Mire não mais do que 4-5 frases. |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Uso `TEST` ao configurar seu destino pela primeira vez. |

{style="table-layout:auto"}

## Configurações de autenticação do cliente {#customer-authentication-configurations}

Essa seção na configuração de destinos gera a variável [Configurar novo destino](/help/destinations/ui/connect-destination.md) página na interface do usuário do Experience Platform, onde os usuários conectam o Experience Platform às contas que têm com seu destino. Dependendo da opção de autenticação indicada na caixa `authType` , a página Experience Platform é gerada para os usuários da seguinte maneira:

### Autenticação do portador

Ao configurar o tipo de autenticação de portador, os usuários precisam inserir o token de portador que obtêm do seu destino.

![Renderização da interface do usuário com autenticação do portador](assets/bearer-authentication-ui.png)

### Autenticação OAuth 2

Os usuários selecionam **[!UICONTROL Conectar ao destino]** para acionar o fluxo de autenticação do OAuth 2 para o seu destino, como mostrado no exemplo abaixo para o destino de Públicos-alvo personalizados da Twitter. Para obter informações detalhadas sobre como configurar a autenticação OAuth 2 para o endpoint de destino, leia a seção dedicada [Página de autenticação OAuth 2 do Destination SDK](./oauth2-authentication.md).

![Renderização da interface do usuário com autenticação OAuth 2](assets/oauth2-authentication-ui.png)

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `customerAuthenticationConfigurations` | String | Indica a configuração usada para autenticar clientes do Experience Platform no servidor. Consulte `authType` abaixo para obter os valores aceitos. |
| `authType` | String | Os valores aceitos para destinos de transmissão são:<ul><li>`BASIC`. Se o destino suportar autenticação básica, defina `"authType":"Basic"` e  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` no [seção de entrega de destino](./destination-configuration.md).</li><li>`BEARER`. Se o destino suportar autenticação de portador, defina `"authType":"Bearer"` e  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` no [seção de entrega de destino](./destination-configuration.md).</li><li>`OAUTH2`. Se o destino suportar a autenticação OAuth 2, defina `"authType":"OAUTH2"` e adicione os campos obrigatórios para o OAuth 2, conforme mostrado no [Página de autenticação OAuth 2 do Destination SDK](./oauth2-authentication.md). Além disso, defina `"authenticationRule":"CUSTOMER_AUTHENTICATION"` no [seção de entrega de destino](./destination-configuration.md).</li> |

{style="table-layout:auto"}

## Campos de dados do cliente {#customer-data-fields}

Use esta seção para solicitar que os usuários preencham campos personalizados, específicos para seu destino, ao se conectarem ao destino na interface do usuário do Experience Platform. A configuração é refletida no fluxo de autenticação, conforme mostrado abaixo.

![Fluxo de autenticação de campo personalizado](./assets/custom-field-authentication-flow.png)

>[!TIP]
>
>Você pode acessar e usar as entradas do cliente dos campos de dados do cliente na modelagem. Usar a macro `{{customerData.name}}`. Por exemplo, se você pedir aos usuários para inserir um campo ID do cliente, com o nome `userId`, é possível acessá-lo na modelagem usando a macro `{{customerData.userId}}`. Veja um exemplo de como um campo de dados do cliente é usado no URL do endpoint da API, na [configuração do servidor de destino](/help/destinations/destination-sdk/server-and-template-configuration.md#server-specs).

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Forneça um nome para o campo personalizado que você está introduzindo. |
| `type` | String | Indica o tipo de campo personalizado que você está introduzindo. Os valores aceitos são `string`, `object`, `integer`. |
| `title` | String | Indica o nome do campo, como visto pelos clientes na interface do usuário do Experience Platform. |
| `description` | String | Forneça uma descrição para o campo personalizado. |
| `isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. |
| `enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para aplicar um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, insira `^[A-Za-z]+$` neste campo. |

{style="table-layout:auto"}

## Atributos da interface {#ui-attributes}

Esta seção se refere aos elementos da interface na configuração acima que o Adobe deve usar para seu destino na interface do usuário do Adobe Experience Platform. Consulte abaixo:

![Imagem da configuração de atributos da interface do usuário.](/help/destinations/destination-sdk/assets/ui-attributes-configuration.png)

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `documentationLink` | String | Refere-se à página da documentação no [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para o seu destino. Uso `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `http://www.adobe.com/go/destinations-moviestar-en`. Observe que esse link funciona somente depois que o Adobe definir seu destino como ativo e a documentação for publicada. |
| `category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br> Observe que, atualmente, você pode selecionar apenas uma categoria por destino. |
| `connectionType` | String | `Server-to-server` O é a única opção disponível no momento. |
| `frequency` | String | Refere-se ao tipo de exportação de dados compatível com o destino. Valores compatíveis: <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style="table-layout:auto"}

## Configuração de esquema na etapa de mapeamento {#schema-configuration}

![Habilitar etapa de mapeamento](./assets/enable-mapping-step.png)

Use os parâmetros em `schemaConfig` para habilitar a etapa de mapeamento do workflow de ativação de destino. Usando os parâmetros descritos abaixo, você pode determinar se os usuários do Experience Platform podem mapear atributos de perfil e/ou identidades para o esquema desejado no lado do destino.

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `profileFields` | Matriz | *Não mostrado no exemplo de configuração acima.* Quando você adiciona predefinidos `profileFields`, os usuários do Experience Platform têm a opção de mapear atributos da Platform para os atributos predefinidos do lado do destino. |
| `profileRequired` | Booleano | Uso `true` se os usuários precisarem mapear atributos de perfil do Experience Platform para atributos personalizados no seu destino, conforme mostrado no exemplo de configuração acima. |
| `segmentRequired` | Booleano | Sempre usar `segmentRequired:true`. |
| `identityRequired` | Booleano | Uso `true` se os usuários puderem mapear namespaces de identidade do Experience Platform para o esquema desejado. |

{style="table-layout:auto"}

## Identidades e atributos {#identities-and-attributes}

Os parâmetros nesta seção determinam quais identidades seu destino aceita. Essa configuração também preenche as identidades e os atributos do público-alvo na [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) da interface do usuário do Experience Platform, em que os usuários mapeiam identidades e atributos de seus esquemas XDM para o esquema em seu destino.

Você deve indicar qual [!DNL Platform] identidades que os clientes podem exportar para o seu destino. Alguns exemplos são [!DNL Experience Cloud ID], email com hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Esses valores são [!DNL Platform] namespaces de identidade que os clientes podem mapear para namespaces de identidade do seu destino. Você também pode indicar se os clientes podem mapear namespaces personalizados para identidades compatíveis com seu destino (`acceptsCustomNamespaces: true`) e se os clientes puderem mapear atributos XDM padrão para identidades compatíveis com seu destino (`acceptsAttributes: true`).

Os namespaces de identidade não exigem uma correspondência de 1 para 1 entre [!DNL Platform] e seu destino.
Por exemplo, os clientes podem mapear um [!DNL Platform] [!DNL IDFA] namespace para um [!DNL IDFA] namespace do seu destino ou eles podem mapear o mesmo [!DNL Platform] [!DNL IDFA] namespace para um [!DNL Customer ID] namespace no seu destino.

Leia mais sobre identidades na [Visão geral do namespace de identidade](/help/identity-service/namespaces.md).

![Renderizar identidades de destino na interface](./assets/target-identities-ui.png)

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `acceptsAttributes` | Booleano | Indica se os clientes podem mapear atributos de perfil padrão para a identidade que você está configurando. |
| `acceptsCustomNamespaces` | Booleano | Indica se os clientes podem configurar namespaces personalizados no seu destino. |
| `transformation` | String | *Não mostrado no exemplo de configuração*. Usado, por exemplo, quando a variável [!DNL Platform] o cliente tem endereços de email simples como um atributo e sua plataforma aceita apenas emails com hash. Nesse objeto, você pode modificar a transformação que precisa ser aplicada (por exemplo, transformar o email em minúsculas e depois em hash). Para ver um exemplo, consulte `requiredTransformation` no [referência da API de configuração de destino](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | Indica qual [namespaces de identidade padrão](/help/identity-service/namespaces.md#standard) (por exemplo, IDFA), os clientes podem mapear para a identidade que você está configurando. <br> Quando você usa `acceptedGlobalNamespaces`, você pode usar `"requiredTransformation":"sha256(lower($))"` para endereços de email ou números de telefone em letras minúsculas e com hash. |

{style="table-layout:auto"}

## Entrega de destino {#destination-delivery}

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon no sistema por meio de um nome de usuário e senha, um token de portador ou outro método de autenticação. Por exemplo, você selecionaria essa opção se também selecionasse `authType: OAUTH2` ou `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Uso `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e a [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [Credenciais](./credentials-configuration-api.md) configuração. </li><li>Uso `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationServerId` | String | A variável `instanceId` do [configuração do servidor de destino](./destination-server-api.md) usado para este destino. |

{style="table-layout:auto"}

## Configuração do mapeamento de segmentos {#segment-mapping}

![Seção de configuração de mapeamento de segmento](./assets/segment-mapping-configuration.png)

Esta seção da configuração de destino está relacionada a como os metadados de segmento, como nomes de segmentos ou IDs, devem ser compartilhados entre o Experience Platform e o destino.

Por meio da `audienceTemplateId`, esta seção também vincula essa configuração com o [configuração de metadados de público](./audience-metadata-management.md).

Os parâmetros mostrados na configuração acima estão descritos no [referência da API do endpoint de destinos](./destination-configuration-api.md).

## Política de agregação {#aggregation}

![Política de agregação no modelo de configuração](./assets/aggregation-configuration.png)

Esta seção permite que você defina as políticas de agregação que o Experience Platform deve usar ao exportar dados para seu destino.

Uma política de agregação determina como os perfis exportados são combinados nas exportações de dados. As opções disponíveis são:
* Agregação de melhor esforço
* Agregação configurável (mostrada na configuração acima)

Leia a seção sobre [uso de modelos](./message-format.md#using-templating) e a variável [exemplos de chave de agregação](./message-format.md#template-aggregation-key) para entender como incluir a política de agregação no seu template de transformação de mensagem com base na sua política de agregação selecionada.

### Agregação de melhor esforço {#best-effort-aggregation}

>[!TIP]
>
>Use essa opção se o terminal da API aceitar menos de 100 perfis por chamada de API.

Essa opção funciona melhor para destinos que preferem menos perfis por solicitação e que prefeririam receber mais solicitações com menos dados do que menos solicitações com mais dados.

Use o `maxUsersPerRequest` para especificar o número máximo de perfis que seu destino pode assumir em uma solicitação.

### Agregação configurável {#configurable-aggregation}

Essa opção funciona melhor se você preferir pegar lotes grandes, com milhares de perfis na mesma chamada. Essa opção também permite agregar os perfis exportados com base em regras de agregação complexas.

Essa opção permite:

* Defina o tempo máximo e o número máximo de perfis a serem agregados antes que uma chamada de API seja feita ao seu destino.
* Agregar os perfis exportados mapeados para o destino com base em:
   * ID de segmento;
   * Status do segmento;
   * Identidade ou grupos de identidades.

>[!NOTE]
>
>Ao usar a opção de agregação configurável para seu destino, lembre-se dos valores mínimo e máximo que você pode usar para os dois parâmetros `maxBatchAgeInSecs` (mínimo 1 800 e máximo 3 600) e `maxNumEventsInBatch` (mínimo 1.000, máximo 10.000).

Para obter explicações detalhadas sobre os parâmetros de agregação, consulte a seção [Operações de endpoint da API de destinos](./destination-configuration-api.md) página de referência, onde cada parâmetro é descrito.

## Qualificações do perfil histórico {#profile-backfill}

Você pode usar o `backfillHistoricalProfileData` na configuração de destinos para determinar se as qualificações de perfil históricas devem ser exportadas para o seu destino.

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os segmentos são ativados para o destino. <br> <ul><li> `true`: [!DNL Platform] envia os perfis históricos do usuário que se qualificaram para o segmento antes que ele seja ativado. </li><li> `false`: [!DNL Platform] O inclui somente perfis de usuário qualificados para o segmento após a ativação do segmento. </li></ul> |

{style="table-layout:auto"}

## Como essa configuração conecta todas as informações necessárias ao seu destino {#connecting-all-configurations}

Algumas das configurações de destino devem ser definidas por meio do [servidor de destino](./server-and-template-configuration.md) ou o [configuração de metadados de público](./audience-metadata-management.md). A configuração de destino descrita aqui conecta todas essas configurações fazendo referência às duas outras configurações da seguinte maneira:

* Use o `destinationServerId` para referenciar o servidor de destino e a configuração do modelo definida para o seu destino.
* Use o `audienceMetadataId` para referenciar a configuração de metadados de público-alvo configurada para o seu destino.