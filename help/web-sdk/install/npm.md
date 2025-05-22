---
title: Instalar o Web SDK usando o pacote NPM
description: Use um pacote NPM para instalar e fazer referência à biblioteca Web SDK.
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: 8b6c958613923127880263679ce00ce359151300
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Instalar o Web SDK usando o pacote NPM

O Adobe Experience Platform Web SDK está disponível como um [pacote NPM](https://www.npmjs.com). A instalação do pacote NPM permite que você tenha controle do processo de criação da biblioteca JavaScript do Adobe Experience Platform Web SDK. O pacote NPM expõe os módulos do EcmaScript versão 5 ou os módulos do EcmaScript versão 2015 (ES6) destinados a serem executados no navegador.

```bash
npm install @adobe/alloy
```

O pacote NPM do Adobe Experience Platform Web SDK expõe uma função `createInstance`. A opção name transmitida para a função controla o prefixo usado no registro em log. Abaixo estão exemplos de uso do pacote.

## Uso do pacote como um módulo ECMAScript 2015 (ES6)

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>O pacote NPM depende de módulos CommonJS; portanto, ao usar um pacote, verifique se ele é compatível com módulos CommonJS. Alguns pacotes, como o [Rollup](https://rollupjs.org), exigem um [plug-in](https://www.npmjs.com/package/@rollup/plugin-commonjs) que ofereça suporte a CommonJS.

## Uso do pacote como um módulo ECMAScript 5

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```
