---
title: Suporte a IAB TCF 2.0 no SDK da Web da Adobe Experience Platform
description: Saiba como suportar as preferências de consentimento do IAB TCF 2.0 usando o Adobe Experience Platform Web SDK
keywords: consentimento;setConsent;Mixin de privacidade do Perfil;Mixin de privacidade do Evento de experiência;Mixin de privacidade;IAB TCF 2.0;CDP em tempo real;Perfil de dados do cliente em tempo real
translation-type: tm+mt
source-git-commit: 1c6238a0cf72230e019fd10d9a72f30444bd9fb9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---


# Suporte a IAB TCF 2.0 no Adobe Experience Platform Web SDK

O SDK da Web da Adobe Experience Platform tem suporte para o Interative Advertising Bureau Transparency &amp; Consent Framework, versão 2.0 (IAB TCF 2.0). Este guia mostra os requisitos para suportar o IAB TCF 2.0 por meio do Adobe Experience Platform Web SDK, integrando-se à Plataforma de dados do cliente em tempo real, Audience Manager, Eventos da experiência, Adobe Analytics e Experience Edge.

Além disso, os seguintes guias estão disponíveis para ajudar a aprender como integrar o IAB TCF 2.0 com e sem a Adobe Experience Platform Launch.

- [Com Adobe Experience Platform Launch](./with-launch.md)
- [Sem Adobe Experience Platform Launch](./without-launch.md)

## Introdução

Para implementar o SDK da Web com o IAB TCF 2.0, é necessário conhecer os Eventos do Experience Data Model (XDM) e da Experience. Antes do start, reveja o seguinte documento:

- [Visão geral](../../../xdm/home.md) do sistema do Experience Data Model (XDM): A normalização e a interoperabilidade são conceitos-chave por trás da Adobe Experience Platform. [!DNL Experience Data Model (XDM)], impulsionada pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

## integração Experience Platform

Para enviar dados de consentimento à Adobe Experience Platform usando o SDK, é necessário o seguinte:

- Um conjunto de dados cujo schema é baseado na classe [!DNL XDM Individual Profile] e contém campos de consentimento TCF 2.0, habilitados para uso em [!DNL Real-time Customer Profile].
- Uma configuração de borda configurada com Plataforma e o conjunto de dados habilitado para Perfis mencionado acima.

Consulte o guia em [Conformidade com TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter instruções sobre como criar os conjuntos de dados e a configuração de borda necessários.

## integração Audience Manager

A Adobe Audience Manager (AAM) inclui suporte para o IAB TCF 2.0, que permite avaliar, honrar e encaminhar as opções de privacidade do cliente para parceiros downstream. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para fazer a integração com o Audience Manager pelo Adobe Experience Platform Web SDK, verifique se você tem uma configuração de borda configurada para encaminhar para a Adobe Audience Manager.

## Eventos de experiência e integração com Adobe Analytics

Enquanto a CDP em tempo real e as audiências de experiência acompanham as preferências de consentimento atuais de um cliente, os Eventos podem reter as preferências de consentimento do cliente que estavam ativas quando o evento foi coletado.

Para coletar informações de consentimento sobre eventos, é necessário o seguinte:

- Um conjunto de dados baseado na classe [!DNL XDM Experience Event], com a combinação de privacidade [!DNL Experience Event].
- Uma configuração de borda configurada com o conjunto de dados [!DNL XDM Experience Event] acima.

Para obter mais informações sobre como converter um Evento de experiência XDM em uma ocorrência do Analytics, consulte a documentação [Visão geral do Analytics](../../data-collection/adobe-analytics/analytics-overview.md).

## Integração do Adobe Experience Platform Web SDK

As seções abaixo descrevem os principais pontos de integração entre o IAB TCF 2.0 e o Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Mesmo sem a CDP ou Audience Manager em tempo real configurada, você ainda pode integrar o IAB TCF 2.0 ao SDK da Web. As preferências de consentimento podem ser usadas para controlar a coleção de Eventos de experiência e configurar um cookie de identidade.

### Consentimento padrão

O consentimento padrão é usado quando não há preferência de consentimento já salva para um cliente. Isso significa que as opções de consentimento padrão podem controlar o comportamento do Adobe Experience Platform Web SDK e alterar com base na região do cliente.

Por exemplo, se você tiver um cliente que não esteja na jurisdição do Regulamento Geral de Proteção de Dados (RGPD), o consentimento padrão poderá ser definido como `in`, mas dentro da jurisdição do RGPD, o consentimento padrão poderá ser definido como `pending`. Sua Plataforma de gerenciamento de consentimento (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para o IAB TCF 2.0. Esse sinalizador pode ser usado para definir o consentimento padrão.

Para obter mais informações sobre o consentimento padrão, consulte a [seção de consentimento padrão](../../fundamentals/configuring-the-sdk.md#default-consent) na documentação de configuração do SDK.

### Definir consentimento quando ele for alterado

O Adobe Experience Platform Web SDK tem um comando `setConsent`, que comunica as preferências de consentimento do cliente a todos os serviços do Adobe usando o IAB TCF 2.0. Se você estiver integrando a CDP em tempo real, isso atualizará o perfil do cliente. Se você estiver integrando o Audience Manager, isso atualizará as informações do cliente. Chamar isso também define um cookie com uma preferência de consentimento completo ou nulo que controla se os futuros Eventos de experiência podem ser enviados. Pretende-se que esta ação seja chamada sempre que o consentimento muda. Em cargas futuras de página, o cookie de consentimento da Experience Edge será lido para determinar se os Eventos da experiência podem ser enviados e se um cookie de identidade pode ser definido.

Semelhante à integração com a IAB TCF 2.0, a Experience Edge dá o consentimento de um cliente ter fornecido seu consentimento explícito para os seguintes fins:

- **Finalidade 1:** Armazenar e/ou acessar informações em um dispositivo
- **Finalidade 10:** Desenvolver e melhorar produtos
- **Finalidade especial 1:** Garanta a segurança, evite fraudes e depure. (De acordo com os regulamentos do TCF da IAB, isso é sempre aceito)
- **Permissão de fornecedor de Adobe:** Consentimento para Adobe (Fornecedor 565)

Para obter mais informações sobre o comando `setConsent`, leia a documentação em [Consentimento de suporte](../../consent/supporting-consent.md).

### Adicionando consentimento aos Eventos de experiência

O Adobe Experience Platform Web SDK tem um comando `sendEvent` que coleta um Evento da experiência. Se você estiver integrando Eventos de experiência ou Adobe Analytics e quiser as preferências de consentimento em cada Evento de experiência, adicione as informações de consentimento a cada comando `sendEvent`.

Para obter mais informações sobre o comando `sendEvent`, leia a documentação em [eventos de rastreamento](../../fundamentals/tracking-events.md).

## Próximas etapas

Agora que você tem uma compreensão básica do IAB Transparency &amp; Consent Framework 2.0, consulte qualquer um dos guias sobre como usar o IAB TCF 2.0 [com Adobe Experience Platform Launch](./with-launch.md) ou [sem o Adobe Experience Platform Launch](./without-launch.md).
