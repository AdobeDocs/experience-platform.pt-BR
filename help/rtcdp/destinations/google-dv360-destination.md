---
title: Destino do Google Display & Video 360
seo-title: Destino do Google Display & Video 360
description: O Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar o redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de inventário de Vídeo, Vídeo e Móvel.
seo-description: 'O Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar o redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de inventário de Vídeo, Vídeo e Móvel. '
translation-type: tm+mt
source-git-commit: 810028edc662a7f52484e37cf0fbdfafe5db650f

---


# Destino do Google Display &amp; Video 360

## Visão geral

O Display &amp; Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar o redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de inventário de Vídeo, Vídeo e Móvel.

## Especificações de destino

Observe os seguintes detalhes que são específicos para os destinos do Google Display &amp; Video 360:

* Você pode enviar as seguintes [identidades](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) para os destinos do Google Display &amp; Video 360: ID de cookie do **Google, IDFA, GAID, IDs do Roku, IDs da Microsoft, IDs** da Amazon Fire TV.
* Os públicos-alvo ativados são criados de forma programática na plataforma do Google.
* A CDP em tempo real da Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o tamanho da definição de metas do público-alvo.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com o Google Display &amp; Video 360 e não tiver ativado a funcionalidade [de sincronização de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID no Serviço da Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente integrações do Google no Audience Manager, a ID será sincronizada se você configurou a transferência para o Adobe Real-time CDP.

## Pré-requisitos

### Lista branca

>[!NOTE]
>
>A lista de permissões é obrigatória antes da configuração do primeiro destino do Google Display &amp; Video 360 no Adobe Real-time CDP. Verifique se o processo de listagem de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o destino do Google Display &amp; Video 360 no Adobe Real-time CDP, você deve entrar em contato com o Google solicitando que a Adobe seja incluída na lista de permissões como um provedor de dados e que sua conta seja incluída na lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID** da conta: esta é a ID da conta da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **Seu tipo** de conta: use **[!DNL Invite advertiser]** para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica na sua conta de Vídeo e Vídeo 360 ou use **[!DNL Invite partner]** para permitir que os públicos-alvo sejam compartilhados com todas as marcas na sua conta de Vídeo e Vídeo 360.

## Criar destino

1. Em **[!UICONTROL Connections > Destinations]**, selecione Google Display &amp; Video 360 e selecione **[!UICONTROL Create destination]**.
   ![Destino do Connect Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. No assistente Criar destino, preencha as Informações básicas para o destino.
   ![Informações básicas sobre o Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **Nome**: Preencha o nome preferencial para este destino.
* **Descrição**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **Tipo** de conta: Selecione uma opção, dependendo da sua conta no Google:
   * Use `Invite Advertiser` para permitir que os públicos-alvo sejam compartilhados somente para uma marca específica na sua conta de Vídeo e Vídeo 360.
   * Use `Invite Partner` para permitir que os públicos-alvo sejam compartilhados com todas as marcas em sua conta de Vídeo e Vídeo 360.
* **ID** da conta: Preencha sua ID de conta **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** com o Google. Normalmente, essa é uma ID de seis ou sete dígitos.

>[!NOTE]
>
>Ao configurar um destino do Google Display &amp; Video 360, entre em contato com seu gerente de conta do Google ou representante da Adobe para entender que tipo de conta você possui.

## Ativar segmentos para o Google Display &amp; Video 360

Para obter instruções sobre como ativar segmentos no Google Display &amp; Video 360, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).