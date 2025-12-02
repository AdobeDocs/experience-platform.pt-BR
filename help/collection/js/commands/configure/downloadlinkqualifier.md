---
title: downloadLinkQualifier
description: Ajuda a determinar como o rastreamento automático de links qualifica os links de download.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

Se você habilitar o rastreamento automático de links usando o [`clickCollectionEnabled`](clickcollectionenabled.md), a propriedade `downloadLinkQualifier` ajudará a determinar os critérios para uma URL ser considerada um link de download.

Essa propriedade é uma sequência de caracteres regex. Se a URL clicada corresponder a este regex, `xdm.web.webInteraction.type` será definido como `"download"`. Os links também são classificados imediatamente como um link de download se incluírem um atributo do HTML `download`. Se `clickCollectionEnabled` não estiver habilitado, esta propriedade não fará nada.

Defina a cadeia de caracteres `downloadLinkQualifier` ao executar o comando `configure`. Se você omitir essa propriedade, ela assumirá como padrão o seguinte valor:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Se você quiser usar critérios diferentes para qualificar links de download, defina essa propriedade com o valor de regex desejado.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## Baixar qualificador de link usando a extensão de tag do Web SDK

O equivalente da extensão de tag do Web SDK deste campo está em [Configurações da coleção de dados](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier) ao configurar a extensão de tag.
