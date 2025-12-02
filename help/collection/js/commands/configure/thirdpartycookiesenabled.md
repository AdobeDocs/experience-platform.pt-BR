---
title: thirdPartyCookiesEnabled
description: Permitir o uso de cookies de terceiros para identificar visitantes.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

A propriedade `thirdPartyCookiesEnabled` é um booliano que determina se o Web SDK define cookies em um contexto de terceiros. Ativar essa opção é útil se você quiser identificar visitantes entre subdomínios ou domínios pertencentes à sua organização. No entanto, muitos navegadores modernos limitam a configuração e a expiração de cookies de terceiros. Se o navegador de um visitante não suportar cookies de terceiros, essa propriedade não fará nada.

A propriedade `thirdPartyCookiesEnabled` também controla se um [`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk) pode ser solicitado nas chamadas [`getIdentity`](../getidentity.md).

Quando essa opção é ativada, o Web SDK usa o Adobe Audience Manager para ajudar a identificar um visitante. Quando essa opção está desativada, a chamada para o Audience Manager é desativada. Consulte [Compreender as chamadas para o domínio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=pt-BR) no guia do usuário do Audience Manager para obter mais informações.

Defina o booleano `thirdPartyCookiesEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o Web SDK, o padrão será `true`. Defina esse valor como `false` se não quiser que o Web SDK use o Audience Manager para ajudar a identificar visitantes.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## Ativar cookies de terceiros usando a extensão de tag da Web SDK

Esta configuração pode ser definida na extensão de marca do Web SDK usando [configurações de identidade](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies).
