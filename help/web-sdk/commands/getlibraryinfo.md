---
title: getLibraryInfo
description: Recupere informações sobre a versão atual da biblioteca do SDK da Web.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

A variável `getLibraryInfo` O comando fornece informações sobre a versão da biblioteca do SDK da Web usada no momento. Você pode usar este comando para rastrear quais versões do SDK da Web você implantou em diferentes propriedades da Web.

## Informações da biblioteca usando a extensão de tag do SDK da Web

A extensão de tag não fornece uma interface para enviar esse comando. Use o editor de código personalizado após a sintaxe da biblioteca JavaScript.

Se você executar esse comando usando a extensão de tag, a versão da extensão de tag e a versão da biblioteca serão incluídas, concatenadas com uma `+` símbolo. A versão da biblioteca do SDK da Web é listada primeiro, seguida pela versão da extensão de tag.

## Informações da biblioteca usando a biblioteca JavaScript do SDK da Web

Execute o `getLibraryInfo` ao chamar a instância configurada do SDK da Web. Normalmente, esse comando é emparelhado com uma promessa JavaScript que permite recuperar os objetos preenchidos.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Objeto de resposta

Se você decidir [lidar com respostas](command-responses.md) com esse comando, as seguintes propriedades estão disponíveis no objeto de resposta:

* **`libraryInfo.commands`**: uma matriz de comandos à qual esta versão do SDK da Web dá suporte.
* **`libraryInfo.configs`**: uma matriz de definições de configuração à qual esta versão do SDK da Web dá suporte.
* **`libraryInfo.version`**: a versão da biblioteca do SDK da Web.
