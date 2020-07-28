---
title: Destino do Google Ad Manager
seo-title: Destino do Google Ad Manager
description: 'O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de serviço de anúncios do Google que oferece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e em aplicativos móveis. '
seo-description: 'O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de serviço de anúncios do Google que oferece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e em aplicativos móveis. '
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Visão geral

[!DNL Google Ad Manager], anteriormente conhecida como [!DNL DoubleClick] para editores ou [!DNL DoubleClick AdX], é uma plataforma de veiculação de anúncios [!DNL Google] que oferece aos editores os meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e em aplicativos móveis.

## Especificações de destino

Observe os seguintes detalhes específicos para [!DNL Google Ad Manager] os destinos:

* Você pode enviar as seguintes [identidades](../../identity-service/namespaces.md) para [!DNL Google Ad Manager] destinos: **ID de cookie do Google, IDFA, GAID, IDs do Roku, IDs da Microsoft, IDs** da Amazon Fire TV.
* audiências ativadas são criadas de forma programática na [!DNL Google] plataforma.
* A CDP em tempo real da Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de audiências no Google para validar a integração e entender o tamanho da definição de metas de audiência.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com [!DNL Google Ad Manager] e não tiver ativado a funcionalidade [de sincronização de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID no Serviço de ID de Experience Cloud no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente [!DNL Google] integrações no Audience Manager, a ID sincronizará a transferência para o Adobe Real-time CDP.

## Pré-requisitos

### Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro [!DNL Google Ad Manager] destino no Adobe Real-time CDP. Verifique se o processo de lista de permissões descrito abaixo foi concluído [!DNL Google] antes de criar um destino.

Antes de criar o [!DNL Google Ad Manager] destino no Adobe Real-time CDP, você deve entrar em contato [!DNL Google] para que a Adobe seja colocada na lista de provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Entre em contato [!DNL Google] e forneça as seguintes informações:

* **ID** da conta: esta é a ID da conta da Adobe com [!DNL Google]. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente da Adobe com [!DNL Google]. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **ID** de rede: esta é a sua conta com [!DNL Google Ad Manager]
* **ID** do link de Audiência: esta é a sua conta com [!DNL Google Ad Manager]
* Seu tipo de conta. **DFP pelo Google** ou comprador **do** AdX.

## Criar destino

1. Em **[!UICONTROL Conexões > Destinos]**, selecione [!DNL Google Ad Manager]e selecione **[!UICONTROL Criar destino]**.
   ![Destino do Google Ad Manager do Connect](/help/rtcdp/destinations/assets/google-1-destination.png)

2. Na etapa **Configuração** do fluxo de trabalho de criação de destino, preencha as Informações  básicas para o destino. <br>

   ![Informações básicas sobre o Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: Selecione uma opção, dependendo da sua conta no Google:
   * Usar `DFP by Google` para [!DNL DoubleClick] editores
   * Usar `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL ID]** da conta: Preencha a ID da conta com [!DNL Google]. Essa pode ser sua ID de rede ou sua ID do link de Audiência. Normalmente, essa é uma ID de oito dígitos.
* **[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar entre casos de uso de marketing definidos pela Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pela Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados.

>[!NOTE]
>
> Ao configurar um [!DNL Google Ad Manager] destino, entre em contato com seu representante da Adobe [!DNL Google Account Manager] ou Adobe para saber que tipo de conta você possui.

## Ativar segmentos para [!DNL Google Ad Manager]

Para obter instruções sobre como ativar segmentos para [!DNL Google Ad Manager], consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).