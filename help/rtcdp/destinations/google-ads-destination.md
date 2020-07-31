---
title: Google AdsDestination
seo-title: Destino de anúncios do Google
description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem propaganda por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
seo-description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem propaganda por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
translation-type: tm+mt
source-git-commit: 7f3df12da5e93c3d0cc53eed1aa603ddbafdb0b2
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# [!DNL Google Ads] Destino

## Visão geral

[!DNL Google Ads], anteriormente conhecido como [!DNL Google AdWords][!DNL YouTube] , é um serviço de publicidade online que permite que as empresas paguem anúncios por clique em pesquisas baseadas em texto, exibições gráficas, vídeos e exibições móveis no aplicativo.

## Especificações de destino

Observe os seguintes detalhes específicos para [!DNL Google Ads] os destinos:

* Você pode enviar as seguintes [identidades](../../identity-service/namespaces.md) para [!DNL Google Ads] destinos: **ID de cookie do Google, IDFA, GAID, IDs do Roku, IDs da Microsoft, IDs** da Amazon Fire TV.
* audiências ativadas são criadas de forma programática na [!DNL Google] plataforma.
* A CDP em tempo real do Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de audiências no Google para validar a integração e entender o tamanho da definição de metas de audiência.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com [!DNL Google Ads] e não tiver ativado a funcionalidade [de sincronização de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID no Serviço de ID da Experience Cloud no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Consultoria da Adobe ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente integrações do Google no Audience Manager, a ID sincroniza o transporte para o CDP em tempo real do Adobe.

## Pré-requisitos

### Conta [!DNL Google Ads] existente

[!DNL Google] pausou novas integrações [!DNL Google Ads] com fornecedores terceirizados. É necessário ter uma integração existente com [!DNL Google Ads] o para poder executar as etapas de lista de permissões na próxima seção e criar um [!DNL Google Ads] destino no CDP em tempo real do Adobe.

### Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro [!DNL Google Ads] destino no Adobe Real-time CDP. Verifique se o processo de lista de permissões descrito abaixo foi concluído [!DNL Google] antes de criar um destino.

Antes de criar o [!DNL Google Ads] destino na CDP em tempo real do Adobe, você deve entrar em contato [!DNL Google] para que o Adobe seja colocado na lista dos provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Entre em contato [!DNL Google] e forneça as seguintes informações:

* **ID** da conta: esta é a ID da conta Adobe com [!DNL Google]. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante de Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente com [!DNL Google]. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante de Adobe para obter essa ID.
* Seu tipo de conta: **AdWords**
* **ID** do Google AdWords: Esta é a sua ID com [!DNL Google]. Normalmente, o formato da ID é 123-456-7890.

## Criar destino

1. Em **[!UICONTROL Conexões > Destinos]**, selecione [!DNL Google Ads]e selecione **[!UICONTROL Criar destino]**.
   ![Destino do Connect Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

2. Na etapa **Configuração** do fluxo de trabalho de criação de destino, preencha as Informações  básicas para o destino. <br>

   ![Informações básicas sobre o Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: AdWords é a única opção disponível.
* **[!UICONTROL ID]** da conta: Preencha a ID da conta com [!DNL Google Ads]. Normalmente, o formato da ID é 123-456-7890.
* **[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados.

## Ativar segmentos para [!DNL Google Ads]

Para obter instruções sobre como ativar segmentos para [!DNL Google Ads], consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).

## Dados exportados

Para verificar se os dados foram exportados com êxito para o [!DNL Google Ads] destino, verifique sua [!DNL Google Ads] conta. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua conta.