---
title: thirdPartyCookiesEnabled
description: Permitir o uso de cookies de terceiros para identificar visitantes.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

A propriedade `thirdPartyCookiesEnabled` é um booliano que determina se o SDK da Web define cookies em um contexto de terceiros. Ativar essa opção é útil se você quiser identificar visitantes entre subdomínios ou domínios pertencentes à sua organização. No entanto, muitos navegadores modernos limitam a configuração e a expiração de cookies de terceiros.

A propriedade `thirdPartyCookiesEnabled` também controla se um [`CORE ID`](../../identity/overview.md#tracking-coreid-web-sdk) pode ser solicitado nas chamadas [`getIdentity`](../getidentity.md).

Quando esta opção é ativada, o SDK da Web usa o Adobe Audience Manager para ajudar a identificar um visitante. Quando essa opção está desativada, a chamada para o Audience Manager é desativada. Consulte [Compreender as chamadas para o domínio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=pt-BR) no guia do usuário do Audience Manager para obter mais informações.

## Ativar cookies de terceiros usando a extensão de tag do SDK da Web

Marque a caixa de seleção **[!UICONTROL Usar cookies de terceiros]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Identidade] e marque a caixa de seleção **[!UICONTROL Usar cookies de terceiros]**.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Ativar cookies de terceiros usando a biblioteca JavaScript do SDK da Web

Defina o booleano `thirdPartyCookiesEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `true`. Defina esse valor como `false` se você não quiser que o SDK da Web use o Audience Manager para ajudar a identificar visitantes.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```
