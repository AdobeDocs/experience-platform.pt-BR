---
description: Esta página lista e descreve as etapas para configurar um destino de transmissão usando o Destination SDK.
title: Usar o Destination SDK para configurar um destino de transmissão
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---

# Usar o Destination SDK para configurar um destino de transmissão

## Visão geral {#overview}

Esta página descreve como usar as informações em [Opções de configuração no SDK de Destinos](../functionality/configuration-options.md) e em outras funcionalidades do Destination SDK e documentos de referência de API para configurar um [destino de streaming](../../destination-types.md#streaming-destinations). As etapas são apresentadas em ordem sequencial abaixo.

## Pré-requisitos {#prerequisites}

Antes de seguir para as etapas ilustradas abaixo, leia a página [Introdução ao Destination SDK](../getting-started.md) para obter informações sobre como obter as credenciais de autenticação do Adobe I/O necessárias e outros pré-requisitos para trabalhar com as APIs do Destination SDK. Isso pressupõe que você concluiu os pré-requisitos de parceria e permissão e está pronto para começar a desenvolver seu destino.

## Etapas para usar as opções de configuração no Destination SDK para definir seu destino {#steps}

![Etapas ilustradas do uso de pontos de extremidade do Destination SDK](../assets/guides/destination-sdk-steps.png)

## Etapa 1: criar uma configuração de servidor e modelo {#create-server-template-configuration}

Comece [criando uma configuração de servidor e modelo](../authoring-api/destination-server/create-destination-server.md) usando o ponto de extremidade `/destinations-server`.

Veja abaixo um exemplo de configuração. Observe que o modelo de transformação de mensagem no parâmetro `requestBody.value` é tratado na etapa 3, [Criar modelo de transformação](#create-transformation-template).

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## Etapa 2: Criar configuração de destino {#create-destination-configuration}

Veja abaixo um exemplo de configuração para um modelo de destino, criado usando o ponto de extremidade da API `/destinations`. Consulte [criar uma configuração de destino](../authoring-api/destination-configuration/create-destination-configuration.md) para obter mais informações.

Para conectar o servidor e a configuração do modelo na etapa 1 a essa configuração de destino, adicione a ID da instância do servidor e a configuração do modelo como `destinationServerId` aqui.

>[!IMPORTANT]
>
>Para criar um destino em tempo real (streaming) configurado corretamente, você *deve* adicionar pelo menos uma identidade de destino em `identityNamespaces`, como mostrado abaixo. Se nenhuma identidade de destino estiver configurada, os usuários não poderão continuar após a [etapa de Mapeamento](../../ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação.

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
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

## Etapa 3: Criar modelo de transformação de mensagem - use a linguagem de modelo para especificar o formato de saída da mensagem {#create-transformation-template}

Com base nas cargas que seu destino aceita, você deve criar um modelo que transforme o formato dos dados exportados do formato XDM do Adobe em um formato compatível com seu destino. Consulte exemplos de modelo na seção [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de público-alvo](../functionality/destination-server/message-format.md#using-templating) e use a [ferramenta de criação de modelo](../testing-api/streaming-destinations/create-template.md) fornecida pela Adobe.

Depois de criar um template de transformação de mensagem que funcione para você, adicione-o ao servidor e à configuração de template criados na etapa 1.

```json {line-numbers="true" highlight="13-14"}
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## Etapa 4: criar configuração de metadados de público {#create-audience-metadata-configuration}

Para alguns destinos, o Destination SDK exige a definição de uma configuração de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo no destino de forma programática. Consulte [Gerenciamento de metadados de público-alvo](../functionality/audience-metadata-management.md) para obter informações sobre quando e como definir essa configuração.

Se você usar uma configuração de metadados de público, deverá conectá-la à configuração de destino criada na etapa 2. Adicione a ID da instância da configuração de metadados de público-alvo à configuração de destino como `audienceTemplateId`.

```json {line-numbers="true" highlight="53"}
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


## Etapa 5: configurar autenticação {#set-up-authentication}

Se você especificar `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` na configuração de destino acima, poderá configurar a autenticação para o seu destino usando o ponto de extremidade `/destination` ou `/credentials`.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` é a mais comum das duas regras de autenticação e é a que deve ser usada se você exigir que os usuários forneçam alguma forma de autenticação para o seu destino antes que eles possam configurar uma conexão e exportar dados.

Se você selecionou `"authenticationRule": "CUSTOMER_AUTHENTICATION"` na configuração de destino e seu destino oferece suporte ao método de autenticação OAuth 2, leia [Autenticação do OAuth 2](../functionality/destination-configuration/oauth2-authorization.md).

Se você selecionou `"authenticationRule": "PLATFORM_AUTHENTICATION"`, deve criar uma [configuração de credenciais](../credentials-api/create-credential-configuration.md) e passar a ID do objeto de credencial no parâmetro `authenticationId` na configuração de [entrega de destino](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication).

## Etapa 6: testar o destino {#test-destination}

Depois de configurar seu destino usando os pontos de extremidade de configuração nas etapas anteriores, você pode usar a [ferramenta de teste de destino](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) para testar a integração entre o Adobe Experience Platform e seu destino.

Como parte do processo para testar o destino, é necessário usar a interface do usuário do Experience Platform para criar segmentos, que você ativará para o destino. Consulte os dois recursos abaixo para obter instruções sobre como criar públicos-alvo no Experience Platform:

* [Criar uma página de documentação de público-alvo](/help/segmentation/ui/audience-portal.md#create-audience)
* [Criar uma apresentação de vídeo de público](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## Etapa 7: publicar seu destino {#publish-destination}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Depois de configurar e testar o destino, use a [API de publicação de destino](../publishing-api/create-publishing-request.md) para enviar a configuração à Adobe para revisão.

## Etapa 8: documentar seu destino {#document-destination}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Se você for um ISV (Fornecedor Independente de Software) ou um SI (Integrador de Sistemas) criando uma [integração de produtos](../overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](../docs-framework/documentation-instructions.md) para criar uma página de documentação de produto para seu destino no [catálogo de destinos do Experience Platform](/help/destinations/catalog/overview.md).

## Etapa 9: enviar destino para revisão da Adobe {#submit-for-review}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Por fim, antes que o destino possa ser publicado no catálogo do Experience Platform e ser visível a todos os clientes do Experience Platform, é necessário enviar oficialmente o destino para a revisão da Adobe. Encontre informações completas sobre como [enviar para revisão um destino produzido criado no Destination SDK](../guides/submit-destination.md).
