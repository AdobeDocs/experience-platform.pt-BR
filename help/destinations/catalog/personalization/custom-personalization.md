---
keywords: personalização personalizada; destino; destino personalizado da experience platform;
title: Conexão de personalização personalizada
description: Esse destino fornece personalização externa, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados em seu site para recuperar informações de segmento do Adobe Experience Platform. Esse destino fornece personalização em tempo real com base na associação de segmentos de perfis de usuários.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: fb79d0697244518cc713efeada7d017d64ce6214
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Conexão de personalização personalizada {#custom-personalization-connection}

## Visão geral {#overview}

Esse destino fornece uma maneira de recuperar informações do segmento do Adobe Experience Platform para plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados em sites do cliente.

## Pré-requisitos {#prerequisites}

Essa integração é alimentada pela variável [Adobe Experience Platform Web SDK](../../../edge/home.md) ou [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Você deve usar um desses SDKs para usar esse destino.

## Tipo de exportação {#export-type}

**Solicitação de perfil** - você está solicitando todos os segmentos que estão mapeados no destino de personalização personalizada para um único perfil. Diferentes destinos de personalização personalizada podem ser configurados para diferentes [Datastreams de coleta de dados do Adobe](../../../edge/fundamentals/datastreams.md).

## Casos de uso {#use-cases}

Esse destino compartilha públicos com servidores de anúncios e aplicativos de personalização que não sejam Adobe, a serem usados em tempo real, para decidir quais usuários de anúncios devem ver em um site.

### Caso de uso nº 1

**Personalização de uma página inicial**

Um site de aluguel doméstico e vendas deseja personalizar sua página inicial com base nas qualificações de segmento no Adobe Experience Platform. A empresa pode selecionar quais públicos-alvo devem obter uma experiência personalizada e mapeá-los para o destino de personalização personalizado que foi configurado para seu aplicativo de personalização que não é Adobe como critério de direcionamento.

**Anúncios no site direcionados**

Usando um destino de personalização personalizado separado para o servidor de publicidade, o mesmo site pode direcionar a publicidade no site usando um conjunto diferente de segmentos do Adobe Experience Platform como critérios de definição de metas.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
>
>Antes de criar uma conexão de personalização personalizada, recomendamos que você leia nosso guia sobre como [configurar destinos de personalização para a personalização da mesma página e da próxima página](../../ui/configure-personalization-destinations.md). Este guia o orienta pelas etapas de configuração necessárias para casos de uso de personalização de página mesma e próxima, em vários componentes de Experience Platform.

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Sobre IDs de fluxo de dados"
>abstract="Essa opção determina em qual conjunto de dados de coleta os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. Você deve configurar um armazenamento de dados antes de configurar seu destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Saiba como configurar um armazenamento de dados."

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **[!UICONTROL Alias de integração]**: Esse valor é enviado para o SDK da Web do Experience Platform como um nome de objeto JSON.
* **[!UICONTROL ID do fluxo de dados]**: Isso determina em qual conjunto de dados da Coleta de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. Consulte [Configurar um conjunto de dados](../../../edge/fundamentals/datastreams.md) para obter mais detalhes.

## Ativar segmentos para este destino {#activate}

Ler [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-profile-request-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

Se estiver usando [Tags no Adobe Experience Platform](../../../tags/home.md) para implantar o SDK da Web do Experience Platform, use o [enviar evento concluído](../../../edge/extension/event-types.md) e sua ação de código personalizado terá uma `event.destinations` que pode ser usada para ver os dados exportados.

Este é um exemplo de valor para a variável `event.destinations` variável:

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
