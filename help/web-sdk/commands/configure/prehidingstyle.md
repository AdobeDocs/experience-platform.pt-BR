---
title: prehideStyle
description: Crie uma definição de CSS que permita o carregamento de conteúdo personalizado sem oscilação.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

A variável `prehidingStyle` permite definir um seletor de CSS para ocultar o conteúdo personalizado até que seja carregado. Essa propriedade é importante em implementações síncronas do SDK da Web para evitar oscilação. O Adobe recomenda o uso de [pré-ocultação de trecho](../../personalization/manage-flicker.md) para implementações assíncronas do SDK da Web.

Os seletores de CSS definidos nesta propriedade começam a ocultar o conteúdo quando você executa o primeiro [`sendEvent`](../sendevent/overview.md) em uma página. O conteúdo não fica oculto quando uma resposta do Adobe é recebida, o que normalmente inclui conteúdo personalizado. O conteúdo também não fica oculto se a variável `sendEvent` falha ou atinge o tempo limite.

Se você incluir ambos `prehidingStyle` e o trecho pré-ocultação na implementação, o trecho pré-ocultação tem prioridade sobre essa propriedade de configuração.

## Estilo pré-ocultado usando a extensão de tag do SDK da Web

Selecione o **[!UICONTROL Fornecer estilo pré-ocultação]** botão quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Personalização] e selecione o botão **[!UICONTROL Fornecer estilo pré-ocultação]**.
1. Esse botão abre uma janela modal com um editor CSS. Insira o seletor de CSS e o bloco de declaração desejados e clique em **[!UICONTROL Salvar]** para fechar a janela modal.
1. Clique em **[!UICONTROL Salvar]** em configurações de extensão, publique as alterações.

## Estilo pré-ocultado usando a biblioteca JavaScript do SDK da Web

Defina o `prehidingStyle` string ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK da Web, nada ficará oculto ao executar o primeiro `sendEvent` em uma página. Defina esse valor com o seletor de CSS desejado e o bloco de declaração para bibliotecas carregadas de forma síncrona.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
