---
keywords: personalização personalizada; destino; destino personalizado da experience platform;
title: Conexão de personalização personalizada
description: Esse destino fornece personalização externa, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados em seu site para recuperar informações de segmento do Adobe Experience Platform. Esse destino fornece personalização em tempo real com base na associação de segmentos de perfis de usuários.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 09e81093c2ed2703468693160939b3b6f62bc5b6
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 6%

---

# Conexão de personalização personalizada {#custom-personalization-connection}

## Log de alterações de destino {#changelog}

Com a versão beta do **[!UICONTROL Personalização personalizada]** conector de destino, você pode estar vendo dois **[!UICONTROL Personalização personalizada]** cartões no catálogo de destinos.

O **[!UICONTROL Personalização Personalizada Com Atributos]** no momento, o conector está em beta e só está disponível para um número selecionado de clientes. Além da funcionalidade fornecida pelo **[!UICONTROL Personalização personalizada]**, o **[!UICONTROL Personalização Personalizada Com Atributos]** adiciona um conector opcional [etapa de mapeamento](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) para o fluxo de trabalho de ativação, que permite mapear atributos de perfil para o destino de personalização personalizado, permitindo a personalização de mesma página e próxima página com base em atributos.

>[!IMPORTANT]
>
>Os atributos de perfil podem conter dados confidenciais. Para proteger esses dados, o **[!UICONTROL Personalização Personalizada Com Atributos]** O destino exige que você use a variável [API do Servidor de Rede de Borda](/help/server-api/overview.md) para coleta de dados. Além disso, todas as chamadas da API do servidor devem ser feitas em um [contexto autenticado](../../../server-api/authentication.md).
>
>Se você já estiver usando o SDK da Web ou o SDK móvel para sua integração, poderá recuperar atributos por meio da API do servidor de duas formas:
>
> * Adicione uma integração do lado do servidor que recupera atributos por meio da API do servidor.
> * Atualize sua configuração do lado do cliente com um código Javascript personalizado para recuperar atributos por meio da API do servidor.
>
> Se você não seguir os requisitos acima, a personalização será baseada somente na associação de segmentos, idêntica à experiência oferecida pela **[!UICONTROL Personalização personalizada]** conector.

![Imagem dos dois cartões de destino de personalização personalizados em uma exibição lado a lado.](../../assets/catalog/personalization/custom-personalization/custom-personalization-side-by-side-view.png)

## Visão geral {#overview}

Esse destino fornece uma maneira de recuperar informações do segmento do Adobe Experience Platform para plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados em sites do cliente.

## Pré-requisitos {#prerequisites}

Essa integração é alimentada pela variável [Adobe Experience Platform Web SDK](../../../edge/home.md) ou [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Você deve usar um desses SDKs para usar esse destino.

>[!IMPORTANT]
>
>Antes de criar uma conexão de personalização personalizada, leia o guia sobre como [configurar destinos de personalização para a personalização da mesma página e da próxima página](../../ui/configure-personalization-destinations.md). Este guia o orienta pelas etapas de configuração necessárias para casos de uso de personalização de página mesma e próxima, em vários componentes de Experience Platform.

## Tipo e frequência de exportação {#export-type-frequency}

**Solicitação de perfil** - você está solicitando todos os segmentos que estão mapeados no destino de personalização personalizada para um único perfil. Diferentes destinos de personalização personalizada podem ser configurados para diferentes [Datastreams de coleta de dados do Adobe](../../../edge/datastreams/overview.md).

## Casos de uso {#use-cases}

O [!DNL Custom Personalization Connection] permite usar suas próprias plataformas de parceiros de personalização (por exemplo, [!DNL Optimizely], [!DNL Pega]), bem como sistemas proprietários (por exemplo, CMS interno), além de aproveitar os recursos de coleta e segmentação de dados da rede Experience Platform Edge para potencializar uma experiência mais profunda de personalização do cliente.

Os casos de uso descritos abaixo incluem personalização de site e publicidade direcionada no site.

Para ativar esses casos de uso, os clientes precisam de uma maneira rápida e simplificada de recuperar informações de segmento do Experience Platform e enviar essas informações para seus sistemas designados, configurados como conexões de personalização personalizadas na interface do usuário do Experience Platform.

Esses sistemas podem ser plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos em execução nas propriedades móveis e da Web dos clientes.

### Personalização de mesma página {#same-page}

Um usuário visita uma página de seu site. O cliente pode usar as informações de visita da página atual (por exemplo, URL de referência, idioma do navegador, informações de produto incorporadas) para selecionar a próxima ação/decisão (por exemplo, personalização), usando a conexão de personalização personalizada para plataformas que não sejam Adobe (por exemplo, [!DNL Pega], [!DNL Optimizely], etc.).

### Personalização de próxima página {#next-page}

Um usuário visita a Página A em seu site. Com base nessa interação, o usuário se qualificou para um conjunto de segmentos. O usuário então clica em um link que os leva da Página A para a Página B. Os segmentos para os quais o usuário se qualificou durante a interação anterior na Página A, juntamente com as atualizações de perfil determinadas pela visita atual ao site, serão usados para potencializar a próxima ação/decisão (por exemplo, que banner de anúncio exibir para o visitante ou, no caso de testes A/B, qual versão da página será exibida).

### Personalização da próxima sessão {#next-session}

Um usuário visita várias páginas em seu site. Com base nessas interações, o usuário se qualificou para um conjunto de segmentos. O usuário finaliza a sessão de navegação atual.

No dia seguinte, o usuário retorna ao mesmo site do cliente. Os segmentos para os quais eles se qualificaram durante a interação anterior com todas as páginas do site visitadas, juntamente com as atualizações de perfil determinadas pela visita atual ao site, serão usados para selecionar a próxima ação/decisão (por exemplo, que banner de anúncio exibir para o visitante ou, no caso de testes A/B, qual versão da página exibir).

## Conecte-se ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Sobre IDs de sequência de dados"
>abstract="Essa opção determina em qual sequência de coleção de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Você deve configurar uma sequência de dados de dados antes de configurar seu destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=br" text="Saiba como configurar uma sequência de dados"

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **[!UICONTROL Alias de integração]**: Esse valor é enviado para o SDK da Web do Experience Platform como um nome de objeto JSON.
* **[!UICONTROL ID do fluxo de dados]**: Isso determina em qual conjunto de dados da Coleta de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Consulte [Configurar um conjunto de dados](../../../edge/datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

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

### Exemplo de resposta para [!UICONTROL Personalização Personalizada Com Atributos]

Ao usar **[!UICONTROL Personalização Personalizada Com Atributos]**, a resposta da API será semelhante ao exemplo abaixo.

A diferença entre **[!UICONTROL Personalização Personalizada Com Atributos]** e **[!UICONTROL Personalização personalizada]** é a inclusão do `attributes` na resposta da API.

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

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](../../../data-governance/home.md).
