---
title: getLibraryInfo
description: Recupere informações sobre a versão atual da biblioteca do Web SDK.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# `getLibraryInfo`

O comando `getLibraryInfo` fornece informações sobre a versão da biblioteca Web SDK usada no momento. Você pode usar esse comando para rastrear quais versões do Web SDK você implanta em diferentes propriedades da Web.

Execute o comando `getLibraryInfo` ao chamar a instância configurada do Web SDK. Normalmente, esse comando é emparelhado com uma promessa do JavaScript que permite recuperar os objetos preenchidos.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Objeto de resposta

Se você decidir [manipular respostas](command-responses.md) com este comando, as seguintes propriedades estarão disponíveis no objeto de resposta:

* **`libraryInfo.commands`**: Uma matriz de comandos à qual esta versão do Web SDK dá suporte.
* **`libraryInfo.configs`**: uma matriz de definições de configuração à qual esta versão do Web SDK dá suporte.
* **`libraryInfo.version`**: a versão da biblioteca Web SDK.

## Informações da biblioteca usando a extensão de tag do Web SDK

A extensão de tag não fornece uma interface para enviar esse comando. Use o editor de código personalizado após a sintaxe da biblioteca JavaScript.

Se você executar esse comando usando a extensão de tag, a versão da extensão de tag e a versão da biblioteca serão incluídas, concatenadas com um símbolo `+`. A versão da biblioteca do Web SDK é listada primeiro, seguida pela versão da extensão de tag.
