---
title: Destino do Google Ad Manager
seo-title: Destino do Google Ad Manager
description: 'O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de serviço de anúncios do Google que oferece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e em aplicativos móveis. '
seo-description: 'O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de serviço de anúncios do Google que oferece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e em aplicativos móveis. '
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Destino do Google Ad Manager

## Visão geral

O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de serviço de anúncios do Google que oferece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e em aplicativos móveis.

## Especificações de destino

Observe os seguintes detalhes específicos para os destinos do Google Ad Manager:

* Você pode enviar as seguintes [identidades](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) para os destinos do Google Ad Manager: ID de cookie do **Google, IDFA, GAID, IDs do Roku, IDs da Microsoft, IDs** da Amazon Fire TV.
* Os públicos-alvo ativados são criados de forma programática na plataforma do Google.
* A CDP em tempo real da Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o tamanho da definição de metas do público-alvo.

>[!IMPORTANT]
>
>Se você estiver procurando criar seu primeiro destino com o Google Ad Manager e não tiver ativado a funcionalidade [de sincronização de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID no Serviço da Experience Cloud ID no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar sincronizações de ID. Se você tiver configurado anteriormente integrações do Google no Audience Manager, a ID será sincronizada se você configurou a transferência para o Adobe Real-time CDP.

## Pré-requisitos

### Lista branca

>[!NOTE]
>
>A lista de permissões é obrigatória antes da configuração do primeiro destino do Google Ad Manager na CDP em tempo real da Adobe. Verifique se o processo de listagem de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o destino do Google Ad Manager na Adobe Real-time CDP, você deve entrar em contato com o Google solicitando que a Adobe seja incluída na lista de permissões como um provedor de dados e que sua conta seja incluída na lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID** da conta: esta é a ID da conta da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente da Adobe com o Google. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para obter essa ID.
* **ID** de rede: esta é sua conta no Google Ad Manager
* **ID** do link de público-alvo: esta é sua conta no Google Ad Manager
* Seu tipo de conta. **DFP pelo Google** ou comprador **do** AdX.

## Criar destino

1. Em **[!UICONTROL Connections > Destinations]**, selecione Google Ad Manager e selecione **[!UICONTROL Create destination]**.
   ![Destino do Google Ad Manager do Connect](/help/rtcdp/destinations/assets/google-1-destination.png)

2. No assistente Criar destino, preencha as Informações básicas para o destino.
   ![Informações básicas sobre o Google Ad Manager](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **Nome**: Preencha o nome preferencial para este destino.
* **Descrição**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **Tipo** de conta: Selecione uma opção, dependendo da sua conta no Google:
   * Usar `DFP by Google` para DoubleClick for Publishers
   * Usar `AdX buyer` para Google AdX
* **ID** da conta: Preencha a ID da sua conta com o Google. Essa pode ser sua ID de rede ou sua ID do link de público-alvo. Normalmente, essa é uma ID de oito dígitos.

>[!NOTE]
>
>Ao configurar um destino do Google Ad Manager, entre em contato com seu gerente de contas do Google ou representante da Adobe para entender que tipo de conta você possui.

## Ativar segmentos no Google Ad Manager

Para obter instruções sobre como ativar segmentos no Google Ad Manager, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).