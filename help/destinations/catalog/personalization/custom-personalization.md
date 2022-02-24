---
keywords: custom personalization; destination; experience platform custom destination;
title: Custom personalization connection
description: This destination provides external personalization, content management systems, ad servers, and other applications that are running on your site a way to retrieve segment information from Adobe Experience Platform. This destination provides real-time personalization based on user profile segment membership.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: a990e829c8ba034f31b883360495513f3f5b4cfc
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# Custom personalization connection {#custom-personalization-connection}

## Visão geral {#overview}

Esse destino fornece uma maneira de recuperar informações do segmento do Adobe Experience Platform para plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados em sites do cliente.

## Pré-requisitos {#prerequisites}

This integration is powered by the [Adobe Experience Platform Web SDK](../../../edge/home.md) or the [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). You must be using one of these SDKs to use this destination.

>[!IMPORTANT]
>
>Antes de criar uma conexão de personalização personalizada, leia o guia sobre como [configurar destinos de personalização para a personalização da mesma página e da próxima página](../../ui/configure-personalization-destinations.md). Este guia o orienta pelas etapas de configuração necessárias para casos de uso de personalização de página mesma e próxima, em vários componentes de Experience Platform.

## Tipo de exportação {#export-type}

**Profile request** - you are requesting all the segments that are mapped in the custom personalization destination for a single profile. Diferentes destinos de personalização personalizada podem ser configurados para diferentes [Datastreams de coleta de dados do Adobe](../../../edge/fundamentals/datastreams.md).

## Casos de uso {#use-cases}

This destination shares audiences with ad servers and non-Adobe personalization applications, to be used in real-time, for deciding which advertisement users should see on a website.

### Caso de uso nº 1

**Personalização de uma página inicial**

A home rental and sales website wants to personalize their home page based on segment qualifications in Adobe Experience Platform. The company can select what audiences should get a personalized experience and map those to the custom personalization destination that had been set up for their non-Adobe personalization application as targeting criteria.

**Anúncios no site direcionados**

Usando um destino de personalização personalizado separado para o servidor de publicidade, o mesmo site pode direcionar a publicidade no site usando um conjunto diferente de segmentos do Adobe Experience Platform como critérios de definição de metas.

## Conecte-se ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Sobre IDs de fluxo de dados"
>abstract="Essa opção determina em qual conjunto de dados de coleta os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. You must configure a datastream before you can configure your destination."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Learn how to configure a datastream."

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

While [setting up](../../ui/connect-destination.md) this destination, you must provide the following information:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **[!UICONTROL Integration alias]**: This value is sent to the Experience Platform Web SDK as a JSON object name.
* **[!UICONTROL ID do fluxo de dados]**: Isso determina em qual conjunto de dados da Coleta de dados os segmentos serão incluídos na resposta à página. The drop-down menu shows only datastreams that have the destination configuration enabled. Consulte [Configurar um conjunto de dados](../../../edge/fundamentals/datastreams.md) para obter mais detalhes.

## Activate segments to this destination {#activate}

Read [Activate profiles and segments to profile request destinations](../../ui/activate-profile-request-destinations.md) for instructions on activating audience segments to this destination.

## Dados exportados {#exported-data}

Se estiver usando [Tags no Adobe Experience Platform](../../../tags/home.md) para implantar o SDK da Web do Experience Platform, use o [enviar evento concluído](../../../edge/extension/event-types.md) e sua ação de código personalizado terá uma `event.destinations` que pode ser usada para ver os dados exportados.

Here is a sample value for the `event.destinations` variable:

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

Se você não estiver usando [Tags](../../../tags/home.md) para implantar o SDK da Web do Experience Platform, use o [tratamento de respostas de eventos](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) para ver os dados exportados.

A resposta JSON do Adobe Experience Platform pode ser analisada para encontrar o alias de integração correspondente do aplicativo que você está integrando com o Adobe Experience Platform. As IDs de segmento podem ser passadas para o código do aplicativo como parâmetros de direcionamento. Abaixo está uma amostra de como isso pareceria específico para a resposta de destino.

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](../../../data-governance/home.md).
