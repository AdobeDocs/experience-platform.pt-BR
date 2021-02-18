---
title: Notas de versão do SDK da Web da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Plataforma Web SDK;Web SDK;notas de versão;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 5%

---


# Notas de versão

## Versão 2.3.0

* Adição de suporte único para permitir políticas de segurança de conteúdo mais rigorosas.
* Adicionado suporte à personalização para aplicativos de página única.
* Compatibilidade aprimorada com outros códigos JavaScript na página que podem estar substituindo `window.console` APIs.
* Correção de erros: `sendBeacon` não estava sendo usado quando `documentUnloading` estava definido como `true` ou quando cliques em links eram acompanhados automaticamente.
* Correção de erros: Um link não seria rastreado automaticamente se o elemento âncora contivesse conteúdo HTML.
* Correção de erros: Determinados erros de navegador contendo uma propriedade somente leitura `message` não foram tratados adequadamente, resultando em um erro diferente sendo exposto ao cliente.
* Correção de erros: A execução do SDK em um iframe resultaria em um erro se a página HTML do iframe fosse de um subdomínio diferente da página HTML da janela pai.

## Versão 2.2.0

* Correção de erros: O objeto Opt-in estava bloqueando o Alloy de fazer chamadas quando `idMigrationEnabled` é `true`.
* Correção de erros: Informe o Alloy sobre solicitações que devem retornar ofertas de personalização para evitar problemas de oscilação.

## Versão 2.1.0

* Remova o comando `syncIdentity` e suporte a transmissão dessas IDs no comando `sendEvent`.
* Suporte ao padrão de consentimento IAB 2.0.
* Suporte para a transmissão de IDs adicionais no comando `setConsent`.
* Suporte que substitui `datasetId` no comando `sendEvent`.
* Suportar Monitores de Ligação ([Leia mais](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passe `environment: browser` nos dados de contexto dos detalhes da implementação.
