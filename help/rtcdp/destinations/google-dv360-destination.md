---
keywords: DoubleClick Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Destino do Google Display & Video 360
seo-title: Destino do Google Display & Video 360
description: O Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar o redirecionamento e a audiência de campanhas digitais direcionadas em fontes de inventário de Vídeo e Móvel.
seo-description: 'O Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar o redirecionamento e a audiência de campanhas digitais direcionadas em fontes de inventário de Vídeo e Móvel. '
translation-type: tm+mt
source-git-commit: c66fb4cf0a414e02ceb58becc9d9b59db3fe987b
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] Destino

## Visão geral

[!DNL Display & Video 360], anteriormente conhecida como [!DNL DoubleClick Bid Manager], é uma ferramenta usada para executar redirecionamento e campanhas digitais direcionadas para audiência em fontes de inventário de Vídeo, Vídeo e Móvel.

## Especificações de destino

Observe os seguintes detalhes específicos para [!DNL Google Display & Video 360] os destinos:

* Você pode enviar as seguintes [identidades](../../identity-service/namespaces.md) para [!DNL Google Display & Video 360] destinos: **ID de cookie do Google, IDFA, GAID, IDs do Roku, IDs da Microsoft, IDs** da Amazon Fire TV.
* Audiências ativadas são criadas de forma programática na plataforma do Google.
* A CDP em tempo real do Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de audiências no Google para validar a integração e entender o tamanho da definição de metas de audiência.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com o Google Display &amp; Video 360 e não tiver ativado a funcionalidade [de sincronização de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID no Serviço de ID de Experience Cloud no passado (com a Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente integrações do Google no Audience Manager, a ID sincroniza o transporte para o CDP em tempo real do Adobe.

### Tipo de exportação {#export-type}

**Exportação** de segmento - você está exportando todos os membros de um segmento (audiência) para o destino do Google.

## Pré-requisitos

### Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro [!DNL Google Display & Video 360] destino no Adobe Real-time CDP. Verifique se o processo de lista de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o [!DNL Google Display & Video 360] destino na CDP em tempo real do Adobe, você deve entrar em contato com o Google solicitando que o Adobe seja colocado na lista de provedores de dados permitidos e que sua conta seja adicionada à lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID** da conta: esta é uma conta Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante de Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante de Adobe para obter essa ID.
* **Seu tipo** de conta: use **[!DNL Invite advertiser]** para permitir que as audiências sejam compartilhadas somente com uma marca específica na sua conta de Vídeo e Vídeo 360 ou use **[!DNL Invite partner]** para permitir que as audiências sejam compartilhadas com todas as marcas na sua conta de Vídeo e Vídeo 360.

## Configurar destino

1. Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Google Display & Video 360]e selecione **[!UICONTROL Configurar]**.
   ![Destino do Connect Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-destination.png)

   >[!NOTE]
   >
   >Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativar]** e **[!UICONTROL Configurar]**, consulte a seção [Catálogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.

2. Na etapa **Configuração** do fluxo de trabalho de criação de destino, preencha as Informações  básicas para o destino, bem como os casos de uso de marketing que devem se aplicar a esse destino. <br>

   ![Informações básicas sobre o Google Display &amp; Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: Selecione uma opção, dependendo da sua conta no Google:
   * Use `Invite Advertiser` para permitir que as audiências sejam compartilhadas somente com uma marca específica na sua conta de Vídeo e Vídeo 360.
   * Use `Invite Partner` para permitir que as audiências sejam compartilhadas com todas as marcas em sua conta de Vídeo e Vídeo 360.
* **[!UICONTROL ID]** da conta: Preencha sua ID de conta **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** com o Google. Normalmente, essa é uma ID de seis ou sete dígitos.
* **[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados.

>[!NOTE]
>
>Ao configurar um [!DNL Google Display & Video 360] destino, entre em contato com seu representante [!DNL Google Account Manager] ou com seu representante de Adobe para entender que tipo de conta você possui.

## Ativar segmentos para [!DNL Google Display & Video 360]

Para obter instruções sobre como ativar segmentos para [!DNL Google Display & Video 360], consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).

## Dados exportados

Para verificar se os dados foram exportados com êxito para o [!DNL Google Display & Video 360] destino, verifique sua [!DNL Google Display & Video 360] conta. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua conta.