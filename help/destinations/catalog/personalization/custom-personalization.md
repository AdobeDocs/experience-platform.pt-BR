---
keywords: personalização personalizada, destino, destino personalizado da experience platform,
title: Conexão de personalização personalizada
description: Esse destino fornece personalização externa, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados no site uma maneira de recuperar informações de público-alvo do Adobe Experience Platform. Esse destino fornece personalização em tempo real com base na associação do público-alvo do perfil do usuário.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 9%

---


# Conexão de personalização personalizada {#custom-personalization-connection}

## Log de alterações de destino {#changelog}

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Maio de 2023 | Atualização de funcionalidade e documentação | A partir de maio de 2023, a **[!UICONTROL Personalização personalizada]** suporte para conexão [personalização baseada em atributos](../../ui/activate-edge-personalization-destinations.md#map-attributes) e está disponível para todos os clientes. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Os atributos do perfil podem conter dados confidenciais. Para proteger esses dados, a variável **[!UICONTROL Personalização personalizada]** o destino exige que você use o [API do servidor de rede de borda](/help/server-api/overview.md) ao configurar o destino para personalização baseada em atributo. Todas as chamadas à API do servidor devem ser feitas em um [contexto autenticado](../../../server-api/authentication.md).
>
><br>Se você já estiver usando o SDK da Web ou o SDK móvel para a integração, poderá recuperar atributos por meio da API do servidor adicionando uma integração do lado do servidor.
>
><br>Se você não seguir os requisitos acima, a personalização será baseada somente na associação ao público-alvo.

## Visão geral {#overview}

Esse destino fornece uma maneira de recuperar informações de público-alvo do Adobe Experience Platform para plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados nos sites do cliente.

## Pré-requisitos {#prerequisites}

Essa integração é viabilizada pelo [Adobe Experience Platform Web SDK](../../../edge/home.md) ou o [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Você deve usar um desses SDKs para usar esse destino.

>[!IMPORTANT]
>
>Antes de criar uma conexão de personalização personalizada, leia o guia sobre como [ativar dados do público-alvo para destinos de personalização de borda](../../ui/activate-edge-personalization-destinations.md). Este guia orienta você sobre as etapas de configuração necessárias para casos de uso de personalização de mesma página e próxima página, em vários componentes do Experience Platform.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve todos os públicos-alvo que você pode exportar para esse destino.

Esse destino suporta a ativação de todos os públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md).

*Além disso*, esse destino também suporta a ativação dos públicos-alvo descritos na tabela abaixo.

| Tipo de público | Descrição |
---------|----------|
| Uploads personalizados | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!DNL Profile request]** | Você está solicitando todos os públicos mapeados no destino de personalização personalizado para um único perfil. Diferentes destinos de personalização personalizados podem ser configurados para diferentes [Fluxos de dados de Coleção de dados do Adobe](../../../datastreams/overview.md). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

## Conectar ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Sobre IDs de sequências de dados"
>abstract="Essa opção determina em qual sequência de coleção de dados os públicos-alvo serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Você deve configurar uma sequência de dados de dados antes de configurar seu destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=pt-BR" text="Saiba como configurar uma sequência de dados"

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: digite uma descrição para o destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **[!UICONTROL Alias de integração]**: esse valor é enviado para o SDK da Web do Experience Platform como um nome de objeto JSON.
* **[!UICONTROL ID da sequência de dados]**: determina em qual sequência de dados de Coleção de dados os públicos-alvo serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Consulte [Configurar um fluxo de dados](../../../datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar destinos de personalização de borda de perfis e públicos](../../ui/activate-edge-personalization-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Dados exportados {#exported-data}

Se você estiver usando [Tags no Adobe Experience Platform](../../../tags/home.md) para implantar o SDK da Web do Experience Platform, use o [evento de envio concluído](../../../tags/extensions/client/web-sdk/event-types.md) e sua ação de código personalizado terá uma `event.destinations` que você pode usar para ver os dados exportados.

Este é um exemplo de valor para a variável `event.destinations` Variável:

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

Se você não estiver usando [Tags](../../../tags/home.md) para implantar o SDK da Web do Experience Platform, use o [tratamento de respostas de eventos](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) funcionalidade para ver os dados exportados.

A resposta JSON do Adobe Experience Platform pode ser analisada para encontrar o alias de integração correspondente do aplicativo que você está integrando com o Adobe Experience Platform. As IDs de público-alvo podem ser passadas para o código do aplicativo como parâmetros de direcionamento. Abaixo está uma amostra do que isso pareceria específico para a resposta de destino.

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Exemplo de resposta para [!UICONTROL Personalização personalizada com atributos]

Ao usar **[!UICONTROL Personalização personalizada com atributos]**, a resposta da API será semelhante ao exemplo abaixo.

A diferença entre **[!UICONTROL Personalização personalizada com atributos]** e **[!UICONTROL Personalização personalizada]** é a inclusão da `attributes` na resposta da API.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](../../../data-governance/home.md).
