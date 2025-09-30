---
solution: Data Collection
audience: user
user-guide-title: Ajuda do SDK da Web da Adobe Experience Platform
breadcrumb-title: Guia do SDK da Web
user-guide-description: Interaja com os serviços da Experience Cloud por meio da Rede de borda.
feature: Web SDK
role: Developer
source-git-commit: c697d0e924545caf430382385797bde340b57d94
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 27%

---


# SDK da Web da Adobe Experience Platform {#web-sdk}

* [Visão geral do SDK Web](home.md)
* [Notas de versão](release-notes.md)
* Instalação do Web SDK {#install}
   * [Visão geral](install/overview.md)
   * [Instalar o Web SDK usando a extensão de tag](install/extension.md)
   * [Instale o Web SDK usando a biblioteca JavaScript](install/library.md)
   * [Instalar o Web SDK usando o pacote NPM](install/npm.md)
   * [Criar um build personalizado do Web SDK usando o pacote NPM](install/create-custom-build.md)
* Comandos {#commands}
   * configure {#configure}
      * [Visão geral](commands/configure/overview.md)
      * [autoCollectPropositionInteractions](commands/configure/autocollectpropositioninteractions.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [contexto](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [streamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [prehideStyle](commands/configure/prehidingstyle.md)
      * [notificações por push](commands/configure/pushnotifications.md)
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
   * [sendPushSubscription](commands/sendPushSubscription.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [Configurar substituições de sequência de dados](commands/datastream-overrides.md)
   * [Respostas de comando](commands/command-responses.md)

* Identidade {#identity}
   * [Visão geral](identity/overview.md)
   * [IDs próprias para dispositivos](identity/first-party-device-ids.md)
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
      * [Comparação da biblioteca at.js com a Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Registro do Analytics for Target (A4T) {#a4t}
         * [Visão geral](personalization/adobe-target/analytics-logging/overview.md)
         * [Registro no lado do cliente](personalization/adobe-target/analytics-logging/client-side.md)
         * [Registro do lado do servidor](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [Visão geral](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Visão geral](personalization/ajo/overview.md)
      * [Implementação de aplicativos de página única](personalization/ajo/web-spa-implementation.md)
      * [Configurar o suporte a mensagens no aplicativo da Web no Web SDK](personalization/web-in-app-messaging.md)

* Consentimento {#consent}
   * Estrutura de transparência e consentimento 2.0 do IAB {#iab-tcf}
      * [Visão geral](consent/iab-tcf/overview.md)
      * [Integrar a tags](consent/iab-tcf/with-tags.md)
      * [Integrar sem tags](consent/iab-tcf/without-tags.md)

* Casos de uso {#use-cases}
   * [Visão geral](use-cases/overview.md)
   * [Enviar dados para o Adobe Analytics usando a Web SDK](use-cases/adobe-analytics.md)
   * [Dicas do cliente do agente do usuário](use-cases/client-hints.md)
   * [Coletar dados de comércio](use-cases/collect-commerce-data.md)
   * [Configurar uma CSP](use-cases/configuring-a-csp.md)
   * [Métodos de depuração](use-cases/debugging.md)
   * [Usar várias instâncias do Web SDK](use-cases/multiple-instances.md)
   * [Configurar eventos de página superior e inferior](use-cases/top-bottom-page-events.md)
* [Monitoramento de ganchos](monitoring-hooks.md)
* [Perguntas frequentes](faq.md)
* [Recursos](resources.md)
