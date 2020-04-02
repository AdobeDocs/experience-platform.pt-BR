---
title: Google AdsDestination
seo-title: Destino de anúncios do Google
description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem propaganda por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
seo-description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem propaganda por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Destino de anúncios do Google

## Visão geral

O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem propaganda por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.

## Especificações de destino

Observe os seguintes detalhes que são específicos para os destinos do Google Ads:

* Você pode enviar as seguintes [identidades](../../identity-service/namespaces.md) para os destinos do Google Ads: ID de cookie do **Google, IDFA, GAID, IDs do Roku, IDs da Microsoft, IDs** da Amazon Fire TV.
* audiências ativadas são criadas de forma programática na plataforma do Google.
* A CDP em tempo real da Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de audiências no Google para validar a integração e entender o tamanho da definição de metas de audiência.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com o Google Ads e não tiver ativado a funcionalidade [de sincronização de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID no Serviço da Experience Cloud ID no passado (com o Audiência Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente integrações do Google no Audiência Manager, a ID sincronizará a transferência para o Adobe Real-time CDP.

## Pré-requisitos

### Conta existente do Google Ads

O Google pausou quaisquer integrações novas do Google Ads com fornecedores de terceiros. Você deve ter uma integração existente com o Google Ads para poder executar as etapas da lista de permissões na próxima seção e criar um destino do Google Ads na Adobe Real-time CDP.

### Lista branca

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro destino de Anúncios do Google no CDP em tempo real da Adobe. Verifique se o processo de listagem de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o destino do Google Ads na Adobe Real-time CDP, você deve entrar em contato com o Google solicitando que a Adobe seja incluída na lista de permissões como um provedor de dados e que sua conta seja incluída na lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID** da conta: esta é a ID da conta da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* Seu tipo de conta: **AdWords**
* **ID** do Google AdWords: Esta é a sua ID com o Google. Normalmente, o formato da ID é 123-456-7890.

## Criar destino

1. Em **[!UICONTROL Connections > Destinations]**, selecione Google Ads e selecione **[!UICONTROL Create destination]**.
   ![Destino do Connect Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

2. No fluxo de trabalho Criar destino, preencha o campo [!UICONTROL Basic Information] para o destino.
   ![Informações básicas sobre o Google Ads](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Description]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Account Type]**: AdWords é a única opção disponível.
* **[!UICONTROL Account ID]**: Preencha a ID da sua conta com o Google Ads. Normalmente, o formato da ID é 123-456-7890.

## Ativar segmentos para Google Ads

Para obter instruções sobre como ativar segmentos no Google Ads, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).

