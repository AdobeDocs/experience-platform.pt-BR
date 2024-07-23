---
title: debugEnabled
description: Use o código para ativar os recursos de depuração no SDK da Web.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

A propriedade `debugEnabled` permite habilitar ou desabilitar a depuração usando o código do SDK da Web. É uma das maneiras disponíveis de habilitar a [depuração](../../use-cases/debugging.md). Ativar a depuração na implementação pode ser mais conveniente do que outros métodos durante o desenvolvimento do site, quando você sempre deseja ativar a depuração. Esse método de depuração o ativa para todos os visitantes, de modo que não é recomendado para páginas de produção.

Consulte a página de casos de uso [Depuração](../../use-cases/debugging.md) para obter mais maneiras de habilitar a depuração.

## Ativar a depuração usando a extensão de tag do SDK da Web

Não há opções de depuração disponíveis nativamente ao usar a extensão de tag do SDK da Web. Use um [método de depuração alternativo](../../use-cases/debugging.md).

## Habilitar a depuração usando a biblioteca JavaScript do SDK da Web

Defina o booleano `debugEnabled` como `true` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK, o padrão será `false`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```
