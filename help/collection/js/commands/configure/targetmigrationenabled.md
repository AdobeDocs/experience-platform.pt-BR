---
title: targetMigrationEnabled
description: Permitir que o Web SDK leia e grave cookies do Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: dade74bf4a5cfd7b60eaf216583deb67b93a61db
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# `targetMigrationEnabled`

A propriedade `targetMigrationEnabled` é um booleano que permite que o Web SDK leia e grave os [`mbox` e `mboxEdgeCluster` cookies](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/data-collection/cookies/web-sdk) que as bibliotecas Adobe Target 1.x e 2.x usam. Essa opção permite preservar o perfil do visitante entre páginas que usam implementações anteriores do Adobe Target e páginas que usam o Web SDK.

Defina o booleano `targetMigrationEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o Web SDK, o padrão será `false`. Defina esse valor como `true` se você tiver algumas páginas que ainda usam as bibliotecas do Adobe Target 1.x ou 2.x.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Habilitar a migração do Target usando a extensão de tag da Web SDK

Esta configuração pode ser definida na extensão de tag do Web SDK usando [as configurações do Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
