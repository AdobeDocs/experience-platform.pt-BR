---
title: setDebug()
description: Ative a depuração no site por meio do console do navegador.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

O método `_satellite.setDebug()` permite habilitar ou desabilitar a [Depuração](../use-cases/debugging.md) no site. Esse método deve ser executado localmente no console do navegador; a Adobe recomenda não chamar esse método nas regras de tag.

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**: Permite [Depuração](../use-cases/debugging.md). As mensagens geradas pela biblioteca de tags (incluindo [`_satellite.logger`](logger.md)) estão visíveis no console do navegador.
* **`_satellite.setDebug(false);`**: Desabilita a depuração. As mensagens de console geradas pela biblioteca de tags não estão visíveis.

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>As mensagens gravadas com o `console.log()` nativo do JavaScript são sempre visíveis para qualquer pessoa com DevTools aberto. A Adobe recomenda usar o [`_satellite.logger`](logger.md) quando possível.

## Persistência do modo de depuração

Ao chamar esse método, o modo de depuração usa o seguinte escopo:

* **Sessão do navegador**: o modo de depuração persiste entre carregamentos de página. Ela permanece ativada até que você encerre a sessão do navegador ou a desative explicitamente.
* **Com escopo de origem**: o modo de depuração persiste somente para o mesmo site (domínio + porta + protocolo).
* **Por perfil de navegador**: o modo de depuração não é entre perfis.

Outras formas de [Depuração](../use-cases/debugging.md) podem afetar e substituir o modo de depuração usando o método do console do navegador.
