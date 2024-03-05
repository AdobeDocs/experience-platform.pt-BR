---
title: targetMigrationEnabled
description: Permitir que o SDK da Web leia e grave cookies do Adobe Target.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

A variável `targetMigrationEnabled` é uma propriedade booleana que permite que o SDK da Web leia e grave os cookies mbox e mboxEdgeCluster que as bibliotecas do Adobe Target 1.x e 2.x usam. Essa opção permite preservar o perfil do visitante entre páginas que usam implementações anteriores do Adobe Target e páginas que usam o SDK da Web.

## Habilitar a migração do Target da at.js usando a extensão de tag do SDK da Web

Selecione o **[!UICONTROL Migração do Target da at.js para o SDK da Web]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Personalização] e marque a caixa de seleção **[!UICONTROL Migração do Target da at.js para o SDK da Web]**.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Ative a migração do Target da at.js usando a biblioteca JavaScript do SDK da Web

Defina o `targetMigrationEnabled` booleano ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `false`. Defina esse valor como `true` se você tiver algumas páginas que ainda usam as bibliotecas Adobe Target 1.x ou 2.x.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
