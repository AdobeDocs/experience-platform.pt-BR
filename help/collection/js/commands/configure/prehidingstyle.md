---
title: prehideStyle
description: Crie uma definição de CSS que permita o carregamento de conteúdo personalizado sem oscilação.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

A propriedade `prehidingStyle` permite definir um seletor de CSS para ocultar conteúdo personalizado até que ele seja carregado. Essa propriedade é importante em implementações síncronas do Web SDK para evitar oscilação. A Adobe recomenda usar o [trecho pré-ocultação](/help/collection/use-cases/personalization/manage-flicker.md) para implementações assíncronas do Web SDK.

Os seletores de CSS definidos nesta propriedade começam a ocultar o conteúdo quando você executa o primeiro comando [`sendEvent`](../sendevent/overview.md) em uma página. O conteúdo não fica oculto quando uma resposta do Adobe é recebida, o que normalmente inclui conteúdo personalizado. O conteúdo também não fica oculto se o comando `sendEvent` falhar ou atingir o tempo limite.

Se você incluir `prehidingStyle` e o trecho pré-ocultação na implementação, o trecho pré-ocultação terá prioridade sobre essa propriedade de configuração.

Defina a cadeia de caracteres `prehidingStyle` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o Web SDK, nada ficará oculto ao executar o primeiro comando `sendEvent` em uma página. Defina esse valor com o seletor de CSS desejado e o bloco de declaração para bibliotecas carregadas de forma síncrona.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## Estilo pré-ocultado usando a extensão de tag do Web SDK

Essas configurações podem ser definidas na extensão de tag do Web SDK usando [as configurações do Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md).
