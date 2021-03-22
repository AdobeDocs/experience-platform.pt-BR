---
keywords: publicidade; o serviço de comércio;
title: A conexão com o Trade Desk
description: 'O Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de exibição, vídeo e inventário móvel. '
translation-type: tm+mt
source-git-commit: 24e0a274e61fcf6311c647067920686e4f25e840
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# [!DNL The Trade Desk] conexão

## Visão geral {#overview}

[!DNL The Trade Desk] ajuda a enviar dados do perfil para o  [!DNL The Trade Desk].

[!DNL The Trade Desk] O é uma plataforma de autoatendimento para compradores de anúncios executarem campanhas digitais direcionadas ao público-alvo por meio de exibição, vídeo e fontes de inventário móvel.

Para enviar dados de perfil para [!DNL Trade Desk], primeiro você deve se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, desejo poder usar segmentos criados a partir de [!DNL Trade Desk IDs] ou IDs de dispositivo para criar redirecionamento ou campanhas digitais direcionadas ao público-alvo.

## Identidades suportadas {#supported-identities}

[!DNL The Trade Desk] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| A ID do Trade Desk | ID do anunciante na plataforma do Trade Desk |

## Tipo de exportação {#export-type}

**[!DNL Segment export]** - você está exportando todos os membros de um segmento (público-alvo) para o destino.

## Pré-requisitos {#prerequisites}

Se você deseja criar seu primeiro destino com [!DNL The Trade Desk] e não ativou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já havia configurado [!DNL The Trade Desk] integrações no Audience Manager, as sincronizações de ID que você havia configurado continuam para a Platform.

## Conecte-se ao destino {#connect-destination}

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione [!DNL The Trade Desk] e selecione **[!UICONTROL Configure]**.

![Configurar O Destino Do Trade Desk](../../assets/catalog/advertising/tradedesk/configure.png)

Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Activate]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulte a seção [Catálogo](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

![Ativar O Destino Do Trade Desk](../../assets/catalog/advertising/tradedesk/activate.png)

## Etapa de autenticação {#authentication}

Na etapa **[!UICONTROL Authentication]**, é necessário inserir os detalhes da conexão [!DNL The Trade Desk]:

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Description]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Account ID]**: Seu [!DNL Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Pergunte ao seu  [!DNL Trade Desk] representante qual servidor regional você deve usar. Esses são os servidores regionais disponíveis que você pode escolher:

   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

* **[!UICONTROL Marketing action]**: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Governança de dados no Adobe Experience Platform](../../../data-governance/policies/overview.md) . Para obter informações sobre as ações de marketing individuais definidas pelo Adobe, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Etapa de Autenticação do Trade Desk](../../assets/catalog/advertising/tradedesk/authenticate.png)

Clique em **[!UICONTROL Create destination]**. Seu destino foi criado. Você pode clicar em [!UICONTROL Save & Exit] se desejar ativar segmentos posteriormente, ou selecionar [!UICONTROL Next] para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

Na etapa [Agendamento do segmento](../../ui/activate-destinations.md#segment-schedule), você deve mapear manualmente os segmentos para a ID correspondente ou para o nome amigável no destino.

Ao mapear segmentos, recomendamos que você use o nome do segmento [!DNL Platform] ou uma forma mais curta dele, para facilitar o uso. No entanto, a ID do segmento ou o nome no seu destino não precisam corresponder àquela em sua conta [!DNL Platform]. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

Se estiver usando vários mapeamentos de dispositivo (IDs de cookie, [!DNL IDFA], [!DNL GAID]), certifique-se de usar o mesmo valor de mapeamento para todos os três mapeamentos. [!DNL The Trade Desk] O agregará todos em um único segmento, com um detalhamento em nível de dispositivo.

![ID de mapeamento de segmento](../../assets/common/segment-mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL The Trade Desk], verifique sua conta [!DNL Trade Desk]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.
