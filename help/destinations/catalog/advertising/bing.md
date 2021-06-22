---
keywords: 'publicidade; bing; '
title: Conexão do Microsoft Bing
description: Com o destino de conexão do Microsoft Bing, você pode executar redirecionamento e campanhas digitais direcionadas ao público-alvo em todo o Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 2931efa6f67a042255fb1d31c0683f73d817b55b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Microsoft Bing] conexão  {#bing-destination}

## Visão geral {#overview}

O destino [!DNL Microsoft Bing] ajuda a enviar os dados do perfil para [!DNL Microsoft Display Advertising].

Para enviar dados de perfil para [!DNL Microsoft Bing], primeiro você deve se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, eu desejo poder usar segmentos criados a partir de [!DNL Microsoft Advertising IDs] para direcionar usuários por meio de publicidade de exibição em [!DNL Microsoft Advertising] canais.

## Identidades suportadas {#supported-identities}

[!DNL Microsoft Bing] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| MAID | ID de publicidade da Microsoft |

## Tipo de exportação {#export-type}

**[!DNL Segment Export]** - você está exportando todos os membros de um segmento (público-alvo) para o  [!DNL Microsoft Bing] destino.

## Pré-requisitos {#prerequisites}

Se você deseja criar seu primeiro destino com [!DNL Microsoft Bing] e não ativou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já havia configurado [!DNL Microsoft Bing] integrações no Audience Manager, as sincronizações de ID que você havia configurado continuam para a Platform.

Ao configurar o destino, você deve fornecer as seguintes informações:

* [!UICONTROL ID] da conta: este é seu  [!DNL Bing Ads CID], no formato inteiro.

## Conecte-se ao destino {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Microsoft Bing] e selecione **[!UICONTROL Configurar]**.

![Configurar o destino do Microsoft Bing](../../assets/catalog/advertising/bing/configure.png)

Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

![Ativar Destino do Microsoft Bing](../../assets/catalog/advertising/bing/activate.png)

## Etapa de autenticação {#authentication}

Na etapa **[!UICONTROL Authentication]**, você deve inserir os detalhes da conexão de destino:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID]** da conta: Seu  [!DNL Bing Ads CID].
* **[!UICONTROL Ação]** de marketing: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Governança de dados no Adobe Experience Platform](../../../data-governance/policies/overview.md) . Para obter informações sobre as ações de marketing individuais definidas pelo Adobe, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Autenticação de Destino do Microsoft Bing](../../assets/catalog/advertising/bing/authentication.png)

Clique em **[!UICONTROL Criar destino]**. Seu destino foi criado. Você pode clicar em [!UICONTROL Salvar e sair] se desejar ativar segmentos posteriormente, ou clicar em [!UICONTROL Próximo] para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

Na etapa [Agendamento do segmento](../../ui/activate-destinations.md#segment-schedule), você deve mapear manualmente os segmentos para a ID correspondente ou para o nome amigável no destino.

Ao mapear segmentos, recomendamos que você use o nome do segmento [!DNL Platform] ou uma forma mais curta dele, para facilitar o uso. No entanto, a ID do segmento ou o nome no seu destino não precisam corresponder àquela em sua conta [!DNL Platform]. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

![ID de mapeamento de segmento](../../assets/common/segment-mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Microsoft Bing], verifique sua conta [!DNL Microsoft Bing Ads]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.
