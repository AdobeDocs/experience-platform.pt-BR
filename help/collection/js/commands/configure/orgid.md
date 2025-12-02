---
title: orgId
description: A propriedade orgId é uma string que informa à Adobe para qual organização os dados são enviados.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

A propriedade `orgId` é uma cadeia de caracteres que informa à Adobe para qual organização os dados são enviados. **Esta propriedade é necessária para todos os dados enviados usando o Web SDK.**

Para localizar seu `orgID`:

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Em qualquer lugar na Adobe Experience Cloud, pressione **`[Ctrl]`** + **`[I]`**. Uma janela [!UICONTROL User Data Debugger] é aberta.
1. Clique em **[!UICONTROL Copy]** ![Copiar](../../assets/copy.png) ao lado de [!UICONTROL Current Org ID] ou clique na guia **[!UICONTROL Assigned Orgs]** para ver outras IDs da organização que você pode acessar.
1. Quando terminar de localizar as informações desejadas, clique em **[!UICONTROL Close]**.

As IDs de organização são sempre cadeias alfanuméricas de 24 caracteres e sempre terminam em `@AdobeOrg`.

Defina a cadeia de caracteres `orgId` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o Web SDK, o Web SDK emitirá um erro de console e os dados não serão enviados para o Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## Defina a ID da organização usando a extensão de tag do Web SDK

Esta configuração pode ser definida na extensão de marca do Web SDK usando as [configurações da instância do SDK](/help/tags/extensions/client/web-sdk/configure/general.md). O campo é preenchido automaticamente com base na organização na qual a propriedade de tag foi criada.
