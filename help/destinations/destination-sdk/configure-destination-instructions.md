---
description: Esta página descreve como usar as informações de referência nas opções de Configuração do SDK de Destinos para configurar seu destino usando o SDK de destino.
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: Como usar o SDK de destino para configurar o destino
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 32b61276f3fe81ffa82fec1debf335ea51020ccd
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Como usar o SDK de destino para configurar o destino

## Visão geral {#overview}

Esta página descreve como usar as informações de referência em [Opções de configuração no SDK de destinos](./configuration-options.md) para configurar o destino. As etapas são apresentadas na ordem sequencial abaixo.

## Pré-requisitos {#prerequisites}

Antes de seguir para as etapas ilustradas abaixo, leia a página [SDK de destino que começa](./getting-started.md) para obter informações sobre como obter as credenciais de autenticação do Adobe I/O necessárias e outros pré-requisitos para funcionar com APIs de SDK de destino.

## Etapas para usar as opções de configuração no SDK de destino para configurar o destino {#steps}

![Etapas ilustradas do uso de endpoints do SDK de destino](./assets/destination-sdk-steps.png)

## Etapa 1: Criar um servidor e uma configuração de modelo {#create-server-template-configuration}

Comece criando um servidor e uma configuração de modelo usando o ponto de extremidade `/destinations-server` (leia [Referência da API](./destination-server-api.md)). Para obter mais informações sobre a configuração do servidor e do modelo, consulte [Especificações do servidor e do modelo](./configuration-options.md#server-and-template) na seção de referência.

Veja abaixo um exemplo de configuração. Observe que o modelo de transformação de mensagem no parâmetro `requestBody.value` é abordado na etapa 3, [Criar modelo de transformação](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

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

Veja abaixo um exemplo de configuração para um modelo de destino, criado usando o ponto de extremidade da API `/destinations`. Para obter mais informações sobre esse template, consulte [Configuração de destino](./destination-configuration.md).

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
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
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
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

Com base nas cargas que seu destino suporta, você deve criar um modelo que transforma o formato dos dados exportados do formato Adobe XDM em um formato compatível com seu destino. Consulte exemplos de modelo na seção [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento](./message-format.md#using-templating) e use a [ferramenta de criação de modelo](./create-template.md) fornecida pelo Adobe.

## Etapa 4: Criar configuração de metadados de público-alvo {#create-audience-metadata-configuration}

Para alguns destinos, o SDK de destino requer a configuração de um modelo de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo de forma programática no destino. Consulte [Gerenciamento de metadados de público-alvo](./audience-metadata-management.md) para obter informações sobre quando você precisa configurar essa configuração e como fazer isso.

## Etapa 5: Criar configuração de credenciais / Configurar autenticação {#set-up-authentication}

Dependendo de você especificar `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` na configuração de destino acima, é possível configurar a autenticação para seu destino usando o ponto de extremidade `/destination` ou `/credentials`.

* **Caso** mais comum: Se você selecionou  `"authenticationRule": "CUSTOMER_AUTHENTICATION"` e seu destino oferecer suporte ao método de autenticação OAuth 2, leia autenticação  [OAuth 2](./oauth2-authentication.md).
* Se você selecionou `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulte [Configuração de credenciais](./credentials-configuration.md) na documentação de referência.

## Etapa 6: Teste seu destino {#test-destination}

Depois de configurar seu destino usando os modelos nas etapas anteriores, você pode usar a [ferramenta de teste de destino](./create-template.md) para testar a integração entre o Adobe Experience Platform e seu destino.

Como parte do processo para testar seu destino, você deve usar a interface do usuário do Experience Platform para criar segmentos, que você ativará no seu destino. Consulte os dois recursos abaixo para obter instruções sobre como criar segmentos no Experience Platform:

* [Criar uma página de documentação do segmento](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Criar uma apresentação de vídeo de segmento](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## Etapa 7: Publicar o destino {#publish-destination}

Após configurar e testar seu destino, use a [API de publicação de destino](./destination-publish-api.md) para enviar sua configuração ao Adobe para revisão.

## Etapa 8: Documente seu destino {#document-destination}

Se você for um Fornecedor de Software Independente (ISV) ou Integrador de Sistema (SI) criando um [integração produtizada](./overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](./docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para seu destino no [catálogo de destinos do Experience League](/help/destinations/catalog/overview.md).
