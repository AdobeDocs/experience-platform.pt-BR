---
title: orgId
description: A propriedade orgId é uma string que informa ao Adobe para qual organização os dados são enviados.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

A propriedade `orgId` é uma cadeia de caracteres que informa ao Adobe para qual organização os dados são enviados. **Esta propriedade é necessária para todos os dados enviados usando o SDK da Web.**

Para localizar seu `orgID`:

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Em qualquer lugar na Adobe Experience Cloud, pressione **`[Ctrl]`** + **`[I]`**. Uma janela [!UICONTROL Depurador de Dados de Usuário] é aberta.
1. Clique em **[!UICONTROL Copiar]** ![Copiar](../../assets/copy.png) ao lado da [!UICONTROL ID da Organização Atual] ou clique na guia **[!UICONTROL Organizações Atribuídas]** para ver outras IDs da organização que você pode acessar.
1. Quando você terminar de localizar as informações desejadas, clique em **[!UICONTROL Fechar]**.

As IDs de organização são sempre cadeias alfanuméricas de 24 caracteres e sempre terminam em `@AdobeOrg`.

## Configurar um `orgID` usando a extensão de tag do SDK da Web

Insira a ID da organização no campo de texto **[!UICONTROL ID da organização IMS]** ao [configurar a extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Insira a ID da organização desejada no campo de texto [!UICONTROL ID da organização IMS] próximo à parte superior.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Configurar um `orgID` usando a biblioteca JavaScript do SDK da Web

Defina a cadeia de caracteres `orgId` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK da Web, o SDK da Web emitirá um erro de console e os dados não serão enviados para o Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
