---
title: debugEnabled
description: Use o código para ativar os recursos de depuração no Web SDK.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

A propriedade `debugEnabled` permite habilitar ou desabilitar a depuração usando o código do Web SDK. É uma das maneiras disponíveis de habilitar a [depuração](/help/collection/use-cases/debugging.md). Ativar a depuração na implementação pode ser mais conveniente do que outros métodos durante o desenvolvimento do site, quando você sempre deseja ativar a depuração. Esse método de depuração o ativa para todos os visitantes, de modo que não é recomendado para páginas de produção. Consulte a página de casos de uso [Depuração](/help/collection/use-cases/debugging.md) para obter mais maneiras de habilitar a depuração.

Defina o booleano `debugEnabled` como `true` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK, o padrão será `false`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## Habilitar depuração usando a extensão de tag do Web SDK

Não há opções de depuração disponíveis nativamente ao usar a extensão de tag do Web SDK. Use um [método de depuração alternativo](/help/collection/use-cases/debugging.md) ao configurar sua propriedade de marca.
