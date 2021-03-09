---
title: Notas de versão do SDK da Web da Adobe Experience Platform
description: As notas de versão mais recentes do SDK da Web da Adobe Experience Platform.
keywords: SDK da Web da Adobe Experience Platform; SDK da Web da plataforma; SDK da Web; notas de versão;
translation-type: tm+mt
source-git-commit: b0e6d1f7cf7302bb3a7403bb18dfd8b7489d583e
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 6%

---


# Notas de versão

## Versão 2.4.0

* O SDK agora pode ser [instalado como um pacote npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* Adição de suporte para uma opção `out` ao [configurar o consentimento padrão](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), que elimina todos os eventos até o recebimento do consentimento (a opção `pending` existente enfileira os eventos e os envia depois que o consentimento é recebido).
* O retorno de chamada [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) agora pode ser usado para impedir o envio de um evento.
* Agora usa um mixin XDM em vez de `meta.personalization` ao enviar eventos sobre o conteúdo personalizado que está sendo renderizado ou clicado.
* O [comando getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) agora retorna a ID da região de borda ao lado da identidade.
* Os avisos e erros recebidos do servidor foram aprimorados e são tratados de forma mais apropriada.
* Adição de suporte para [Padrão de Consentimento 2.0 da Adobe](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* As preferências de consentimento, quando recebidas, são armazenadas em hash e no armazenamento local para uma integração otimizada entre CMPs, SDK da Web da plataforma e Rede de borda da plataforma. Se você estiver coletando preferências de consentimento, agora incentivamos você a chamar `setConsent` em cada carregamento de página.
* Dois [ganchos de monitoramento](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` e `onCommandRejected` foram adicionados.
* Correção de erros: Os eventos de notificação de interação de personalização conteriam informações duplicadas sobre a mesma atividade quando um usuário navegasse para uma nova visualização de aplicativo de página única, voltasse para a visualização original e clicasse em um elemento qualificado para conversão.
* Correção de erros: Se o primeiro evento enviado pelo SDK tivesse `documentUnloading` definido como `true`, [`sendBeacon`](https://developer.mozilla.org/pt-BR/docs/Web/API/Navigator/sendBeacon) seria usado para enviar o evento, resultando em um erro em relação a uma identidade que não estava sendo estabelecida.

## Versão 2.3.0

* Adição de suporte nonce para permitir políticas de segurança de conteúdo mais rigorosas.
* Adição do suporte de personalização para aplicativos de página única.
* Aprimorada a compatibilidade com outro código JavaScript na página que pode estar substituindo `window.console` APIs.
* Correção de erros: `sendBeacon` não estava sendo usado quando `documentUnloading` estava definido como `true` ou quando os cliques em links eram rastreados automaticamente.
* Correção de erros: Um link não seria rastreado automaticamente se o elemento da âncora contivesse conteúdo HTML.
* Correção de erros: Determinados erros do navegador que continham uma propriedade somente leitura `message` não eram tratados adequadamente, resultando em um erro diferente sendo exposto ao cliente.
* Correção de erros: A execução do SDK em um iframe resultaria em um erro se a página HTML do iframe fosse de um subdomínio diferente da página HTML da janela pai.

## Versão 2.2.0

* Correção de erros: O objeto Opt-in estava bloqueando o Alloy de fazer chamadas quando `idMigrationEnabled` é `true`.
* Correção de erros: Informe Alloy sobre as solicitações que devem retornar ofertas de personalização para evitar um problema de cintilação.

## Versão 2.1.0

* Remova o comando `syncIdentity` e suporte a transmissão dessas IDs no comando `sendEvent`.
* Suporte ao Padrão de consentimento IAB 2.0.
* Suporte à transmissão de IDs adicionais no comando `setConsent`.
* Suporte à substituição de `datasetId` no comando `sendEvent`.
* Suporte a Monitores de Alloy ([Leia mais](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passe `environment: browser` nos dados de contexto dos detalhes da implementação.
