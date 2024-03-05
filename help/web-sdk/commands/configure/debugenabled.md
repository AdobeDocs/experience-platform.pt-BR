---
title: debugEnabled
description: Use o código para ativar os recursos de depuração no SDK da Web.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

A variável `debugEnabled` permite ativar ou desativar a depuração usando o código do SDK da Web. É uma das maneiras disponíveis de ativar o [depuração](../../use-cases/debugging.md). Ativar a depuração na implementação pode ser mais conveniente do que outros métodos durante o desenvolvimento do site, quando você sempre deseja ativar a depuração. Esse método de depuração o ativa para todos os visitantes, de modo que não é recomendado para páginas de produção.

Consulte a [Depuração](../../use-cases/debugging.md) caso de uso para obter mais maneiras de ativar a depuração.

## Ativar a depuração usando a extensão de tag do SDK da Web

Não há opções de depuração disponíveis nativamente ao usar a extensão de tag do SDK da Web. Use um [método de depuração alternativo](../../use-cases/debugging.md).

## Ativar a depuração usando a biblioteca JavaScript do SDK da Web

Defina o `debugEnabled` booleano para `true` ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK, o padrão será `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
