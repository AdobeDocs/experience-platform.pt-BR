---
title: Instalar o SDK da Web usando o pacote NPM
description: Use um pacote NPM para instalar e fazer referência à biblioteca do SDK da Web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Instalar o SDK da Web usando o pacote NPM

O Adobe Experience Platform Web SDK está disponível como um [Pacote NPM](https://www.npmjs.com). A instalação do pacote NPM permite que você tenha controle do processo de criação da biblioteca JavaScript do SDK da Web da Adobe Experience Platform. O pacote NPM expõe os módulos do EcmaScript versão 5 ou os módulos do EcmaScript versão 2015 (ES6) destinados a serem executados no navegador.

```bash
npm install @adobe/alloy
```

O pacote NPM do SDK da Web do Adobe Experience Platform expõe uma `createInstance` função. A opção name transmitida para a função controla o prefixo usado no registro em log. Abaixo estão exemplos de uso do pacote.

## Uso do pacote como um módulo ECMAScript 2015 (ES6)

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>O pacote NPM depende de módulos CommonJS; portanto, ao usar um pacote, verifique se ele é compatível com módulos CommonJS. Alguns pacotes, como [Acúmulo](https://rollupjs.org), exigem uma [plug-in](https://www.npmjs.com/package/@rollup/plugin-commonjs) que fornece suporte a CommonJS.

## Uso do pacote como um módulo ECMAScript 5

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
