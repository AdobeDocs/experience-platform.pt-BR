---
title: Notas de versão do Adobe Experience Platform Web SDK
seo-title: Notas de versão do Adobe Experience Platform Web SDK
description: Notas de versão do Adobe Experience Platform Web SDK.
seo-description: Notas de versão do Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 738dfe782ee7d6bef06d14910e0c26540b0ec734
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Notas de versão

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
