---
title: thirdPartyCookiesEnabled
description: Permitir o uso de cookies de terceiros para identificar visitantes.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

>[!IMPORTANT]
>
>Google [anunciou](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) planeja descontinuar o suporte do Chrome para cookies de terceiros no segundo semestre de 2024. Consequentemente, os cookies de terceiros não serão mais compatíveis com a maioria dos navegadores.
>
>Quando essa alteração for implementada, o Adobe descontinuará o suporte para o `demdex` cookie atualmente compatível com o SDK da Web.


A variável `thirdPartyCookiesEnabled` é um booliano que determina se o SDK da Web define cookies em um contexto de terceiros. Ativar essa opção é útil se você quiser identificar visitantes entre subdomínios ou domínios pertencentes à sua organização. No entanto, muitos navegadores modernos limitam a configuração e a expiração de cookies de terceiros.

Quando esta opção é ativada, o SDK da Web usa o Adobe Audience Manager para ajudar a identificar um visitante. Quando essa opção está desativada, a chamada para o Audience Manager é desativada. Consulte [Compreender as chamadas para o domínio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=pt-BR) no guia do usuário Audience Manager para obter mais informações.

## Ativar cookies de terceiros usando a extensão de tag do SDK da Web

Selecione o **[!UICONTROL Usar cookies de terceiros]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Identidade] e marque a caixa de seleção **[!UICONTROL Usar cookies de terceiros]**.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Ativar cookies de terceiros usando a biblioteca JavaScript do SDK da Web

Defina o `thirdPartyCookiesEnabled` booleano ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `true`. Defina esse valor como `false` se não quiser que o SDK da Web use o Audience Manager para ajudar a identificar visitantes.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
