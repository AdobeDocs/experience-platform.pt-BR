---
title: Configurar o SDK da Web da Adobe Experience Platform
description: Use o comando configure para definir as configurações necessárias ao usar o SDK da Web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Configurar o SDK da Web da Adobe Experience Platform

A configuração do SDK da Web é feita com o `configure` comando. A configuração do SDK da Web é uma etapa essencial e necessária que deve ocorrer sempre que a biblioteca ou extensão de tag for usada.

## Configurações usando a extensão de tag do SDK da Web

Navegue até a [página de configuração de extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.

Essas configurações são definidas sempre que a extensão é usada para enviar dados para o Adobe.

## Configurações usando a biblioteca JavaScript do SDK da Web

Execute o `configure` comando. Esse comando é necessário antes de chamar qualquer outro comando do SDK da Web, como [`sendEvent`](../sendevent/overview.md). As propriedades [`edgeConfigId`](edgeconfigid.md) e [`orgId`](orgid.md) são obrigatórios. Todas as outras propriedades são opcionais, dependendo dos requisitos de implementação de sua organização.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
