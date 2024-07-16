---
title: edgeDomain
description: Determine o domínio raiz para o qual deseja enviar dados.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

A propriedade `edgeDomain` permite alterar o domínio para o qual o SDK da Web envia dados. Esta propriedade é usada com frequência por organizações que usam [cookies próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR). Os dados são enviados para o próprio domínio da organização, e um registro CNAME encaminha esses dados para o Adobe.

Sua organização determina o valor correto dessa propriedade ao configurar [cookies próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR). Uma organização normalmente usa um subdomínio dedicado para essa finalidade. Por exemplo, se você usar o domínio `example.com`, poderá configurar cookies próprios em `data.example.com`.

## Configurar um domínio de borda usando a extensão de tag do SDK da Web

Defina o campo de texto **[!UICONTROL domínio Edge]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Localize o campo de texto **[!UICONTROL domínio Edge]** e insira o valor desejado.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Configurar um domínio de borda usando a biblioteca JavaScript do SDK da Web

Defina a cadeia de caracteres `edgeDomain` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK, o padrão será `edge.adobedc.net`. Defina esse valor se quiser substituir o domínio para o qual o SDK da Web envia dados.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
