---
title: downloadLinkQualifier
description: Ajuda a determinar como o rastreamento automático de links qualifica os links de download.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Se você ativar o rastreamento automático de links usando [`clickCollectionEnabled`](clickcollectionenabled.md), o `downloadLinkQualifier` ajuda a determinar os critérios para que um URL seja considerado um link de download.

Essa propriedade é uma sequência de caracteres regex. Se o URL clicado corresponder a este regex, `xdm.web.webInteraction.type` está definida como `"download"`. Os links também são classificados imediatamente como um link de download se incluírem uma `download` atributo HTML. Se `clickCollectionEnabled` não estiver ativada, essa propriedade não fará nada.

## Baixar qualificador de link usando a extensão de tag do SDK da Web

Ativar o **[!UICONTROL Ativar a coleta de dados de cliques]** e insira o texto desejado em **[!UICONTROL Qualificador de link de download]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Coleta de dados] e marque a caixa de seleção **[!UICONTROL Ativar a coleta de dados de cliques]**.
1. Uma vez habilitado, o **[!UICONTROL Qualificador de link de download]** é exibida. Insira o valor desejado. Também há botões disponíveis para testar o regex e restaurar o valor padrão.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Baixar qualificador de link usando a biblioteca JavaScript do SDK da Web

Defina o `downloadLinkQualifier` string ao executar o `configure` comando. Se você omitir essa propriedade, ela assumirá como padrão o seguinte valor:

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
