---
keywords: ativar destinos; ativar dados
title: Visão geral de Activation
type: Tutorial
seo-title: Activation overview
description: Saiba como ativar os dados do público-alvo que você tem no Adobe Experience Platform para vários tipos de destinos.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform to various types of destinations.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: f4ae6831569e8a5b458c42f76810212174f04811
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# Visão geral de Activation

O Adobe Experience Platform é compatível com uma grande variedade de destinos. O fluxo de trabalho de ativação do público-alvo varia entre os destinos, com base no tipo de dados de público-alvo suportados por eles e na frequência da exportação de dados.

## Métodos de ativação {#activation-methods}

Depois de [configurar o destino](connect-destination.md), é possível ativar segmentos de público-alvo de várias maneiras:

### Ativar públicos-alvo do catálogo de destinos

Consulte os guias a seguir para obter informações detalhadas sobre como ativar públicos-alvo para seu destino a partir do catálogo de destinos:

* [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](activate-segment-streaming-destinations.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](activate-streaming-profile-destinations.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](activate-batch-profile-destinations.md)

### Ativar públicos-alvo da [!UICONTROL Procurar] página

Siga as etapas abaixo para ativar os dados para seus destinos do **[!UICONTROL Procurar]** página.

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione o **[!UICONTROL Procurar]** guia .

   ![Guia Procurar](../assets/ui/activation-overview/browse-tab.png)

1. Encontre a conexão de destino que deseja usar para ativar seus segmentos, selecione os três pontos na [!UICONTROL Nome] e selecione **[!UICONTROL Ativar segmentos]**.

   ![Botão Ativar segmentos](../assets/ui/activation-overview/activate-segments.png)

1. Dependendo do destino selecionado, siga as etapas descritas nos artigos abaixo, começando com **[!UICONTROL Selecionar segmentos]** para concluir o fluxo de trabalho de ativação:

   * [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](activate-segment-streaming-destinations.md)
   * [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](activate-streaming-profile-destinations.md)
   * [Ativar dados do público-alvo para destinos de exportação de perfil em lote](activate-batch-profile-destinations.md)

### Ativar públicos-alvo da página de detalhes do segmento {#activate-segment-details}

Você pode ativar segmentos para destinos a partir da página de detalhes do segmento. Consulte [Detalhes do segmento](../../segmentation/ui/overview.md#segment-details) para obter mais informações.

Dependendo do destino selecionado, siga as etapas descritas nos artigos abaixo para concluir o fluxo de trabalho de ativação:

* [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](activate-segment-streaming-destinations.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](activate-streaming-profile-destinations.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](activate-batch-profile-destinations.md)
