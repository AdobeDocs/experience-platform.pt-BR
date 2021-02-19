---
keywords: 'publicidade; bing; '
title: Conexão do Microsoft Bing
description: Com o destino da conexão do Microsoft Bing, você pode executar redirecionamento e audiência de campanhas digitais direcionadas através do Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# [!DNL Microsoft Bing] conexão  {#bing-destination}

O destino [!DNL Microsoft Bing] ajuda a enviar dados de perfil para [!DNL Microsoft Display Advertising].

Para enviar dados de perfil para [!DNL Microsoft Bing], primeiro conecte-se ao destino.

## Especificações de destino {#destination-specs}

Observe os seguintes detalhes específicos do destino [!DNL Microsoft Bing]:

* Você pode enviar as seguintes [identidades](../../../identity-service/namespaces.md) para [!DNL Microsoft Bing] destinos: [!DNL Microsoft ID].

## Casos de uso {#use-cases}

Como profissional de marketing, quero ser capaz de usar segmentos criados de [!DNL Microsoft Advertising IDs] para usuários do público alvo por meio de anúncios de exibição em canais [!DNL Microsoft Advertising].

## Tipo de exportação {#export-type}

**[!DNL Segment Export]** - você está exportando todos os membros de um segmento (audiência) para o  [!DNL Microsoft Bing] destino.

## Pré-requisitos {#prerequisites}

Ao configurar o destino, você será solicitado a fornecer as seguintes informações:

* [!UICONTROL ID] da conta: este é o seu  [!DNL Bing Ads CID], no formato inteiro.

## Conectar ao destino {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Microsoft Bing] e **[!UICONTROL Configurar]**.

![Configurar o Destino do Microsoft Bing](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.
>
>![Ativar o Destino do Microsoft Bing](../../assets/catalog/advertising/bing/activate.png)

Na etapa [!UICONTROL Authentication], você deve digitar os detalhes da conexão de destino:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID]** da conta: Seu  [!DNL Bing Ads CID].
* **[!UICONTROL Ação]** de marketing: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. É possível selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Data Governance no Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obter informações sobre as ações de marketing individuais definidas pelo Adobe, consulte [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Autenticação de Destino do Microsoft Bing](../../assets/catalog/advertising/bing/authentication.png)

Clique em **[!UICONTROL Criar destino]**. Seu destino agora é criado. Você pode clicar em [!UICONTROL Salvar e Sair] se quiser ativar segmentos posteriormente, ou clicar em [!UICONTROL Próximo] para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

Na etapa [Agendamento do segmento](../../ui/activate-destinations.md#segment-schedule), é necessário mapear manualmente seus segmentos para a ID correspondente ou o nome amigável no destino.

Ao mapear segmentos, recomendamos que você use o nome do segmento [!DNL Platform] ou uma forma mais curta dele, para facilitar o uso. No entanto, a ID do segmento ou o nome no destino não precisa corresponder àquela da sua conta [!DNL Platform]. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

![ID de mapeamento de segmento](../../assets/common/segment-mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Microsoft Bing], verifique sua conta [!DNL Microsoft Bing Ads]. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua conta.