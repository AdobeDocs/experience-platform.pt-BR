---
title: edgeBasePath
description: O caminho base do endpoint usado para interagir com os serviços da Adobe.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

A propriedade `edgeBasePath` altera o caminho de destino quando você interage com os serviços da Adobe. A maioria das organizações não precisa definir ou alterar essa propriedade.

## Caminho básico do Edge usando a extensão de tag do SDK da Web

Insira o texto desejado no campo de texto **[!UICONTROL caminho base do Edge]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Configurações avançadas] e insira o valor desejado no campo de texto **[!UICONTROL caminho base do Edge]**.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Caminho básico do Edge usando a biblioteca JavaScript do SDK da Web

Definir o campo de texto `edgeBasePath` ao executar o comando `configure`. Se você omitir essa propriedade, o padrão será o valor de `ee`. O Adobe recomenda omitir essa propriedade na maioria das configurações.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```
