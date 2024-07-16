---
title: targetMigrationEnabled
description: Permitir que o SDK da Web leia e grave cookies do Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

A propriedade `targetMigrationEnabled` é booliana e permite que o SDK da Web leia e grave os cookies mbox e mboxEdgeCluster que as bibliotecas do Adobe Target 1.x e 2.x usam. Essa opção permite preservar o perfil do visitante entre páginas que usam implementações anteriores do Adobe Target e páginas que usam o SDK da Web.

## Habilitar a migração do Target da at.js usando a extensão de tag do SDK da Web

Marque a caixa de seleção **[!UICONTROL Migrar destino do at.js para o SDK da Web]** ao [configurar a extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Personalization] e marque a caixa de seleção **[!UICONTROL Migrar do Target da at.js para o SDK da Web]**.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Habilitar a migração do Target da at.js usando a biblioteca JavaScript do SDK da Web

Defina o booleano `targetMigrationEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `false`. Defina esse valor como `true` se você tiver algumas páginas que ainda usam as bibliotecas do Adobe Target 1.x ou 2.x.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
