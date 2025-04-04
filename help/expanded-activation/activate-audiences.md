---
title: Ativar públicos-alvo da Audience Manager por meio da Ativação expandida
description: Saiba como ativar públicos-alvo da Audience Manager para destinos sociais e de publicidade, por meio da Ativação estendida do Audience Manager.
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Ativar públicos-alvo por meio da Ativação expandida do Audience Manager

Esta página descreve o fluxo de trabalho completo que deve ser seguido para ativar públicos-alvo do Audience Manager para as plataformas de destino compatíveis com a Ativação expandida.

## Antes de começar {#before-you-begin}

As etapas descritas neste guia supõem que você tenha lido a [página de visão geral da Ativação expandida](overview.md) e confirmado que atende aos pré-requisitos para a ativação do público-alvo.

>[!IMPORTANT]
>
>Para ativar públicos-alvo por meio do [!DNL Expanded Activation], verifique se seus públicos-alvo da Audience Manager estão baseados em **endereços de email com hash**. Consulte os [pré-requisitos](overview.md#prerequisites) para obter mais detalhes.

## Etapa 1: configurar a conexão de origem do Audience Manager {#configure-source}

O [conector de origem do Audience Manager](../sources/connectors/adobe-applications/audience-manager.md) envia dados de público-alvo coletados no Adobe Audience Manager para ativação nas plataformas de destino com suporte da Ativação Expandida.

Siga o guia sobre como [criar uma conexão de origem do Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para configurar seu conector de origem.

![Imagem da interface do Experience Platform mostrando a guia Fontes com a conexão de origem do Audience Manager.](assets/sources-tab.png)

>[!TIP]
>
>O conector de origem do Adobe Audience Manager é o único conector de origem disponível na Ativação expandida.
>
>Para assimilar públicos com base em identificadores adicionais, compre uma edição do [Real-Time CDP](../rtcdp/overview.md). Entre em contato com seu representante da Adobe para obter mais detalhes.

### Exibir e monitorar públicos-alvo assimilados {#view-audiences}

Os públicos-alvo que você traz para a Ativação expandida do Audience Manager estão disponíveis para exibição no painel **[!UICONTROL Públicos-alvo]**.

Para exibir seus públicos-alvo, vá para **[!UICONTROL Cliente]** -> **[!UICONTROL Públicos-alvo]** -> **[!UICONTROL Procurar]**.

![Imagem da interface do Experience Platform mostrando a página Públicos-alvo.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* O Audiences pode levar até 48 horas para ser totalmente preenchido na Ativação expandida. Isso também se aplica a atualizações em públicos-alvo existentes da Audience Manager.
>* Os públicos-alvo do Audience Manager recém-criados não aparecem automaticamente na Ativação expandida. Para assimilar novos segmentos na Ativação expandida, você deve adicioná-los por meio do conector de origem do Audience Manager.

Após configurar o conector de origem do Audience Manager, vá para a [etapa 2](#create-destination-connection).

## Etapa 2: criar uma nova conexão de destino {#create-destination-connection}

Antes de enviar os públicos-alvo da Audience Manager para a plataforma de destino escolhida, é necessário criar uma conexão com a plataforma de destino.

Na barra lateral esquerda, vá para **[!UICONTROL Conexões]** -> **[!UICONTROL Destinos]** -> **[!UICONTROL Catálogo]**.

As categorias de destino disponíveis para [!DNL Expanded Activation] são [publicidade](../destinations/catalog/advertising/overview.md) e [social](../destinations/catalog/social/overview.md).

![Imagem da interface do Experience Platform mostrando o catálogo de destino para a Ativação Expandida.](assets/destination-catalog.png)

Para criar uma nova conexão com uma plataforma de destino, siga o guia em [como criar uma nova conexão de destino](../destinations/ui/connect-destination.md). Em seguida, vá para [etapa 3](#activate-audiences).

## Etapa 3: ativar públicos-alvo para o destino {#activate-audiences}

Depois de [assimilar públicos-alvo da Audience Manager](#configure-source) e [criar uma nova conexão de destino](#create-destination-connection) com êxito, você pode ativar os públicos-alvo para a plataforma de destino de sua escolha.

![Imagem da interface do Experience Platform mostrando o catálogo de destino para a Ativação Expandida.](assets/activate-audiences.png)

Para ativar públicos para o seu destino, siga o guia em [como ativar públicos para destinos de streaming](../destinations/ui/activate-segment-streaming-destinations.md).

## Verificar ativação de público {#verify}

Consulte a [documentação de monitoramento de destino](../dataflows/ui/monitor-destinations.md) para obter informações detalhadas sobre como monitorar o fluxo de dados para seus destinos.
