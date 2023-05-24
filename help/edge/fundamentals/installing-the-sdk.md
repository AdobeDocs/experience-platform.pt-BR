---
title: Instalar o SDK da Web da Adobe Experience Platform
description: Saiba como instalar o SDK da Web do Experience Platform.
keywords: instalação do sdk da web;instalando o sdk da web;internet explorer;promessa;pacote npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: e0fc9708edec3b36bed9925f12fca9db8b477262
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 2%

---

# Instalar o SDK {#installing-the-sdk}

Há três maneiras compatíveis de usar o SDK da Web da Adobe Experience Platform:

1. A maneira preferida de usar o SDK da Web da Adobe Experience Platform é por meio da interface da Coleção de dados ou da interface do Experience Platform.
1. O Adobe Experience Platform Web SDK também está disponível em uma rede de entrega de conteúdo (CDN) para você usar.
1. Use a biblioteca NPM que exporta os módulos EcmaScript 5 e EcmaScript 2015 (ES6).

## Opção 1: instalação da extensão de tag

Para obter a documentação sobre a extensão de tag, consulte [Documentação de tags](../../tags/extensions/client/sdk/overview.md)

## Opção 2: instalar a versão independente pré-criada

A versão pré-criada está disponível em um CDN. Você pode fazer referência à biblioteca na CDN diretamente na sua página ou baixá-la e hospedá-la em sua própria infraestrutura. Ele está disponível em formatos minificados e não minificados. A versão não reduzida é útil para fins de depuração.

Estrutura de URL: https://cdn1.adoberesources.net/alloy/[VERSÃO]/alloy.min.js OU alloy.js para a versão não minificada.

Por exemplo:


* Minificado: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js)
* Não minificado: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js)


### Adição do código {#adding-the-code}

A versão independente pré-criada requer um &quot;código base&quot; adicionado diretamente à página. Copie e cole o &quot;código base&quot; a seguir o mais alto possível na variável `<head>` tag do seu HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

O &quot;código base&quot; cria uma função global chamada `alloy`. Use esta função para interagir com o SDK. Se você quiser nomear a função global como algo diferente, altere a `alloy` nome da seguinte forma:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

Neste exemplo, a função global é renomeada `mycustomname`, em vez de `alloy`.

>[!IMPORTANT]
>
>Para evitar possíveis problemas, use um nome que contenha pelo menos um caractere que não seja um dígito e não entre em conflito com o nome de uma propriedade já encontrada em `window`.

Esse código base, além de criar uma função global, também carrega o código adicional contido em um arquivo externo \(`alloy.js`\) hospedado em um servidor. Por padrão, esse código é carregado de forma assíncrona para permitir que a página da Web tenha o máximo de desempenho possível. Essa é a implementação recomendada.

### Suporte ao Internet Explorer {#support-internet-explore}

Esse SDK usa promessas, que são um método de comunicar a conclusão de tarefas assíncronas. A variável [Promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) a implementação usada pelo SDK é nativamente compatível com todos os navegadores de destino, exceto [!DNL Internet Explorer]. Para usar o SDK em [!DNL Internet Explorer], você deve ter `window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar se você já tem `window.Promise` polyfilled:

1. Abra o site em [!DNL Internet Explorer].
1. Abra o console de depuração do navegador.
1. Tipo `window.Promise` no console e pressione Enter.

Se algo diferente de `undefined` for exibida, provavelmente você já está com polyfill `window.Promise`. Outra maneira de determinar se `window.Promise` O é polyfilled (polipreenchimento) ao carregar seu site depois de concluir as instruções de instalação acima. Se o SDK lançar um erro mencionando algo sobre uma promessa, é provável que você não tenha preenchido tudo `window.Promise`.

Se você determinou que você deve preencher em polyfill `window.Promise`, inclua a seguinte tag de script acima do código base fornecido anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Essa tag carrega um script que garante que `window.Promise` é uma implementação Promise válida.

>[!NOTE]
>
>Se optar por carregar uma implementação do Promise diferente, verifique se ela suporta `Promise.prototype.finally`.

### Carregamento do arquivo JavaScript de forma síncrona {#loading-javascript-synchronously}

Conforme explicado na seção [Adição do código](#adding-the-code), o código base que você copiou e colou no HTML do seu site carrega um arquivo externo. O arquivo externo contém a funcionalidade principal do SDK. Qualquer comando que você tentar executar enquanto esse arquivo é carregado será enfileirado e processado depois que o arquivo for carregado. O carregamento assíncrono do arquivo é o método de instalação mais eficiente.

No entanto, em determinadas circunstâncias, talvez você queira carregar o arquivo de forma síncrona \(mais detalhes sobre essas circunstâncias serão documentados posteriormente\). Isso bloqueia a análise e a renderização do restante do documento HTML pelo navegador até que o arquivo externo seja carregado e executado. Normalmente, esse atraso adicional antes de exibir o conteúdo principal aos usuários não é recomendado, mas pode fazer sentido dependendo das circunstâncias.

Para carregar o arquivo de forma síncrona em vez de assíncrona, remova a variável `async` atributo do segundo `script` conforme mostrado abaixo:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>
```

## Opção 3: uso do pacote NPM

O Adobe Experience Platform Web SDK também está disponível como um pacote NPM. [NPM](https://www.npmjs.com) é o gerenciador de pacotes do JavaScript. A instalação do pacote NPM permite que você tenha controle do processo de criação do JavaScript do SDK da Web da Adobe Experience Platform. O pacote NPM expõe os módulos do EcmaScript versão 5 ou os módulos do EcmaScript versão 2015 (ES6) destinados a serem executados no navegador.

```bash
npm install @adobe/alloy
```

O pacote NPM do SDK da Web do Adobe Experience Platform expõe uma `createInstance` função. Esta função é usada para criar uma instância. A opção name transmitida para a função controla o prefixo usado no registro em log. Abaixo estão exemplos de uso do pacote.

### Uso do pacote como um módulo ECMAScript 2015 (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>O pacote NPM depende de módulos CommonJS; portanto, ao usar um pacote, verifique se ele é compatível com módulos CommonJS. Alguns pacotes, como [Acúmulo](https://rollupjs.org), exigem uma [plug-in](https://www.npmjs.com/package/@rollup/plugin-commonjs) que fornece suporte a CommonJS.

### Uso do pacote como um módulo ECMAScript 5

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Suporte ao Internet Explorer

O SDK do Adobe Experience Platform usa promessas, que são um método de comunicar a conclusão de tarefas assíncronas. A variável [Promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) a implementação usada pelo SDK é nativamente compatível com todos os navegadores de destino, exceto [!DNL Internet Explorer]. Para usar o SDK em [!DNL Internet Explorer], você deve ter `window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Uma biblioteca que você poderia usar para polyfill promessa é promessa-polyfill. Consulte a [documentação de promessa-polyfill](https://www.npmjs.com/package/promise-polyfill) para obter mais informações sobre como instalar com NPM.

>[!NOTE]
>
>Se optar por carregar uma implementação do Promise diferente, verifique se ela suporta `Promise.prototype.finally`.
