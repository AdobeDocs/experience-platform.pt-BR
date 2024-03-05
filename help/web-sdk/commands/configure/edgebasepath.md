---
title: edgeBasePath
description: O caminho base do endpoint usado para interagir com os serviços da Adobe.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

A variável `edgeBasePath` altera o caminho de destino quando você interage com os serviços da Adobe. A maioria das organizações não precisa definir ou alterar essa propriedade.

## Caminho base de borda usando a extensão de tag do SDK da Web

Insira o texto desejado na caixa **[!UICONTROL Caminho base da borda]** campo de texto quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Configurações avançadas] e insira o valor desejado na caixa de diálogo **[!UICONTROL Caminho base da borda]** campo de texto.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Caminho base de borda usando a biblioteca JavaScript do SDK da Web

Defina o `edgeBasePath` campo de texto ao executar o `configure` comando. Se você omitir essa propriedade, o padrão será o valor de `ee`. O Adobe recomenda omitir essa propriedade na maioria das configurações.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
