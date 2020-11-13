---
keywords: advertising; bing;
title: Destino do Microsoft Bing
seo-title: O destino do Microsoft Bing ajuda a enviar dados do perfil para o Microsoft Display Advertising.
description: Com o destino do Microsoft Bing, você pode executar redirecionamento e audiência de campanhas digitais direcionadas através do Microsoft Display Advertising.
seo-description: Com o destino do Microsoft Bing, você pode executar redirecionamento e audiência de campanhas digitais direcionadas através do Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: 979256ea975dcc0c1f6c59792b70d6899ee11376
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# [!DNL Microsoft Bing] destino

## Visão geral {#overview}

O [!DNL Microsoft Bing] destino ajuda a enviar dados do perfil para [!DNL Microsoft Display Advertising].

Para enviar dados de perfil para [!DNL Microsoft Bing], primeiro conecte-se ao destino.

## Especificações de destino {#destination-specs}

Observe os seguintes detalhes específicos do [!DNL Microsoft Bing] destino:

* Você pode enviar as seguintes [identidades](../../identity-service/namespaces.md) para [!DNL Microsoft Bing] destinos: [!DNL Microsoft ID].

## Casos de uso {#use-cases}

Como profissional de marketing, quero ser capaz de usar segmentos integrados [!DNL Microsoft Advertising IDs] a usuários de públicos alvos por meio de anúncios de exibição em [!DNL Microsoft Advertising] canais.

## Tipo de exportação {#export-type}

**[!DNL Segment Export]** - você está exportando todos os membros de um segmento (audiência) para o [!DNL Microsoft Bing] destino.

## Pré-requisitos {#prerequisites}

Ao configurar o destino, você será solicitado a fornecer as seguintes informações:

* [!UICONTROL ID]da conta: este é o seu [!DNL Bing Ads CID], no formato inteiro.

## Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Microsoft Bing]e selecione **[!UICONTROL Configurar]**.

   ![Configurar o Destino do Microsoft Bing](assets/bing-destination-configure.png)

   >[!NOTE]
   >
   >Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativar]** e **[!UICONTROL Configurar]**, consulte a seção [Catálogo](../destinations/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.
   >
   >![Ativar o Destino do Microsoft Bing](assets/bing-destination-activate.png)

1. Na etapa [!UICONTROL Autenticação] , você deve digitar os detalhes da conexão de destino:

   * **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
   * **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
   * **[!UICONTROL ID]** da conta: Seu [!DNL Bing Ads CID].
   * **[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte o [Data Governance na página do Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](../../data-governance/policies/overview.md#core-actions)dados.

   ![Autenticação de Destino do Microsoft Bing](assets/bing-destination-authentication.png)

1. Clique em **[!UICONTROL Criar destino]**. Seu destino agora é criado. Você pode clicar em [!UICONTROL Salvar e sair] se quiser ativar segmentos posteriormente ou clicar em [!UICONTROL Avançar] para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

Durante a etapa de agendamento [do](activate-destinations.md#segment-schedule) segmento, é necessário mapear manualmente seus segmentos para a ID correspondente ou o nome amigável no destino.

Ao mapear segmentos, recomendamos que você use o nome do [!DNL Platform] segmento ou um formulário mais curto para facilitar o uso. No entanto, a ID ou o nome do segmento no destino não precisa corresponder ao da sua [!DNL Platform] conta. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

![ID de mapeamento de segmento](assets/segment-mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o [!DNL Microsoft Bing] destino, verifique sua [!DNL Microsoft Bing Ads] conta. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua conta.