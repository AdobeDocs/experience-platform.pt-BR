---
keywords: personalização; target; destino; destinos de personalização; configurar destinos de personalização; mesma página; página seguinte;
title: Configurar destinos de personalização para a personalização da mesma página e da próxima página
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Saiba como configurar destinos de personalização para a personalização de mesma página e próxima página.
seo-description: Configure personalization destinations for same-page and next-page personalization.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: 851a9598523d26ba52a367f6c03e3c9612f6678b
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Configurar destinos de personalização para a personalização da mesma página e da próxima página

O Adobe Experience Platform usa [segmentação de borda](../../segmentation/ui/edge-segmentation.md) para permitir que os clientes criem e direcionem segmentos de público-alvo em alta escala, em tempo real.

Esse recurso ajuda a configurar casos de uso de personalização de página da mesma e da próxima página.

Este artigo fornece instruções passo a passo sobre como configurar o Experience Platform e seus destinos de personalização para esses casos de uso.

## Etapa 1: Configurar um armazenamento de dados na interface do usuário da coleta de dados {#configure-datastream}

A primeira etapa na configuração do destino de personalização é configurar um conjunto de dados para o SDK da Web do Experience Platform. Isso é feito na interface do usuário da coleta de dados.

Ao configurar o armazenamento de dados, em **[!UICONTROL Adobe Experience Platform]** certifique-se de que **[!UICONTROL Segmentação de borda]** e **[!UICONTROL Destinos de personalização]** são selecionadas.

![Configuração do fluxo de dados](../assets/ui/configure-personalization-destinations/datastream-config.png)

Para obter mais detalhes sobre como configurar um conjunto de dados, siga as instruções descritas em [Documentação do SDK da Web da plataforma](../../edge/fundamentals/datastreams.md).

## Etapa 2: Configurar o destino de personalização {#configure-destination}

Após configurar o armazenamento de dados, você pode começar a configurar o destino de personalização.

Siga as [tutorial de criação de conexão de destino](../ui/connect-destination.md) para obter instruções detalhadas sobre como criar uma nova conexão de destino.

Dependendo do destino que você estiver configurando, consulte os seguintes artigos para pré-requisitos específicos do destino e informações relacionadas:

* [Conexão Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [Conexão de personalização personalizada](../catalog/personalization/custom-personalization.md)

## Etapa 3: Crie um [!DNL Active-On-Edge] política de mesclagem {#create-merge-policy}

Após criar a conexão de destino, é necessário criar um [!DNL Active-On-Edge] política de mesclagem.

Siga as instruções em [criação de uma política de mesclagem](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)e certifique-se de ativar a variável **[!UICONTROL Política de Mesclagem Ativa On-Edge]** alternar.

## Etapa 4: Criar um novo segmento na Platform {#create-segment}

Depois de criar o [!DNL Active-On-Edge] política de mesclagem, você deve criar um novo segmento na Platform.

Siga as [construtor de segmentos](../../segmentation/ui/segment-builder.md) para criar seu novo segmento e [atribuí-la](../../segmentation/ui/segment-builder.md#merge-policies) o [!DNL Active-On-Edge] política de mesclagem criada na etapa 3.

## Etapa 5: Ativar o segmento para o seu destino

A última etapa do processo de configuração é ativar o segmento criado na etapa 4 para o destino criado na etapa 2.

Para fazer isso, siga estas [tutorial de ativação](../ui/activate-profile-request-destinations.md).

## Validar a configuração {#validate-configuration}

Depois de seguir com êxito as etapas acima, você deve ver seus novos segmentos no destino de personalização.
