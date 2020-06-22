---
title: Google AdsDestination
seo-title: Destino de anúncios do Google
description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem propaganda por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
seo-description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem propaganda por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---


# Destino de anúncios do Google

## Visão geral

O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem propaganda por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.

## Especificações de destino

Observe os seguintes detalhes que são específicos para os destinos do Google Ads:

* Você pode enviar as seguintes [identidades](../../identity-service/namespaces.md) para os destinos do Google Ads: **ID de cookie do Google, IDFA, GAID, IDs do Roku, IDs da Microsoft, IDs** da Amazon Fire TV.
* audiências ativadas são criadas de forma programática na plataforma do Google.
* A CDP em tempo real da Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de audiências no Google para validar a integração e entender o tamanho da definição de metas de audiência.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com o Google Ads e não tiver ativado a funcionalidade [de sincronização de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID no Serviço de ID de Experience Cloud no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente as integrações do Google no Audience Manager, a ID sincroniza o transporte para o Adobe Real-time CDP.

## Pré-requisitos

### Conta existente do Google Ads

O Google pausou quaisquer integrações novas do Google Ads com fornecedores de terceiros. Você deve ter uma integração existente com o Google Ads para poder executar as etapas da lista de permissão na próxima seção e criar um destino do Google Ads na Adobe Real-time CDP.

### Permitir lista

>[!NOTE]
>
>A lista de permissão é obrigatória antes de configurar seu primeiro destino de Anúncios do Google no Adobe Real-time CDP. Verifique se o processo de lista de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o destino do Google Ads no Adobe Real-time CDP, você deve entrar em contato com o Google para a Adobe para que ele seja colocado na lista de provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID** da conta: esta é a ID da conta da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* Seu tipo de conta: **AdWords**
* **ID** do Google AdWords: Esta é a sua ID com o Google. Normalmente, o formato da ID é 123-456-7890.

## Criar destino

1. Em **[!UICONTROL Conexões > Destinos]**, selecione Google Ads e selecione **[!UICONTROL Criar destino]**.
   ![Destino do Connect Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

2. Na etapa **Configuração** do fluxo de trabalho de criação de destino, preencha as Informações  básicas para o destino. <br>

   ![Informações básicas sobre o Google Ads](/help/rtcdp/destinations/assets/google-ads-setup-step.png)
* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: AdWords é a única opção disponível.
* **[!UICONTROL ID]** da conta: Preencha a ID da sua conta com o Google Ads. Normalmente, o formato da ID é 123-456-7890.
* **[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar entre casos de uso de marketing definidos pela Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pela Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados.

## Ativar segmentos para Google Ads

Para obter instruções sobre como ativar segmentos no Google Ads, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).

