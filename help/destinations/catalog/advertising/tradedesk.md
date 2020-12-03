---
keywords: advertising; the trade desk;
title: O Destino do Trade Desk
seo-title: O Destino do Trade Desk
description: 'O Trade Desk é uma plataforma de autoatendimento para que os compradores de anúncios executem redirecionamentos e campanhas digitais direcionadas para audiência em fontes de vídeo, vídeo e inventário móvel. '
seo-description: O Trade Desk é uma plataforma de autoatendimento para que os compradores de anúncios executem redirecionamentos e campanhas digitais direcionadas para audiência em fontes de vídeo, vídeo e inventário móvel.
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# [!DNL The Trade Desk] destino

## Visão geral {#overview}

[!DNL The Trade Desk] o Destino ajuda a enviar dados do perfil para [!DNL The Trade Desk].

[!DNL The Trade Desk] é uma plataforma de autoatendimento para compradores de anúncios executarem redirecionamentos e audiências digitais direcionadas para exibição, vídeo e fontes de inventário móvel.

Para enviar dados de perfil para [!DNL The Trade Desk], primeiro conecte-se ao destino.

## Especificações de destino {#destination-specs}

Observe os seguintes detalhes específicos do [!DNL The Trade Desk] destino:

* Você pode enviar as seguintes [identidades](../../../identity-service/namespaces.md) para [!DNL The Trade Desk] destinos: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Casos de uso {#use-cases}

Como profissional de marketing, quero ser capaz de usar segmentos criados a partir de [!DNL Trade Desk IDs] ou IDs de dispositivo para criar redirecionamentos ou campanhas digitais direcionadas para a audiência.

## Tipo de exportação {#export-type}

**[!DNL Segment export]** - você está exportando todos os membros de um segmento (audiência) para o destino.

## Conectar ao destino {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL The Trade Desk]e selecione **[!UICONTROL Configurar]**.

![Configurar O Destino Do Trade Desk](../../assets/catalog/advertising/tradedesk/configure.png)

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativar]** e **[!UICONTROL Configurar]**, consulte a seção [Catálogo](../../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.
>
>![Ativar O Destino Do Trade Desk](../../assets/catalog/advertising/tradedesk/activate.png)

Na etapa [!UICONTROL Autenticação] , é necessário digitar os detalhes [!DNL The Trade Desk] da conexão:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID]** da conta: Sua ID [!DNL Trade Desk] de [!UICONTROL conta].
* **[!UICONTROL Segredo]** do cliente: O `clientSecret` parâmetro usado nas credenciais [!DNL OAuth2] do cliente.
* **[!UICONTROL Local]** do servidor: Pergunte ao seu [!DNL The Trade Desk] representante qual servidor regional você deve usar. Estes são os servidores regionais disponíveis que você pode escolher:

   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapura]**
   * **[!UICONTROL Tóquio]**
   * **[!UICONTROL América do Norte - Leste]**
   * **[!UICONTROL América do Norte - Oeste]**
   * **[!UICONTROL América Latina]**

* **[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte o [Data Governance na página do Adobe Experience Platform](../../../rtcdp/privacy/data-governance-overview.md#destinations) . Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](../../../data-governance/policies/overview.md#core-actions)dados.

![Etapa de autenticação do Trade Desk](../../assets/catalog/advertising/tradedesk/authenticate.png)

Clique em **[!UICONTROL Criar destino]**. Seu destino agora é criado. Você pode clicar em [!UICONTROL Salvar e sair] se quiser ativar segmentos posteriormente, ou selecionar [!UICONTROL Próximo] para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

Na etapa de programação [do](../../ui/activate-destinations.md#segment-schedule) segmento, é necessário mapear manualmente seus segmentos para a ID correspondente ou o nome amigável no destino.

Ao mapear segmentos, recomendamos que você use o nome do [!DNL Platform] segmento ou um formulário mais curto para facilitar o uso. No entanto, a ID ou o nome do segmento no destino não precisa corresponder ao da sua [!DNL Platform] conta. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

Se você estiver usando vários mapeamentos de dispositivo (IDs de cookie, [!DNL IDFA], [!DNL GAID]), certifique-se de usar o mesmo valor de mapeamento para todos os três mapeamentos. [!DNL The Trade Desk] agregação todos em um único segmento, com um detalhamento no nível do dispositivo.

![ID de mapeamento de segmento](../../assets/common/segment-mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o [!DNL The Trade Desk] destino, verifique sua [!DNL The Trade Desk] conta. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua conta.
