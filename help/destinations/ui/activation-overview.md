---
keywords: ativar destinos;ativar dados;ativate destinations;ativate data
title: Visão geral de Activation
type: Tutorial
description: Saiba como ativar os públicos-alvo no Adobe Experience Platform para vários tipos de destinos.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# Visão geral de Activation

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

O Adobe Experience Platform é compatível com uma grande variedade de destinos. O fluxo de trabalho de ativação de público varia entre os destinos, com base no tipo de dados de público suportados e na frequência da exportação de dados.

## Métodos de ativação {#activation-methods}

Depois que você [configurar seu destino](connect-destination.md), você pode ativar públicos-alvo de várias maneiras:

### Ativar públicos-alvo do catálogo de destinos

Consulte os guias a seguir para obter informações detalhadas sobre como ativar públicos-alvo para o destino no catálogo de destinos:

* [Ativar dados do público-alvo para streaming de destinos de exportação de público](activate-segment-streaming-destinations.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil de transmissão](activate-streaming-profile-destinations.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](activate-batch-profile-destinations.md)

### Ativar públicos-alvo da [!UICONTROL Procurar] página

Siga as etapas abaixo para ativar dados para seus destinos no **[!UICONTROL Procurar]** página.

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Procurar]** guia.

   ![Guia Procurar](../assets/ui/activation-overview/browse-tab.png)

1. Localize a conexão de destino que deseja usar para ativar seus segmentos, selecione os três pontos no [!UICONTROL Nome] e selecione **[!UICONTROL Ativar públicos]**.

   ![Botão Ativar públicos](../assets/ui/activation-overview/activate-segments.png)

1. Dependendo do destino selecionado, siga as etapas descritas nos artigos abaixo, começando com a variável **[!UICONTROL Selecionar segmentos]** para concluir o fluxo de trabalho de ativação:

   * [Ativar dados do público-alvo para streaming de destinos de exportação de público](activate-segment-streaming-destinations.md)
   * [Ativar dados do público-alvo para destinos de exportação de perfil de transmissão](activate-streaming-profile-destinations.md)
   * [Ativar dados do público-alvo para destinos de exportação de perfil em lote](activate-batch-profile-destinations.md)

### Ativar públicos-alvo na página de detalhes do público-alvo {#activate-audience-details}

Você pode ativar públicos para destinos na página de detalhes do público. Consulte [Detalhes do público](../../segmentation/ui/audience-portal.md#audience-details) para obter mais informações.

Dependendo do destino selecionado, siga as etapas descritas nos artigos abaixo para concluir o fluxo de trabalho de ativação:

* [Ativar dados do público-alvo para streaming de destinos de exportação de público](activate-segment-streaming-destinations.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil de transmissão](activate-streaming-profile-destinations.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](activate-batch-profile-destinations.md)
