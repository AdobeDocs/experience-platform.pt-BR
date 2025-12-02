---
audience: user
solution: Data Collection
user-guide-title: Coleção de dados
breadcrumb-title: Coleção de dados
user-guide-description: Saiba como enviar dados para o Adobe Experience Platform.
feature: Data Collection
role: Developer
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 31%

---


# Coleção de dados {#collection}

+ [Visão geral](home.md)
+ [Permissões](permissions.md)
+ BrightScript {#brightscript}
   + [Visão geral do BrightScript](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [Visão geral do JavaScript](js/js-overview.md)
   + [Notas de versão](js/release-notes.md)
   + Instalação {#install}
      + [Visão geral da instalação](js/install/overview.md)
      + [Biblioteca](js/install/library.md)
      + [NPM](js/install/npm.md)
      + [Compilação personalizada](js/install/create-custom-build.md)
   + Comandos {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyPropositions](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + configure {#configure}
         + [Visão geral](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [contexto](js/commands/configure/context.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgeBasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [prehideStyle](js/commands/configure/prehidingstyle.md)
         + [notificações por push](js/commands/configure/pushnotifications.md)
         + [streamingMedia](js/commands/configure/streamingmedia.md)
         + [targetMigrationEnabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdPartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [Visão geral](js/commands/sendevent/overview.md)
         + [dados](js/commands/sendevent/data.md)
         + [documentUnloading](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [personalização](js/commands/sendevent/personalization.md)
         + [renderDecision](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [Respostas de comando](js/commands/command-responses.md)
   + [Monitoramento de ganchos](js/monitoring-hooks.md)
   + [Perguntas frequentes](js/faq.md)
+ Tags {#tags}
   + [Visão geral](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [empresa](tags/company.md)
   + [_container](tags/container.md)
   + [cookie](tags/cookie.md)
   + [ambiente](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [logger](tags/logger.md)
   + [_monitores](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [track](tags/track.md)
+ Casos de uso {#use-cases}
   + [Visão geral](use-cases/overview.md)
   + [Client hints](use-cases/client-hints.md)
   + [Estado do cliente](use-cases/client-state.md)
   + [Coletar dados de comércio](use-cases/collect-commerce-data.md)
   + [Configurar uma CSP](use-cases/configuring-a-csp.md)
   + [Depuração](use-cases/debugging.md)
   + [Desduplicação de eventos](use-cases/event-duplication.md)
   + Identidade {#identity}
      + [Visão geral](use-cases/identity/id-overview.md)
      + [IDs próprias para dispositivos](use-cases/identity/first-party-device-ids.md)
      + [Compartilhamento de ID](use-cases/identity/id-sharing.md)
   + [Várias instâncias do SDK](use-cases/multiple-instances.md)
   + Personalização {#personalization}
      + [Visão geral](use-cases/personalization/pers-overview.md)
      + [Exibir eventos](use-cases/personalization/display-events.md)
      + [Gerenciar cintilação](use-cases/personalization/manage-flicker.md)
      + [Renderização de conteúdo personalizado](use-cases/personalization/rendering-personalization-content.md)
      + [Eventos de página superior e inferior](use-cases/personalization/top-bottom-page-events.md)
