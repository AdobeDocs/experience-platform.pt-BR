---
title: getVar()
description: Retorna o valor de um elemento de dados ou um conjunto de valores usando setVar().
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# `getVar()`

O método `_satellite.getVar()` retorna o valor atual de um [Elemento de dados](/help/tags/ui/managing-resources/data-elements.md) ou um conjunto de valores usando [`_satellite.setVar()`](setvar.md). Se um elemento de dados e um valor `setVar()` compartilharem o mesmo nome, o elemento de dados terá prioridade. Se você chamar um identificador de cadeia de caracteres que ainda não existe, o método retornará `undefined`. A avaliação é síncrona.

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

O valor e o tipo de retorno dependem do tipo de elemento de dados referenciado. Por exemplo, se você chamar `getVar()`, que recupera uma variável de cadeia de caracteres, o tipo retornado será `string`. Se você chamar `getVar()` que retorna um elemento de dados de variável do Web SDK, o tipo retornado será um `object` contendo todas as propriedades definidas nessa variável.

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## Campos disponíveis

O método `getVar()` dá suporte a dois argumentos. A maioria dos casos de uso não inclui o segundo argumento opcional.

| Nome | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| **`name`** | `string` | Sim | O nome do elemento de dados que você deseja recuperar. Os nomes dos elementos de dados fazem distinção entre maiúsculas e minúsculas. |
| **`event`** | `object` | Não | Contexto de evento da regra de acionamento. Usado apenas em casos de uso avançados por elementos de dados que usam o [código personalizado](/help/tags/ui/managing-resources/data-elements.md#custom-code) ou extensões personalizadas. Quando uma regra é acionada por um evento (como um clique, envio de formulário ou despacho JavaScript personalizado), o objeto de evento associado é incluído aqui. Os elementos de dados podem usar essas informações para retornar valores contextuais, como os detalhes do elemento clicado ou as propriedades de um evento personalizado. |
