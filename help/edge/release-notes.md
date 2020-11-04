---
title: Notas de versão do SDK da Web da Adobe Experience Platform
seo-title: Notas de versão do SDK da Web da Adobe Experience Platform
description: Notas de versão do SDK da Web da Adobe Experience Platform.
seo-description: Notas de versão do SDK da Web da Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 14%

---


# Notas de versão

## Versão 2.3.0

* Adição de suporte único para permitir políticas de segurança de conteúdo mais rigorosas.
* Adicionado suporte à personalização para aplicativos de página única.
* Compatibilidade aprimorada com outros códigos JavaScript na página que podem estar substituindo `window.console` as APIs.
* Correção de erros: `sendBeacon` não estava sendo usado quando `documentUnloading` estava definido como `true` ou quando cliques em links eram acompanhados automaticamente.
* Correção de erros: Um link não seria rastreado automaticamente se o elemento âncora contivesse conteúdo HTML.
* Correção de erros: Determinados erros de navegador contendo uma propriedade somente leitura não foram tratados adequadamente, resultando em um erro diferente sendo exposto ao cliente. `message`
* Correção de erros: A execução do SDK em um iframe resultaria em um erro se a página HTML do iframe fosse de um subdomínio diferente da página HTML da janela pai.

## Versão 2.2.0

* Correção de erros: O objeto Opt-in estava bloqueando o Alloy de fazer chamadas quando `idMigrationEnabled` está `true`.
* Correção de erros: Informe o Alloy sobre solicitações que devem retornar ofertas de personalização para evitar problemas de oscilação.

## Versão 2.1.0

* Remova o `syncIdentity` comando e o suporte para a transmissão dessas IDs no `sendEvent` comando.
* Suporte ao padrão de consentimento IAB 2.0.
* Suporte para passar IDs adicionais no `setConsent` comando.
* Suporte que substitui o `datasetId` no `sendEvent` comando.
* Suportar monitores de liga ([Leia mais](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Transmita `environment: browser` os dados de contexto dos detalhes da implementação.
