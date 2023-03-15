---
keywords: personalização, target, destino, personalização de destinos, configurar destinos de personalização, mesma página, próxima página,
title: Configurar destinos de personalização para personalização de mesma página e próxima página
type: Tutorial
description: Saiba como configurar destinos de personalização para personalização de mesma página e próxima página.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Configurar destinos de personalização para personalização de mesma página e próxima página

## Visão geral {#overview}

>[!NOTE]
>
>Quando [configuração da conexão do Adobe Target](../catalog/personalization/adobe-target-connection.md) sem usar uma ID de fluxo de dados, os casos de uso descritos neste artigo não são compatíveis.

O Adobe Experience Platform usa [segmentação de borda](../../segmentation/ui/edge-segmentation.md) para permitir que os clientes criem e direcionem segmentos de público em alta escala, em tempo real.

Esse recurso ajuda a configurar casos de uso de personalização de mesma página e próxima página.

Este artigo fornece instruções passo a passo sobre como configurar o Experience Platform e seus destinos de personalização para esses casos de uso.

Além disso, assista ao vídeo abaixo para obter uma visão geral do processo de configuração completo.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter mudado desde a gravação deste vídeo. Para obter as informações mais atualizadas, consulte as etapas de configuração descritas nas seções abaixo.

## Etapa 1: configurar um fluxo de dados na interface da Coleção de dados {#configure-datastream}

A primeira etapa na configuração do destino de personalização é configurar um fluxo de dados para o SDK da Web do Experience Platform. Isso é feito na interface da Coleção de dados.

Ao configurar o fluxo de dados, em **[!UICONTROL Adobe Experience Platform]** verifique se ambos **[!UICONTROL Segmentação de borda]** e **[!UICONTROL Destinos de personalização]** são selecionados.

![Configuração da sequência de dados](../assets/ui/configure-personalization-destinations/datastream-config.png)

Para obter mais detalhes sobre como configurar um fluxo de dados, siga as instruções descritas em [Documentação do SDK da Web da Platform](../../edge/datastreams/overview.md).

## Etapa 2: configurar seu destino de personalização {#configure-destination}

Após configurar o fluxo de dados, você pode começar a configurar o destino de personalização.

Siga as [tutorial de criação de conexão de destino](../ui/connect-destination.md) para obter instruções detalhadas sobre como criar uma nova conexão de destino.

Dependendo do destino que você estiver configurando, consulte os seguintes artigos para obter os pré-requisitos específicos do destino e informações relacionadas:

* [Conexão com o Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [Conexão de personalização personalizada](../catalog/personalization/custom-personalization.md)

## Etapa 3: criar um [!DNL Active-On-Edge] política de mesclagem {#create-merge-policy}

Depois de criar a conexão de destino, você deve criar um [!DNL Active-On-Edge] política de mesclagem.

Siga as instruções em [criação de uma política de mesclagem](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)e certifique-se de ativar o **[!UICONTROL Política de mesclagem ativa na borda]** alternar.

## Etapa 4: criar um novo segmento na Platform {#create-segment}

Depois de criar o [!DNL Active-On-Edge] política de mesclagem, você deve criar um novo segmento na Platform.

Siga as [construtor de segmentos](../../segmentation/ui/segment-builder.md) guia para criar seu novo segmento e certifique-se de [atribuir](../../segmentation/ui/segment-builder.md#merge-policies) o [!DNL Active-On-Edge] política de mesclagem criada na etapa 3.

## Etapa 5: ative o segmento para seu destino

A última etapa do processo de configuração é ativar o segmento criado na etapa 4 para o destino criado na etapa 2.

Para fazer isso, siga este [tutorial de ativação](../ui/activate-profile-request-destinations.md).

## Validar a configuração {#validate-configuration}

Depois de seguir as etapas acima com êxito, você deve ver seus novos segmentos no destino de personalização.
