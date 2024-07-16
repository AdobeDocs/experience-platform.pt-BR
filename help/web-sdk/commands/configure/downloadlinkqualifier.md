---
title: downloadLinkQualifier
description: Ajuda a determinar como o rastreamento automático de links qualifica os links de download.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Se você habilitar o rastreamento automático de links usando o [`clickCollectionEnabled`](clickcollectionenabled.md), a propriedade `downloadLinkQualifier` ajudará a determinar os critérios para uma URL ser considerada um link de download.

Essa propriedade é uma sequência de caracteres regex. Se a URL clicada corresponder a este regex, `xdm.web.webInteraction.type` será definido como `"download"`. Os links também são classificados imediatamente como um link de download se incluírem um atributo de HTML `download`. Se `clickCollectionEnabled` não estiver habilitado, esta propriedade não fará nada.

## Baixar qualificador de link usando a extensão de tag do SDK da Web

Habilite a caixa de seleção **[!UICONTROL Habilitar coleta de dados de cliques]** e insira o texto desejado em **[!UICONTROL Qualificador de link de download]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Coleção de dados] e marque a caixa de seleção **[!UICONTROL Habilitar coleta de dados de cliques]**.
1. Depois de habilitada, a caixa de texto **[!UICONTROL Qualificador de link de download]** é exibida. Insira o valor desejado. Também há botões disponíveis para testar o regex e restaurar o valor padrão.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Baixar qualificador de link usando a biblioteca JavaScript do SDK da Web

Defina a cadeia de caracteres `downloadLinkQualifier` ao executar o comando `configure`. Se você omitir essa propriedade, ela assumirá como padrão o seguinte valor:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Se você quiser usar critérios diferentes para qualificar links de download, defina essa propriedade com o valor de regex desejado.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
