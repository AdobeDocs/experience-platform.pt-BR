---
title: setVar()
description: Define um valor que pode ser recuperado posteriormente usando getVar().
source-git-commit: 54c32803136bf37a13bb9ca14b1d1c7b09a2041c
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# `setVar()`

O método `_satellite.setVar()` permite definir um ou mais pares de nome/valor personalizados que podem ser referenciados posteriormente por [`_satellite.getVar()`](getvar.md).

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>Embora o método `getVar()` possa recuperar os elementos de dados e os valores definidos por `setVar()`, esses dois tipos de entidade são separados. Usar `setVar()` para definir um valor com o mesmo nome de um elemento de dados na interface de marcas não o substitui.

## Persistência e escopo

`setVar()` valores vivem somente na memória da página:

* **Somente página atual**: os valores persistem até que a página seja descarregada. Em aplicativos de página única, elas persistem até que seja totalmente recarregado ou você as sobrescreve/apaga.
* **Nenhum armazenamento de navegador**: nada é gravado em cookies, armazenamento local ou armazenamento de sessão.

## Fazendo referência a valores definidos usando `setVar()`

Você pode recuperar valores no código personalizado usando `getVar()`:

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

Você também pode fazer referência a essas variáveis na interface das tags em campos que oferecem suporte à notação de elementos de dados:

```text
%Ad location%
```

>[!NOTE]
>
>Se um conjunto de valores que usa `setVar()` usar o mesmo nome que um elemento de dados e você fizer referência a esse nome na notação do elemento de dados, o elemento de dados terá prioridade.

## Exemplos

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```

>[!NOTE]
>
>Evite usar pontos (`.`) ao definir nomes de variáveis usando esse método. O método `getVar()` não reconhece variáveis que contêm pontos definidos com o uso de `setVar()`. No entanto, `getVar()` _reconhece_ elementos de dados que usam períodos quando são definidos na interface do usuário de marcas.
