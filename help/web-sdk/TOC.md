---
solution: Data Collection
audience: user
user-guide-title: Ajuda do SDK da Web da Adobe Experience Platform
breadcrumb-title: Guia do SDK da Web
user-guide-description: Interaja com os serviços da Experience Cloud por meio da Rede de borda.
feature: Web SDK
role: Developer
source-git-commit: bb2c0b5483bf0b50e98e21bef23d1667660d1981
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 23%

---


# SDK da Web da Adobe Experience Platform {#web-sdk}

* [Visão geral do SDK Web](home.md)
* [Notas de versão](release-notes.md)
* Instalação do SDK da Web {#install}
   * [Visão geral](install/overview.md)
   * [Instale o SDK da Web usando a extensão de tag](install/extension.md)
   * [Instale o SDK da Web usando a biblioteca do JavaScript](install/library.md)
   * [Instalar o SDK da Web usando o pacote NPM](install/npm.md)
* Comandos {#commands}
   * configurar {#configure}
      * [Visão geral](commands/configure/overview.md)
      * [autoTrackPropositionInteractionsEnabled](commands/configure/autotrackpropositioninteractionsenabled.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [contexto](commands/configure/context.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeConfigId](commands/configure/edgeconfigid.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [streamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [prehideStyle](commands/configure/prehidingstyle.md)
      * [targetMigrationEnabled](commands/configure/targetmigrationenabled.md)
      * [thirdPartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [Visão geral](commands/sendevent/overview.md)
      * [dados](commands/sendevent/data.md)
      * [documentUnloading](commands/sendevent/documentunloading.md)
      * [personalização](commands/sendevent/personalization.md)
      * [renderDecision](commands/sendevent/renderdecisions.md)
      * [tipo](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyPropositions](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [Configurar substituições da sequência de dados](commands/datastream-overrides.md)
   * [Respostas de comando](commands/command-responses.md)

* Identidade {#identity}
   * [Visão geral](identity/overview.md)
   * [IDs de dispositivo próprio](identity/first-party-device-ids.md)
   * [Compartilhamento de ID de dispositivo móvel para Web e entre domínios](identity/id-sharing.md)

* Personalização {#personalization}
   * [Gerenciar eventos de exibição](personalization/display-events.md)
   * [Renderizar conteúdo personalizado](personalization/rendering-personalization-content.md)
   * [Personalization por meio de implementação híbrida](personalization/hybrid-personalization.md)
   * [Gerenciar cintilação](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Visão geral](personalization/adobe-target/target-overview.md)
      * [Implementação de aplicativos de página única](personalization/adobe-target/spa-implementation.md)
      * [Acesso aos tokens de resposta](personalization/adobe-target/accessing-response-tokens.md)
      * [Uso da ID de terceiros da mbox](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Comparação da biblioteca at.js com o SDK da Web](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Log do Analytics for Target (A4T) {#a4t}
         * [Visão geral](personalization/adobe-target/analytics-logging/overview.md)
         * [Registro no lado do cliente](personalization/adobe-target/analytics-logging/client-side.md)
         * [Registro do lado do servidor](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer decisioning {#offer-decisioning}
      * [Visão geral](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Visão geral](personalization/ajo/overview.md)
      * [Implementação de aplicativos de página única](personalization/ajo/web-spa-implementation.md)
      * [Configurar o suporte a mensagens no aplicativo da Web no SDK da Web](personalization/web-in-app-messaging.md)

* Consentimento {#consent}
   * Estrutura de transparência e consentimento 2.0 do IAB {#iab-tcf}
      * [Visão geral](consent/iab-tcf/overview.md)
      * [Integrar a tags](consent/iab-tcf/with-tags.md)
      * [Integrar sem tags](consent/iab-tcf/without-tags.md)

* Casos de uso {#use-cases}
   * [Visão geral](use-cases/overview.md)
   * [Enviar dados para a Adobe Analytics usando o SDK da Web](use-cases/adobe-analytics.md)
   * [Dicas do cliente do agente do usuário](use-cases/client-hints.md)
   * [Coletar dados de comércio](use-cases/collect-commerce-data.md)
   * [Configurar uma CSP](use-cases/configuring-a-csp.md)
   * [Métodos de depuração](use-cases/debugging.md)
   * [Usar várias instâncias do SDK da Web](use-cases/multiple-instances.md)
   * [Configurar eventos de página superior e inferior](use-cases/top-bottom-page-events.md)

* [Perguntas frequentes](faq.md)
* [Recursos](resources.md)
