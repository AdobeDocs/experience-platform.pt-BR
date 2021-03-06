---
description: Essa configuração permite indicar informações básicas, como nome de destino, categoria, descrição, logotipo e muito mais. As configurações nessa configuração também determinam como os usuários do Experience Platform se autenticam para o seu destino, como ele aparece na interface do usuário do Experience Platform e as identidades que podem ser exportadas para o seu destino.
title: Opções de configuração de destino de fluxo para o Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: fe61b2ebe1a06e8909ef675cae088cb4e7d2b325
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 4%

---

# Configuração de destino de transmissão {#destination-configuration}

## Visão geral {#overview}

Essa configuração permite indicar informações essenciais para seu destino de streaming, como nome do destino, categoria, descrição e muito mais. As configurações nessa configuração também determinam como os usuários do Experience Platform se autenticam para o seu destino, como ele aparece na interface do usuário do Experience Platform e as identidades que podem ser exportadas para o seu destino.

Essa configuração também conecta as outras configurações necessárias para que o destino funcione - servidor de destino e metadados de público-alvo - a essa configuração. Leia como você pode fazer referência às duas configurações em uma [seção mais abaixo](./destination-configuration.md#connecting-all-configurations).

Você pode configurar a funcionalidade descrita neste documento usando o `/authoring/destinations` Ponto de extremidade da API. Ler [Operações de endpoint da API de destinos](./destination-configuration-api.md) para obter uma lista completa de operações que podem ser realizadas no ponto de extremidade.

## Exemplo de configuração de transmissão {#example-configuration}

Este é um exemplo de configuração de um destino ficcional de transmissão, Moviestar, que tem endpoints em quatro locais no mundo. O destino pertence à categoria destinos móveis .

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
   "backfillHistoricalProfileData":true
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Indica o título do destino no catálogo de Experience Platform. |
| `description` | String | Forneça uma descrição para o cartão de destino no catálogo de destinos do Experience Platform. Mire por não mais do que 4 a 5 frases. |
| `status` | String | Indica o status do ciclo de vida do cartão de destino. Os valores aceitos são `TEST`, `PUBLISHED` e `DELETED`. Use `TEST` ao configurar o destino pela primeira vez. |

{style=&quot;table-layout:auto&quot;}

## Configurações de autenticação do cliente {#customer-authentication-configurations}

Essa seção na configuração de destinos gera a variável [Configurar novo destino](/help/destinations/ui/connect-destination.md) na interface do usuário do Experience Platform, onde os usuários conectam o Experience Platform às contas que têm com seu destino. Dependendo da opção de autenticação que você indicar na `authType` , a Experience Platform é gerada para os usuários da seguinte maneira:

### Autenticação do portador

Ao configurar o tipo de autenticação do portador, os usuários são solicitados a inserir o token do portador que obtêm do seu destino.

![Renderização da interface do usuário com autenticação do portador](assets/bearer-authentication-ui.png)

### Autenticação OAuth 2

Usuários selecionados **[!UICONTROL Ligar ao destino]** para acionar o fluxo de autenticação do OAuth 2 para o seu destino, conforme mostrado no exemplo abaixo para o destino Públicos personalizados do Twitter. Para obter informações detalhadas sobre como configurar a autenticação OAuth 2 para o terminal de destino, leia o [Página de autenticação do Destination SDK OAuth 2](./oauth2-authentication.md).

![Renderização da interface do usuário com autenticação OAuth 2](assets/oauth2-authentication-ui.png)

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `customerAuthenticationConfigurations` | String | Indica a configuração usada para autenticar clientes do Experience Platform para o servidor. Consulte `authType` abaixo para valores aceitos. |
| `authType` | String | Os valores aceitos para destinos de transmissão são:<ul><li>`BEARER`. Se o destino oferecer suporte à autenticação do portador, defina `"authType":"Bearer"` e  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` no [seção delivery de destino](./destination-configuration.md).</li><li>`OAUTH2`. Se o destino oferecer suporte à autenticação OAuth 2, defina `"authType":"OAUTH2"` e adicione os campos obrigatórios para o OAuth 2, conforme mostrado no [Página de autenticação do Destination SDK OAuth 2](./oauth2-authentication.md). Além disso, defina `"authenticationRule":"CUSTOMER_AUTHENTICATION"` no [seção delivery de destino](./destination-configuration.md).</li> |

{style=&quot;table-layout:auto&quot;}

## Campos de dados do cliente {#customer-data-fields}

Use esta seção para solicitar que os usuários preencham campos personalizados, específicos para seu destino, ao se conectar ao destino na interface do usuário do Experience Platform. A configuração é refletida no fluxo de autenticação, como mostrado abaixo.

![Fluxo de autenticação de campo personalizado](./assets/custom-field-authentication-flow.png)

>[!TIP]
>
>Você pode acessar e usar as entradas do cliente dos campos de dados do cliente no modelo. Usar a macro `{{customerData.name}}`. Por exemplo, se você solicitar que os usuários insiram um campo de ID do cliente, com o nome `userId`, você pode acessá-lo no modelo usando a macro `{{customerData.userId}}`. Visualize um exemplo de como um campo de dados do cliente é usado no URL do terminal da API, na [configuração do servidor de destino](/help/destinations/destination-sdk/server-and-template-configuration.md#server-specs).

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `name` | String | Forneça um nome para o campo personalizado que está sendo introduzido. |
| `type` | String | Indica o tipo de campo personalizado que está sendo introduzido. Os valores aceitos são `string`, `object`, `integer`. |
| `title` | String | Indica o nome do campo, como é visto pelos clientes na interface do usuário do Experience Platform. |
| `description` | String | Forneça uma descrição para o campo personalizado. |
| `isRequired` | Booleano | Indica se esse campo é necessário no fluxo de trabalho de configuração de destino. |
| `enum` | String | Renderiza o campo personalizado como um menu suspenso e lista as opções disponíveis para o usuário. |
| `pattern` | String | Impõe um padrão para o campo personalizado, se necessário. Use expressões regulares para impor um padrão. Por exemplo, se as IDs do cliente não incluírem números ou sublinhados, insira `^[A-Za-z]+$` neste campo. |

{style=&quot;table-layout:auto&quot;}

## Atributos da interface do usuário {#ui-attributes}

Esta seção se refere aos elementos da interface do usuário na configuração acima que o Adobe deve usar para seu destino na interface do usuário do Adobe Experience Platform. Consulte abaixo:

![Imagem da configuração de atributos da interface do usuário.](/help/destinations/destination-sdk/assets/ui-attributes-configuration.png)

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `documentationLink` | String | Refere-se à página de documentação na [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para o seu destino. Use `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `http://www.adobe.com/go/destinations-moviestar-en`. Observe que esse link funciona somente após o Adobe definir seu destino live e a documentação ser publicada. |
| `category` | String | Refere-se à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de Destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br> Observe que, no momento, você pode selecionar apenas uma categoria por destino. |
| `connectionType` | String | `Server-to-server` no momento, é a única opção disponível. |
| `frequency` | String | Refere-se ao tipo de exportação de dados suportado pelo destino. Valores compatíveis: <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Configuração de esquema na etapa de mapeamento {#schema-configuration}

![Ativar etapa de mapeamento](./assets/enable-mapping-step.png)

Use os parâmetros em `schemaConfig` para habilitar a etapa de mapeamento do workflow de ativação de destino. Ao usar os parâmetros descritos abaixo, você pode determinar se os usuários do Experience Platform podem mapear atributos e/ou identidades de perfil para o esquema desejado no lado do destino.

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `profileFields` | Matriz | *Não mostrado no exemplo de configuração acima.* Ao adicionar predefinido `profileFields`, os usuários do Experience Platform têm a opção de mapear atributos da plataforma para os atributos predefinidos no lado do destino. |
| `profileRequired` | Booleano | Use `true` se os usuários forem capazes de mapear atributos de perfil do Experience Platform para atributos personalizados no lado do seu destino, como mostrado na configuração de exemplo acima. |
| `segmentRequired` | Booleano | Sempre use `segmentRequired:true`. |
| `identityRequired` | Booleano | Use `true` se os usuários forem capazes de mapear os namespaces de identidade do Experience Platform para o esquema desejado. |

{style=&quot;table-layout:auto&quot;}

## Identidades e atributos {#identities-and-attributes}

Os parâmetros desta seção determinam quais identidades seu destino aceita. Essa configuração também preenche as identidades e os atributos de direcionamento no [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) da interface do usuário do Experience Platform, onde os usuários mapeiam identidades e atributos de seus esquemas XDM para o esquema no seu destino.

Você deve indicar qual [!DNL Platform] identidades que os clientes podem exportar para o seu destino. Alguns exemplos são [!DNL Experience Cloud ID], email com hash, ID do dispositivo ([!DNL IDFA], [!DNL GAID]). Esses valores são [!DNL Platform] namespaces de identidade que os clientes podem mapear para namespaces de identidade a partir do seu destino. Você também pode indicar se os clientes podem mapear namespaces personalizados para identidades suportadas pelo seu destino.

Os namespaces de identidade não exigem uma correspondência de 1 para 1 entre [!DNL Platform] e seu destino.
Por exemplo, os clientes podem mapear uma [!DNL Platform] [!DNL IDFA] namespace para um [!DNL IDFA] namespace do seu destino ou podem mapear o mesmo [!DNL Platform] [!DNL IDFA] namespace para um [!DNL Customer ID] namespace no seu destino.

Leia mais na [Visão geral do Namespace de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR).

![Renderizar identidades de direcionamento na interface do usuário](./assets/target-identities-ui.png)

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `acceptsAttributes` | Booleano | Indica se o destino aceita atributos de perfil padrão. Normalmente, esses atributos são destacados na documentação dos parceiros. |
| `acceptsCustomNamespaces` | Booleano | Indica se os clientes podem configurar namespaces personalizados no seu destino. |
| `transformation` | String | *Não mostrado na configuração de exemplo*. Usado, por exemplo, quando a variável [!DNL Platform] o cliente tem endereços de email simples como um atributo e sua plataforma aceita apenas emails com hash. Nesse objeto, é possível aplicar a transformação que precisa ser aplicada (por exemplo, transformar o email em minúsculas e, em seguida, em hash). Para ver um exemplo, consulte `requiredTransformation` no [referência da API de configuração de destino](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | Usado para casos em que a plataforma aceita [namespaces de identidade padrão](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (por exemplo, IDFA), para que seja possível restringir usuários da plataforma a selecionar somente esses namespaces de identidade. |

{style=&quot;table-layout:auto&quot;}

## Delivery de destino {#destination-delivery}

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authenticationRule` | String | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Use `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon em seu sistema por meio de um nome de usuário e senha, um token portador ou outro método de autenticação. Por exemplo, você selecionaria essa opção se também selecionasse `authType: OAUTH2` ou `authType:BEARER` em `customerAuthenticationConfigurations`. </li><li> Use `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e o [!DNL Platform] o cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [Credenciais](./credentials-configuration-api.md) configuração. </li><li>Use `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationServerId` | String | O `instanceId` do [configuração do servidor de destino](./destination-server-api.md) usado para este destino. |

{style=&quot;table-layout:auto&quot;}

## Configuração do mapeamento de segmento {#segment-mapping}

![Seção de configuração do mapeamento de segmentos](./assets/segment-mapping-configuration.png)

Esta seção da configuração de destino está relacionada a como os metadados do segmento, como nomes de segmento ou IDs, devem ser compartilhados entre o Experience Platform e seu destino.

Por meio da `audienceTemplateId`, esta seção também vincula essa configuração ao [configuração de metadados do público-alvo](./audience-metadata-management.md).

Os parâmetros mostrados na configuração acima são descritos na seção [referência da API do endpoint de destinos](./destination-configuration-api.md).

## Política de agregação {#aggregation}

![Política de agregação no template de configuração](./assets/aggregation-configuration.png)

Esta seção permite definir as políticas de agregação que o Experience Platform deve usar ao exportar dados para seu destino.

Uma política de agregação determina como os perfis exportados são combinados nas exportações de dados. As opções disponíveis são:
* Melhor agregação de esforço
* Agregação configurável (mostrada na configuração acima)

Leia a seção em [uso de modelos](./message-format.md#using-templating) e [exemplos de chaves de agregação](./message-format.md#template-aggregation-key) para entender como incluir a política de agregação em seu template de transformação de mensagem com base em sua política de agregação selecionada.

### Melhor agregação de esforço {#best-effort-aggregation}

>[!TIP]
>
>Use essa opção se o terminal da API aceitar menos de 100 perfis por chamada de API.

Essa opção funciona melhor para destinos que preferem menos perfis por solicitação e preferem receber mais solicitações com menos dados do que menos solicitações com mais dados.

Use o `maxUsersPerRequest` para especificar o número máximo de perfis que seu destino pode receber em uma solicitação.

### Agregação configurável {#configurable-aggregation}

Essa opção funciona melhor se você preferir obter grandes lotes, com milhares de perfis na mesma chamada. Essa opção também permite agregar os perfis exportados com base em regras de agregação complexas.

Essa opção permite:

* Defina o tempo máximo e o número máximo de perfis a serem agregados antes que uma chamada de API seja feita no seu destino.
* Agregue os perfis exportados mapeados para o destino com base em:
   * ID do segmento;
   * Status do segmento;
   * Identidade ou grupos de identidades.

>[!NOTE]
>
>Ao usar a opção de agregação configurável para o seu destino, tenha em mente os valores mínimo e máximo que você pode usar para os dois parâmetros `maxBatchAgeInSecs` (mínimo 1,800 e máximo 3,600) e `maxNumEventsInBatch` (mínimo 1.000, máximo 10.000).

Para obter explicações detalhadas dos parâmetros de agregação, consulte [Operações de endpoint da API de destinos](./destination-configuration-api.md) página de referência, onde cada parâmetro é descrito.

## Qualificações de perfil histórico {#profile-backfill}

Você pode usar o `backfillHistoricalProfileData` na configuração de destinos para determinar se as qualificações de perfil histórico devem ser exportadas para o seu destino.

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controla se os dados históricos do perfil são exportados quando os segmentos são ativados para o destino. <br> <ul><li> `true`: [!DNL Platform] envia os perfis de usuário históricos que se qualificaram para o segmento antes que ele seja ativado. </li><li> `false`: [!DNL Platform] inclui somente perfis de usuário qualificados para o segmento após ele ser ativado. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Como essa configuração conecta todas as informações necessárias ao seu destino {#connecting-all-configurations}

Algumas de suas configurações de destino devem ser configuradas por meio do [servidor de destino](./server-and-template-configuration.md) ou [configuração de metadados do público-alvo](./audience-metadata-management.md). A configuração de destino descrita aqui conecta todas essas configurações fazendo referência às duas outras configurações da seguinte maneira:

* Use o `destinationServerId` para fazer referência ao servidor de destino e à configuração do modelo configurada para o seu destino.
* Use o `audienceMetadataId` para fazer referência à configuração de metadados do público-alvo configurada para o seu destino.