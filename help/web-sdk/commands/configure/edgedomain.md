---
title: edgeDomain
description: Determine o domínio raiz para o qual deseja enviar dados.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

A variável `edgeDomain` permite alterar o domínio para o qual o SDK da Web envia dados. Essa propriedade é usada com frequência por organizações que usam [cookies próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR). Os dados são enviados para o próprio domínio da organização, e um registro CNAME encaminha esses dados para o Adobe.

Sua organização determina o valor correto dessa propriedade ao configurar [cookies próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR). Uma organização normalmente usa um subdomínio dedicado para essa finalidade. Por exemplo, se você usar o domínio `example.com`, você pode configurar cookies próprios no `data.example.com`.

## Configurar um domínio de borda usando a extensão de tag do SDK da Web

Defina o **[!UICONTROL Domínio de borda]** campo de texto quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Localizar o campo de texto **[!UICONTROL Domínio de borda]**, em seguida, insira o valor desejado.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Configurar um domínio de borda usando a biblioteca JavaScript do SDK da Web

Defina o `edgeDomain` string ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK, o padrão será `edge.adobedc.net`. Defina esse valor se quiser substituir o domínio para o qual o SDK da Web envia dados.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
