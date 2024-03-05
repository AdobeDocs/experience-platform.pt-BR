---
title: orgId
description: A propriedade orgId é uma string que informa ao Adobe para qual organização os dados são enviados.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

A variável `orgId` propriedade é uma string que informa ao Adobe para qual organização os dados são enviados. **Essa propriedade é necessária para todos os dados enviados usando o SDK da Web.**

Para localizar seu `orgID`:

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Em qualquer lugar na Adobe Experience Cloud, pressione **`[Ctrl]`** + **`[I]`**. A [!UICONTROL Depurador de dados do usuário] é aberta.
1. Clique em **[!UICONTROL Copiar]** ![Copiar](../../assets/copy.png) ao lado da [!UICONTROL ID da organização atual]ou clique no link **[!UICONTROL Organizações atribuídas]** para ver outras IDs da organização que você pode acessar.
1. Quando terminar de localizar as informações desejadas, clique em **[!UICONTROL Fechar]**.

As IDs da organização são sempre cadeias alfanuméricas de 24 caracteres e sempre terminam em `@AdobeOrg`.

## Configurar um `orgID` uso da extensão de tag do SDK da Web

Insira a ID da organização no **[!UICONTROL IMS organization ID]** campo de texto quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Insira a ID da organização desejada na [!UICONTROL IMS organization ID] campo de texto próximo à parte superior.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Configurar um `orgID` uso da biblioteca JavaScript do SDK da Web

Defina o `orgId` string ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK da Web, o SDK da Web emitirá um erro de console e os dados não serão enviados para o Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
