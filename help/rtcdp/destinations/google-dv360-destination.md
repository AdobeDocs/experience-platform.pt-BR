---
title: Destino do Google Display & Video 360
seo-title: Destino do Google Display & Video 360
description: O Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar o redirecionamento e a audiência de campanhas digitais direcionadas em fontes de inventário de Vídeo e Móvel.
seo-description: 'O Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar o redirecionamento e a audiência de campanhas digitais direcionadas em fontes de inventário de Vídeo e Móvel. '
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] Destino

## Visão geral

[!DNL Display & Video 360], anteriormente conhecida como [!DNL DoubleClick Bid Manager], é uma ferramenta usada para executar redirecionamento e campanhas digitais direcionadas para audiência em fontes de inventário de Vídeo, Vídeo e Móvel.

## Especificações de destino

Observe os seguintes detalhes específicos para [!DNL Google Display & Video 360] os destinos:

* Você pode enviar as seguintes [identidades](../../identity-service/namespaces.md) para [!DNL Google Display & Video 360] destinos: **ID de cookie do Google, IDFA, GAID, IDs do Roku, IDs da Microsoft, IDs** da Amazon Fire TV.
* audiências ativadas são criadas de forma programática na plataforma do Google.
* A CDP em tempo real da Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de audiências no Google para validar a integração e entender o tamanho da definição de metas de audiência.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com o Google Display &amp; Video 360 e não tiver ativado a funcionalidade [de sincronização de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID no Serviço de ID de Experience Cloud no passado (com Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente as integrações do Google no Audience Manager, a ID sincroniza o transporte para o Adobe Real-time CDP.

## Pré-requisitos

### Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro [!DNL Google Display & Video 360] destino no Adobe Real-time CDP. Verifique se o processo de lista de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o [!DNL Google Display & Video 360] destino no Adobe Real-time CDP, você deve entrar em contato com o Google solicitando que a Adobe seja colocada na lista de provedores de dados permitidos e que sua conta seja adicionada à lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID** da conta: esta é a ID da conta da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **Seu tipo** de conta: use **[!DNL Invite advertiser]** para permitir que as audiências sejam compartilhadas somente com uma marca específica na sua conta de Vídeo e Vídeo 360 ou use **[!DNL Invite partner]** para permitir que as audiências sejam compartilhadas com todas as marcas na sua conta de Vídeo e Vídeo 360.

## Criar destino

1. Em **[!UICONTROL Conexões > Destinos]**, selecione [!DNL Google Display & Video 360]e selecione **[!UICONTROL Criar destino]**.
   ![Destino do Connect Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. Na etapa **Configuração** do fluxo de trabalho de criação de destino, preencha as Informações  básicas para o destino, bem como os casos de uso de marketing que devem se aplicar a esse destino. <br>

   ![Informações básicas sobre o Google Display &amp; Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: Selecione uma opção, dependendo da sua conta no Google:
   * Use `Invite Advertiser` para permitir que as audiências sejam compartilhadas somente com uma marca específica na sua conta de Vídeo e Vídeo 360.
   * Use `Invite Partner` para permitir que as audiências sejam compartilhadas com todas as marcas em sua conta de Vídeo e Vídeo 360.
* **[!UICONTROL ID]** da conta: Preencha sua ID de conta **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** com o Google. Normalmente, essa é uma ID de seis ou sete dígitos.
* **[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar entre casos de uso de marketing definidos pela Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pela Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados.

>[!NOTE]
>
>Ao configurar um [!DNL Google Display & Video 360] destino, entre em contato com seu representante da Adobe [!DNL Google Account Manager] ou Adobe para saber que tipo de conta você possui.

## Ativar segmentos para [!DNL Google Display & Video 360]

Para obter instruções sobre como ativar segmentos para [!DNL Google Display & Video 360], consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).