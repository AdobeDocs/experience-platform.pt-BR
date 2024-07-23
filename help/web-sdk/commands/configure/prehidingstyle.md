---
title: prehideStyle
description: Crie uma definição de CSS que permita o carregamento de conteúdo personalizado sem oscilação.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

A propriedade `prehidingStyle` permite definir um seletor de CSS para ocultar conteúdo personalizado até que ele seja carregado. Essa propriedade é importante em implementações síncronas do SDK da Web para evitar oscilação. A Adobe recomenda usar o [trecho pré-ocultação](../../personalization/manage-flicker.md) para implementações assíncronas do SDK da Web.

Os seletores de CSS definidos nesta propriedade começam a ocultar o conteúdo quando você executa o primeiro comando [`sendEvent`](../sendevent/overview.md) em uma página. O conteúdo não fica oculto quando uma resposta do Adobe é recebida, o que normalmente inclui conteúdo personalizado. O conteúdo também não fica oculto se o comando `sendEvent` falhar ou atingir o tempo limite.

Se você incluir `prehidingStyle` e o trecho pré-ocultação na implementação, o trecho pré-ocultação terá prioridade sobre essa propriedade de configuração.

## Estilo pré-ocultado usando a extensão de tag do SDK da Web

Selecione o botão **[!UICONTROL Fornecer estilo pré-ocultação]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Personalization] e selecione o botão **[!UICONTROL Fornecer estilo pré-ocultação]**.
1. Esse botão abre uma janela modal com um editor CSS. Insira o seletor de CSS desejado e o bloco de declaração, em seguida, clique em **[!UICONTROL Salvar]** para fechar a janela modal.
1. Clique em **[!UICONTROL Salvar]** nas configurações de extensão e publique suas alterações.

## Estilo pré-ocultado usando a biblioteca JavaScript do SDK da Web

Defina a cadeia de caracteres `prehidingStyle` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK da Web, nada ficará oculto ao executar o primeiro comando `sendEvent` em uma página. Defina esse valor com o seletor de CSS desejado e o bloco de declaração para bibliotecas carregadas de forma síncrona.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```
