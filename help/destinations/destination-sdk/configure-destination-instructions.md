---
description: Esta página lista e descreve as etapas para configurar um destino de transmissão usando o Destination SDK.
title: Usar o Destination SDK para configurar um destino de transmissão
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: b3d0f0c43b60895961cee2ee54518c0450e2e2f7
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# Usar o Destination SDK para configurar um destino de transmissão

## Visão geral {#overview}

Esta página descreve como usar as informações em [Opções de configuração no SDK de destinos](./configuration-options.md) e em outros documentos de referência da API e funcionalidade do Destination SDK para configurar um [destino de transmissão](/help/destinations/destination-types.md#streaming-destinations). As etapas são apresentadas na ordem sequencial abaixo.

>[!NOTE]
>
>No momento, não há suporte para configurar um destino em lote por meio do Destination SDK.

## Pré-requisitos {#prerequisites}

Antes de avançar para as etapas ilustradas abaixo, leia o [Introdução ao Destination SDK](./getting-started.md) para obter informações sobre como obter as credenciais de autenticação do Adobe I/O e outros pré-requisitos necessários para funcionar com as APIs do Destination SDK.

## Etapas para usar as opções de configuração no Destination SDK para configurar o destino {#steps}

![Etapas ilustradas do uso de pontos de extremidade do Destination SDK](./assets/destination-sdk-steps.png)

## Etapa 1: Criar um servidor e uma configuração de modelo {#create-server-template-configuration}

Comece criando uma configuração de servidor e modelo usando o `/destinations-server` endpoint (lido) [Referência da API](./destination-server-api.md)). Para obter mais informações sobre o servidor e a configuração do modelo, consulte [Especificações do servidor e do modelo](./configuration-options.md#server-and-template) na seção de referência.

Veja abaixo um exemplo de configuração. Observe que o modelo de transformação de mensagem no `requestBody.value` é abordado na etapa 3, [Criar modelo de transformação](./configure-destination-instructions.md#create-transformation-template).

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

Veja abaixo um exemplo de configuração para um modelo de destino, criado usando o `/destinations` Ponto de extremidade da API. Para obter mais informações sobre esse template, consulte [Configuração de destino](./destination-configuration.md).

Para conectar o servidor e a configuração do modelo na etapa 1 a essa configuração de destino, adicione a ID da instância da configuração do servidor e do modelo como `destinationServerId` aqui.

>[!IMPORTANT]
>
>Para criar um destino configurado corretamente, *must* adicionar pelo menos uma identidade de destino em `identityNamespaces`, conforme mostrado abaixo. Se nenhuma identidade de destino estiver configurada, os usuários não poderão continuar após a [Etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação.

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
   "segmentMappingConfig":{
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

Com base nas cargas que seu destino suporta, você deve criar um modelo que transforma o formato dos dados exportados do formato Adobe XDM em um formato compatível com seu destino. Consulte exemplos de modelo na seção [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento](./message-format.md#using-templating) e use o [ferramenta de criação de modelo](./create-template.md) fornecido pelo Adobe.

Depois de criar um template de transformação de mensagem que funcione para você, adicione-o à configuração de servidor e modelo criada na etapa 1.

## Etapa 4: Criar configuração de metadados de público-alvo {#create-audience-metadata-configuration}

Para alguns destinos, o Destination SDK exige que você configure uma configuração de metadados de público-alvo para criar, atualizar ou excluir públicos-alvo de forma programática no seu destino. Consulte [Gerenciamento de metadados do público-alvo](./audience-metadata-management.md) para obter informações sobre quando você precisa configurar essa configuração e como fazer isso.

Se você usar uma configuração de metadados de público-alvo, é necessário conectá-los à configuração de destino criada na etapa 2. Adicione a ID da instância da configuração de metadados do público-alvo à configuração de destino como `audienceTemplateId`.

## Etapa 5: Criar configuração de credenciais / Configurar autenticação {#set-up-authentication}

Dependendo de você especificar `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` na configuração de destino acima, você pode configurar a autenticação para seu destino usando o `/destination` ou `/credentials` endpoint .

* **Caso mais comum**: Se você selecionou `"authenticationRule": "CUSTOMER_AUTHENTICATION"` na configuração de destino e seu destino oferece suporte ao método de autenticação OAuth 2, leia [Autenticação OAuth 2](./oauth2-authentication.md).
* Se você selecionou `"authenticationRule": "PLATFORM_AUTHENTICATION"`, consulte o [Configuração de autenticação](./authentication-configuration.md#when-to-use).

## Etapa 6: Teste seu destino {#test-destination}

Depois de configurar seu destino usando os endpoints de configuração nas etapas anteriores, você pode usar a variável [ferramenta de teste de destino](./test-destination.md) para testar a integração entre o Adobe Experience Platform e seu destino.

Como parte do processo para testar seu destino, você deve usar a interface do usuário do Experience Platform para criar segmentos, que você ativará no seu destino. Consulte os dois recursos abaixo para obter instruções sobre como criar segmentos no Experience Platform:

* [Criar uma página de documentação do segmento](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Criar uma apresentação de vídeo de segmento](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Etapa 7: Publicar o destino {#publish-destination}

Após configurar e testar seu destino, use o [API de publicação de destino](./destination-publish-api.md) para enviar sua configuração ao Adobe para revisão.

## Etapa 8: Documente seu destino {#document-destination}

Se você for um Fornecedor Independente de Software (ISV) ou um Integrador de Sistema (SI) criando um [integração produzida](./overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](./docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para seu destino no [Catálogo de destinos Experience Platform](/help/destinations/catalog/overview.md).
