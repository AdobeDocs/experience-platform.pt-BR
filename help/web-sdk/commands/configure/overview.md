---
title: Configurar o SDK da Web da Adobe Experience Platform
description: Use o comando configure para definir as configurações necessárias ao usar o SDK da Web.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Configurar o SDK da Web da Adobe Experience Platform

A configuração do SDK da Web é feita com o comando `configure`. A configuração do SDK da Web é uma etapa essencial e necessária que deve ocorrer sempre que a biblioteca ou extensão de tag for usada.

## Configurar o SDK da Web usando a extensão de tag {#configure-tag-extension}

Siga as etapas abaixo para configurar o SDK da Web por meio da extensão de tag.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Vá para a [página de configuração da extensão de tag do SDK da Web](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) para obter informações detalhadas sobre todas as opções de configuração.

Essas configurações são definidas sempre que a extensão é usada para enviar dados para o Adobe.

## Configuração do SDK da Web usando a biblioteca do JavaScript {#configure-js}

Execute o comando `configure`. Esse comando é necessário antes de chamar qualquer outro comando do SDK da Web, como [`sendEvent`](../sendevent/overview.md).

As propriedades [`datastreamId`](datastreamid.md) e [`orgId`](orgid.md) são obrigatórias. Todas as outras propriedades são opcionais, dependendo dos requisitos de implementação de sua organização.

Consulte o sumário deste guia do usuário para obter informações detalhadas sobre cada um dos comandos suportados.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
