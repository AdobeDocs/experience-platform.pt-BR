---
keywords: personalização personalizada, destino, destino personalizado da experience platform,
title: Conexão de personalização personalizada
description: Esse destino fornece personalização externa, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados no site uma maneira de recuperar informações de segmento do Adobe Experience Platform. Esse destino fornece personalização em tempo real com base na associação do segmento do perfil do usuário.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 09e81093c2ed2703468693160939b3b6f62bc5b6
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 6%

---

# Conexão de personalização personalizada {#custom-personalization-connection}

## Log de alterações de destino {#changelog}

Com a versão beta do aprimorado **[!UICONTROL Personalização personalizada]** conector de destino, você poderá ver dois **[!UICONTROL Personalização personalizada]** no catálogo de destinos.

A variável **[!UICONTROL Personalização personalizada com atributos]** no momento, o conector está na versão beta e só está disponível para um número selecionado de clientes. Além da funcionalidade fornecida pelo **[!UICONTROL Personalização personalizada]**, o **[!UICONTROL Personalização personalizada com atributos]** O conector adiciona um [etapa de mapeamento](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) ao fluxo de trabalho de ativação, que permite mapear atributos de perfil para o destino de personalização personalizado, permitindo a personalização baseada em atributos de mesma página e próxima página.

>[!IMPORTANT]
>
>Os atributos do perfil podem conter dados confidenciais. Para proteger esses dados, a variável **[!UICONTROL Personalização personalizada com atributos]** o destino exige que você use o [API do servidor de rede de borda](/help/server-api/overview.md) para coleta de dados. Além disso, todas as chamadas à API do servidor devem ser feitas em um [contexto autenticado](../../../server-api/authentication.md).
>
>Se já estiver usando o SDK da Web ou o SDK móvel para a integração, você poderá recuperar atributos por meio da API do servidor de duas maneiras:
>
> * Adicione uma integração do lado do servidor que recupera atributos por meio da API do servidor.
> * Atualize sua configuração do lado do cliente com um código JavaScript personalizado para recuperar atributos por meio da API do servidor.
>
> Se você não seguir os requisitos acima, a personalização será baseada apenas na associação ao segmento, de forma idêntica à experiência oferecida pelo **[!UICONTROL Personalização personalizada]** conector.

![Imagem dos dois cartões de destino de Personalização personalizada em uma exibição lado a lado.](../../assets/catalog/personalization/custom-personalization/custom-personalization-side-by-side-view.png)

## Visão geral {#overview}

Esse destino fornece uma maneira de recuperar informações de segmento do Adobe Experience Platform para plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados nos sites do cliente.

## Pré-requisitos {#prerequisites}

Essa integração é viabilizada pelo [Adobe Experience Platform Web SDK](../../../edge/home.md) ou o [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Você deve usar um desses SDKs para usar esse destino.

>[!IMPORTANT]
>
>Antes de criar uma conexão de personalização personalizada, leia o guia sobre como [configurar destinos de personalização para personalização de mesma página e próxima página](../../ui/configure-personalization-destinations.md). Este guia orienta você sobre as etapas de configuração necessárias para casos de uso de personalização de mesma página e próxima página, em vários componentes do Experience Platform.

## Tipo e frequência de exportação {#export-type-frequency}

**Solicitação de perfil** - você está solicitando todos os segmentos mapeados no destino de personalização personalizado para um único perfil. Diferentes destinos de personalização personalizados podem ser configurados para diferentes [Fluxos de dados de Coleção de dados do Adobe](../../../edge/datastreams/overview.md).

## Casos de uso {#use-cases}

A variável [!DNL Custom Personalization Connection] O permite usar suas próprias plataformas de parceiros de personalização (por exemplo, [!DNL Optimizely], [!DNL Pega]), bem como sistemas proprietários (por exemplo, CMS interno), ao mesmo tempo em que aproveitam os recursos de coleta de dados e segmentação da Rede de borda do Experience Platform para potencializar uma experiência mais profunda de personalização do cliente.

Os casos de uso descritos abaixo incluem personalização do site e publicidade direcionada no site.

Para habilitar esses casos de uso, os clientes precisam de uma maneira rápida e simplificada de recuperar informações de segmento do Experience Platform e enviar essas informações para os sistemas designados que eles configuraram como conexões de personalização personalizadas na interface do usuário do Experience Platform.

Esses sistemas podem ser plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos executados nas propriedades da Web e móveis dos clientes.

### Personalização da mesma página {#same-page}

Um usuário visita uma página do site. O cliente pode usar as informações de visita da página atual (por exemplo, URL de referência, idioma do navegador, informações do produto incorporadas) para selecionar a próxima ação/decisão (por exemplo, personalização), usando a conexão de personalização personalizada para plataformas que não sejam Adobe (por exemplo, [!DNL Pega], [!DNL Optimizely], etc.).

### Personalização da próxima página {#next-page}

Um usuário visita a Página A em seu site. Com base nessa interação, o usuário se qualificou para um conjunto de segmentos. O usuário clica em um link que o leva da Página A para a Página B. Os segmentos para os quais o usuário se qualificou durante a interação anterior na Página A, juntamente com as atualizações de perfil determinadas pela visita atual ao site, serão usados para potencializar a próxima ação/decisão (por exemplo, qual banner de publicidade exibir para o visitante ou, no caso de testes A/B, qual versão da página exibir).

### Personalização da próxima sessão {#next-session}

Um usuário visita várias páginas do site. Com base nessas interações, o usuário se qualificou para um conjunto de segmentos. O usuário então encerra a sessão de navegação atual.

No dia seguinte, o usuário retorna ao mesmo site do cliente. Os segmentos para os quais eles se qualificaram durante a interação anterior com todas as páginas do site visitadas, juntamente com as atualizações de perfil determinadas pela visita atual do site, serão usados para selecionar a próxima ação/decisão (por exemplo, qual banner de publicidade exibir para o visitante ou, no caso de testes A/B, qual versão da página exibir).

## Conectar ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Sobre IDs de sequência de dados"
>abstract="Essa opção determina em qual sequência de coleção de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Você deve configurar uma sequência de dados de dados antes de configurar seu destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=br" text="Saiba como configurar uma sequência de dados"

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: digite uma descrição para o destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **[!UICONTROL Alias de integração]**: esse valor é enviado para o SDK da Web do Experience Platform como um nome de objeto JSON.
* **[!UICONTROL ID da sequência de dados]**: determina em qual sequência de dados de Coleção de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Consulte [Configurar um fluxo de dados](../../../edge/datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-profile-request-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

## Dados exportados {#exported-data}

Se você estiver usando [Tags no Adobe Experience Platform](../../../tags/home.md) para implantar o SDK da Web do Experience Platform, use o [evento de envio concluído](../../../edge/extension/event-types.md) e sua ação de código personalizado terá uma `event.destinations` que você pode usar para ver os dados exportados.

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

A resposta JSON do Adobe Experience Platform pode ser analisada para encontrar o alias de integração correspondente do aplicativo que você está integrando com o Adobe Experience Platform. As IDs de segmento podem ser transmitidas no código do aplicativo como parâmetros de direcionamento. Abaixo está uma amostra do que isso pareceria específico para a resposta de destino.

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
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
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
