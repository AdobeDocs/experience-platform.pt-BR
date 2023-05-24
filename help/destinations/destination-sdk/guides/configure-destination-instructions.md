---
description: Esta página lista e descreve as etapas para configurar um destino de transmissão usando o Destination SDK.
title: Usar o Destination SDK para configurar um destino de transmissão
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Usar o Destination SDK para configurar um destino de transmissão

## Visão geral {#overview}

Esta página descreve como usar as informações em [Opções de configuração no SDK de destinos](../functionality/configuration-options.md) e em outros documentos de referência de API e funcionalidade de Destination SDK para configurar um [destino do streaming](../../destination-types.md#streaming-destinations). As etapas são apresentadas em ordem sequencial abaixo.

## Pré-requisitos {#prerequisites}

Antes de seguir para as etapas ilustradas abaixo, leia a [introdução ao Destination SDK](../getting-started.md) página para obter informações sobre como obter as credenciais de autenticação de Adobe I/O e outros pré-requisitos necessários para trabalhar com as APIs de Destination SDK. Isso pressupõe que você concluiu os pré-requisitos de parceria e permissão e está pronto para começar a desenvolver seu destino.

## Etapas para usar as opções de configuração no Destination SDK para configurar seu destino {#steps}

![Etapas ilustradas do uso de endpoints Destination SDK](../assets/guides/destination-sdk-steps.png)

## Etapa 1: criar uma configuração de servidor e modelo {#create-server-template-configuration}

Iniciar por [criação de uma configuração de servidor e modelo](../authoring-api/destination-server/create-destination-server.md) usando o `/destinations-server` terminal.

Veja abaixo um exemplo de configuração. Observe que o modelo de transformação de mensagem no campo `requestBody.value` é abordado na etapa 3, [Criar modelo de transformação](#create-transformation-template).

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

Veja abaixo um exemplo de configuração para um modelo de destino, criado usando o `/destinations` Endpoint da API. Consulte [criar uma configuração de destino](../authoring-api/destination-configuration/create-destination-configuration.md) para obter mais informações.

Para conectar o servidor e a configuração do modelo na etapa 1 a essa configuração de destino, adicione o ID da instância do servidor e a configuração do modelo como `destinationServerId` aqui.

>[!IMPORTANT]
>
>Para criar um destino em tempo real (transmissão) configurado corretamente, você *deve* adicionar pelo menos uma identidade de destino em `identityNamespaces`, conforme mostrado abaixo. Se nenhuma identidade de destino estiver configurada, os usuários não poderão continuar após a [Etapa de mapeamento](../../ui/activate-segment-streaming-destinations.md#mapping) do workflow de ativação.

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
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
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

Com base nas cargas que seu destino aceita, você deve criar um modelo que transforme o formato dos dados exportados do formato XDM do Adobe em um formato compatível com seu destino. Consulte exemplos de modelo na seção [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento](../functionality/destination-server/message-format.md#using-templating) e use o [ferramenta de criação de modelo](../testing-api/streaming-destinations/create-template.md) fornecido pela Adobe.

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

Para alguns destinos, o Destination SDK exige a definição de uma configuração de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo no destino de forma programática. Consulte [Gerenciamento de metadados de público](../functionality/audience-metadata-management.md) para obter informações sobre quando e como fazer essa configuração.

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
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
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

Dependendo de você especificar ou não `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` na configuração de destino acima, você pode definir a autenticação para seu destino usando o `/destination` ou o `/credentials` terminal.

Se você selecionou `"authenticationRule": "CUSTOMER_AUTHENTICATION"` na configuração de destino e seu destino for compatível com o método de autenticação OAuth 2, leia [Autenticação OAuth 2](../functionality/destination-configuration/oauth2-authentication.md).

Se você selecionou `"authenticationRule": "PLATFORM_AUTHENTICATION"`, você deve criar um [configuração de credenciais](../credentials-api/create-credential-configuration.md).

## Etapa 6: testar o destino {#test-destination}

Depois de definir seu destino usando os endpoints de configuração nas etapas anteriores, você pode usar o [ferramenta de teste de destino](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) para testar a integração entre o Adobe Experience Platform e o seu destino.

Como parte do processo para testar o destino, é necessário usar a interface do usuário do Experience Platform para criar segmentos, que você ativará para o destino. Consulte os dois recursos abaixo para obter instruções sobre como criar segmentos no Experience Platform:

* [Criar uma página de documentação de segmento](/help/segmentation/ui/overview.md#create-segment)
* [Criar uma apresentação de vídeo de segmento](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Etapa 7: publicar seu destino {#publish-destination}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Após configurar e testar o destino, use o [API de publicação de destino](../publishing-api/create-publishing-request.md) para enviar sua configuração ao Adobe para revisão.

## Etapa 8: documentar seu destino {#document-destination}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Se você for um ISV (Independent Software Vendor, Fornecedor independente de software) ou um SI (System Integrator, integrador de sistemas), crie um [integração produtiva](../overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](../docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para seu destino na [catálogo de destinos Experience Platform](/help/destinations/catalog/overview.md).

## Etapa 9: enviar destino para revisão do Adobe {#submit-for-review}

>[!NOTE]
>
>Esta etapa não é necessária se você estiver criando um destino privado para uso próprio e não estiver procurando publicá-lo no catálogo de destinos para que outros clientes usem.

Por fim, antes que o destino possa ser publicado no catálogo de Experience Platform e ser visível a todos os clientes de Experience Platform, é necessário enviar oficialmente o destino para revisão do Adobe. Encontre informações completas sobre como [enviar para revisão um destino produzido criado no Destination SDK](../guides/submit-destination.md).
