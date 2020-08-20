---
title: Notas de versão do Adobe Experience Platform Web SDK
seo-title: Notas de versão do Adobe Experience Platform Web SDK
description: Notas de versão do Adobe Experience Platform Web SDK.
seo-description: Notas de versão do Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 3%

---


# Notas de versão

## Versão 2.1.0

* Remova o `syncIdentity` comando e o suporte para a transmissão dessas IDs no `sendEvent` comando.
* Suporte ao padrão de consentimento IAB 2.0.
* Suporte para passar IDs adicionais no `setConsent` comando.
* Suporte que substitui o `datasetId` no `sendEvent` comando.
* Suportar monitores de liga ([Leia mais](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Transmita `environment: browser` os dados de contexto dos detalhes da implementação.
