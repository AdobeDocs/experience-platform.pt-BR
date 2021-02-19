---
keywords: gerenciador de publicidade do google;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Gerenciador de publicidade do Google
title: Conexão com o Google Ad Manager
description: 'O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de serviço de anúncios do Google que oferece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e em aplicativos móveis.  '
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---


# [!DNL Google Ad Manager] conexão

[!DNL Google Ad Manager], anteriormente conhecida como  [!DNL DoubleClick] para editores ou  [!DNL DoubleClick AdX], é uma plataforma de veiculação de anúncios  [!DNL Google] que oferece aos editores os meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e em aplicativos móveis.

## Especificações de destino

Observe os seguintes detalhes que são específicos para [!DNL Google Ad Manager] destinos:

* Você pode enviar as seguintes [identidades](../../../identity-service/namespaces.md) para [!DNL Google Ads] destinos: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), ID de cookie do Google, IDFA, GAID, Roku IDs, Microsoft IDs e Amazon Fire TV IDs.
   * O Google usará [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para usuários públicos alvos na Califórnia e a ID de cookie do Google para todos os outros usuários.
* As audiências ativadas são criadas programaticamente na plataforma [!DNL Google].
* A plataforma não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de audiências no Google para validar a integração e entender o tamanho da definição de metas de audiência.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com [!DNL Google Ad Manager] e não tiver ativado a funcionalidade de [sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de ID de Experience Cloud no passado (com Audience Manager ou outros aplicativos), entre em contato com a Consultoria de Adobe ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente as integrações [!DNL Google] no Audience Manager, a ID será sincronizada se você tiver configurado o transporte para a Plataforma.

### Tipo de exportação {#export-type}

**Exportação**  de segmentos - você está exportando todos os membros de um segmento (audiência) para o destino do Google.

## Pré-requisitos

### Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro [!DNL Google Ad Manager] destino na Plataforma. Verifique se o processo de lista de permissões descrito abaixo foi concluído por [!DNL Google] antes de criar um destino.

Antes de criar o destino [!DNL Google Ad Manager] na Plataforma, você deve entrar em contato com [!DNL Google] para que a Adobe seja colocada na lista de provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Entre em contato com [!DNL Google] e forneça as seguintes informações:

* **ID**  da conta: esta é a ID da conta Adobe com  [!DNL Google]. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante de Adobe para obter essa ID.
* **ID**  do cliente: esta é a ID da conta do cliente com  [!DNL Google]. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante de Adobe para obter essa ID.
* **ID**  de rede: esta é a sua conta com  [!DNL Google Ad Manager]
* **ID**  do link de audiência: esta é a sua conta com  [!DNL Google Ad Manager]
* Seu tipo de conta. DFP por comprador do Google ou AdX.

## Configurar destino

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione **[!DNL Google Ad Manager]** e **[!UICONTROL Configurar]**.

![Destino do Google Ad Manager do Connect](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.

Na etapa **Setup** do fluxo de trabalho de criação de destino, preencha [!UICONTROL Basic Information] para o destino.

![Informações básicas sobre o Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: Selecione uma opção, dependendo da sua conta no Google:
   * Usar `DFP by Google` para [!DNL DoubleClick] para editores
   * Use `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL ID]** da conta: Preencha a ID da conta com  [!DNL Google]. Essa pode ser sua ID de rede ou sua ID do link de Audiência. Normalmente, essa é uma ID de oito dígitos.
* **[!UICONTROL Ação]** de marketing: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. É possível selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Ao configurar um destino [!DNL Google Ad Manager], entre em contato com seu [!DNL Google Account Manager] ou representante de Adobe para entender que tipo de conta você possui.

## Ativar segmentos para [!DNL Google Ad Manager]

Para obter instruções sobre como ativar segmentos para [!DNL Google Ad Manager], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

## Dados exportados

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Ad Manager], verifique sua conta [!DNL Google Ad Manager]. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua conta.