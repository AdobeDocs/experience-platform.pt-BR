---
title: Destino do Google
seo-title: Destino do Google
description: O Adobe Real-time CDP integra-se ao Google para permitir que você execute e ative seus dados no DV360, Google Ad Manager, Google AdWords e Google AdX.
seo-description: O Adobe Real-time CDP integra-se ao Google para permitir que você execute e ative seus dados no DV360, Google Ad Manager, Google AdWords e Google AdX.
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Destino do Google

## Visão geral

O Adobe Real-time CDP é integrado ao Google para permitir que você execute e ative seus dados no DV360, no Google Ad Manager, no Google AdWords Display e no Google AdX.

## Especificações de destino

Observe os seguintes detalhes que são específicos para os destinos do Google:

* Você pode enviar as seguintes [identidades](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) para destinos do Google: ID de cookie **do Google, IDFA, GAID**.
* Os públicos-alvo ativados são criados de forma programática na plataforma do Google.
* A CDP em tempo real da Adobe não inclui atualmente uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o cancelamento de dados.

## Pré-requisitos

### Lista branca

Antes de conectar o destino do Google no Adobe Real-time CDP, você deve entrar em contato com o Google solicitando que sua conta seja incluída na lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID** da conta: esta é a ID da conta da Adobe com o Google. Entre em contato com o suporte da Adobe para obter essa ID.
* **ID** do cliente: esta é a ID da conta do cliente da Adobe com o Google. Entre em contato com o suporte da Adobe para obter essa ID.
* **ID** do parceiro: Esta é sua ID de parceiro de três dígitos com o Google;
* **ID** de rede: esta é a sua conta no Google;
* **ID** do link de público-alvo: esta é a sua conta no Google;
* Seu tipo de conta. Isso pode ser **Convidar anunciante**, **Convidar parceiro**, **DFP**, **AdWords**, **AdX**.


## Destino do Connect

1. Em **[!UICONTROL Conexões > Destinos]**, selecione Google e selecione **[!UICONTROL Criar destino]**.
   ![Conectar destino do Google](/help/rtcdp/destinations/assets/google-destination.png)

2. No assistente de destino do Connect, preencha as Informações básicas para o destino.
   ![Informações básicas no Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Nome**: Preencha o nome preferencial para este destino.
* **Descrição**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **Tipo** de conta: Selecione uma opção, dependendo da sua conta no Google:
   * Usar `Invite advertiser` para o Google DV360
   * Usar `Invite partner` para o Google DV360
   * Usar `DFP by Google` o Google Ad Manager
   * Usar `AdWords` para exibição do Google AdWords
   * Usar `AdX buyer` para Google AdX
* **ID** da conta: Preencha a ID da sua conta com o Google.

>[!NOTE]
>
>Ao configurar um destino do Google, entre em contato com seu gerente de conta do Google ou representante da Adobe para entender em qual tipo de produto sua conta pertence. Para o Google DV360, pergunte a seu gerente de conta do Google em que tipo de produto sua conta pertence. 

## Ativar segmentos no Google

Para obter instruções sobre como ativar segmentos no Google, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).