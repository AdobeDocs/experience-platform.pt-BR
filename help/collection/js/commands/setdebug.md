---
title: setDebug
description: Ative ou desative a configuração de depuração do Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

O comando `setDebug` permite entrar ou sair do modo de depuração no Web SDK. É uma das várias opções disponíveis para [depuração](../../use-cases/debugging.md). A Adobe aconselha ativar o modo de depuração em ambientes de desenvolvimento ou apenas em sua máquina local em ambientes de produção.

Execute o comando `setDebug` ao chamar a instância configurada do Web SDK. A única opção no objeto de configuração é `enabled`, que é um booleano que determina se o modo de depuração está habilitado.

```js
alloy("setDebug", {"enabled": true});
```

## Definir a depuração usando a extensão de tag do Web SDK

Chame [`_satellite.setDebug()`](/help/collection/tags/setdebug.md) no console do navegador em uma página em que uma biblioteca de tags esteja implementada. A extensão de tag do Web SDK não oferece a capacidade de alternar opções de depuração na própria interface do usuário de tags.
