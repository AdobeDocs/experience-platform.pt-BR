---
title: Visão geral do IAB Transparency & Consent Framework 2.0
seo-title: Suporte às preferências de consentimento do Adobe Experience Platform Web SDK do Interative Advertising Bureau Transparency & Consent Framework 2.0
description: Saiba como suportar as preferências de consentimento do IAB TCF 2.0 com o SDK da Web do Experience Platform
seo-description: Saiba como suportar as preferências de consentimento do IAB TCF 2.0 com o SDK da Web do Experience Platform
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: b82ee2508558f76e3ad56cbb8405abe9bfb235f6
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---


# Visão geral do IAB Transparency &amp; Consent Framework 2.0

O Adobe Experience Platform Web SDK (AEP Web SDK) tem suporte para o Interative Advertising Bureau Transparency &amp; Consent Framework, versão 2.0 (IAB TCF 2.0). Este guia mostra os requisitos para suportar o IAB TCF 2.0 por meio do AEP Web SDK integrando-se à Plataforma de dados do cliente em tempo real, Audience Manager, Eventos da experiência, Adobe Analytics e Experience Edge.

Além disso, os seguintes guias estão disponíveis para ajudar a aprender como integrar o IAB TCF 2.0 com e sem a Adobe Experience Platform Launch.

- [Com Adobe Experience Platform Launch](./with-launch.md)
- [Sem Adobe Experience Platform Launch](./without-launch.md)

## Introdução

Para implementar o AEP Web SDK com IAB TCF 2.0, é necessário que você tenha uma compreensão funcional do Modelo de Dados de Experiência (XDM) e dos Eventos de Experiência. Antes do start, reveja o seguinte documento:

- [Visão geral](../../../xdm/home.md)do sistema do Experience Data Model (XDM): A normalização e a interoperabilidade são conceitos-chave por trás da Adobe Experience Platform. [!DNL Experience Data Model] (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

## Integração da plataforma de dados do cliente em tempo real

Construída no Adobe Experience Platform, a Adobe Real-time Customer Data Platform (CDP em tempo real) ajuda a reunir dados conhecidos e anônimos de várias fontes corporativas. Isso permite criar perfis de clientes que podem ser usados para fornecer experiências personalizadas de clientes em todos os canais e dispositivos em tempo real. Para enviar dados de consentimento para a CDP em tempo real por meio do SDK da Web AEP, é necessário o seguinte:

- Um conjunto de dados baseado na [!DNL XDM Individual Profile] classe, habilitado para uso em, com a combinação de privacidade do Perfil [!DNL Real-time Customer Profile].
- Uma configuração de borda configurada com CDP em tempo real e o conjunto de dados do perfil mencionado acima.

Consulte o tutorial sobre como [criar conjuntos de dados para capturar o consentimento](../../../rtcdp/privacy/iab/dataset-preparation.md) do TCF 2.0 para saber como criar o conjunto de dados necessário.

Consulte a visão geral [de conformidade do](../../../rtcdp/privacy/privacy-overview.md) IAB TCF 2.0 para obter instruções sobre como criar a configuração de borda.

## integração Audience Manager

A Adobe Audience Manager (AAM) inclui suporte para o IAB TCF 2.0, que permite avaliar, honrar e encaminhar as opções de privacidade do cliente para parceiros downstream. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrar com o Audience Manager por meio do SDK da Web AEP, verifique se você tem uma configuração de borda configurada para encaminhar para a Adobe Audience Manager.

## Eventos de experiência e integração com Adobe Analytics

Enquanto a CDP em tempo real e as audiências de experiência acompanham as preferências de consentimento atuais de um cliente, os Eventos podem reter as preferências de consentimento do cliente que estavam ativas quando o evento foi coletado.

Para coletar informações de consentimento sobre eventos, é necessário o seguinte:

- Um conjunto de dados baseado na [!DNL XDM Experience Event] classe, com a combinação de [!DNL Experience Event] privacidade.
- Uma configuração de borda configurada com o [!DNL XDM Experience Event] conjunto de dados acima.

Para obter mais informações sobre como converter um Evento de experiência XDM em uma ocorrência do Analytics, consulte a documentação de visão geral [do](../../data-collection/adobe-analytics/analytics-overview.md) Analytics.

## Integração do SDK da Web AEP

As seções abaixo descrevem os principais pontos de integração entre o IAB TCF 2.0 e o AEP Web SDK.

>[!NOTE]
>
>Mesmo sem a CDP ou Audience Manager em tempo real configurada, você ainda pode integrar o IAB TCF 2.0 ao SDK da Web. As preferências de consentimento podem ser usadas para controlar a coleção de Eventos de experiência e configurar um cookie de identidade.

### Consentimento padrão

O consentimento padrão é usado quando não há preferência de consentimento já salva para um cliente. Isso significa que as opções de consentimento padrão podem controlar o comportamento do AEP Web SDK e alterar com base na região do cliente.

Por exemplo, se você tiver um cliente que não esteja na jurisdição do Regulamento Geral de Proteção de Dados (RGPD), o consentimento padrão poderá ser definido como `in`, mas dentro da jurisdição do RGPD, o consentimento padrão poderá ser definido como `pending`. Sua plataforma de gerenciamento de nuvem (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para o IAB TCF 2.0. Esse sinalizador pode ser usado para definir o consentimento padrão.

Para obter mais informações sobre o consentimento padrão, consulte a seção [consentimento](../../fundamentals/configuring-the-sdk.md#default-consent) padrão na documentação de configuração do SDK.

### Definir consentimento quando ele for alterado

O AEP Web SDK tem um `setConsent` comando, que comunica as preferências de consentimento do cliente a todos os serviços de Adobe usando o IAB TCF 2.0. Se você estiver integrando a CDP em tempo real, isso atualizará o perfil do cliente. Se você estiver integrando o Audience Manager, isso atualizará as informações do cliente. Chamar isso também define um cookie com uma preferência de consentimento completo ou nulo que controla se os futuros Eventos de experiência podem ser enviados. Pretende-se que esta ação seja chamada sempre que o consentimento muda. Em cargas futuras de página, o cookie de consentimento da Experience Edge será lido para determinar se os Eventos da experiência podem ser enviados e se um cookie de identidade pode ser definido.

Semelhante à integração com a IAB TCF 2.0, a Experience Edge dá o consentimento de um cliente ter fornecido seu consentimento explícito para os seguintes fins:

- **Finalidade 1:** Armazenar e/ou acessar informações em um dispositivo
- **Finalidade 10:** Desenvolver e melhorar produtos
- **Finalidade especial 1:** Garanta a segurança, evite fraudes e depure. (De acordo com os regulamentos do TCF da IAB, isso é sempre aceito)
- **Permissão do fornecedor do Adobe:** Consentimento para Adobe (Fornecedor 565)

Para obter mais informações sobre o `setConsent` comando, leia a documentação sobre [Suporte ao Consentimento](../../consent/supporting-consent.md).

### Adicionando consentimento aos Eventos de experiência

O AEP Web SDK tem um `sendEvent` comando que coleta um Evento de experiência. Se você estiver integrando Eventos de experiência ou Adobe Analytics e quiser as preferências de consentimento em cada Evento de experiência, adicione as informações de consentimento a cada `sendEvent` comando.

Para obter mais informações sobre o `sendEvent` comando, leia a documentação sobre o [rastreamento de eventos](../../fundamentals/tracking-events.md).

## Próximas etapas

Agora que você tem uma compreensão básica do IAB Transparency &amp; Consent Framework 2.0, consulte qualquer um dos guias sobre como usar o IAB TCF 2.0 [com o Adobe Experience Platform Launch](./with-launch.md) ou [sem o Adobe Experience Platform Launch](./without-launch.md).
