---
title: Instalar o SDK da Web da Adobe Experience Platform
description: Saiba como instalar o SDK da Web do Experience Platform.
keywords: instalação do sdk da web; instalação do sdk da web; internet explorer; promessa; pacote npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 2%

---

# Instalar o SDK {#installing-the-sdk}

Há três maneiras compatíveis de usar o Adobe Experience Platform Web SDK:

1. A maneira preferida de usar o SDK da Web do Adobe Experience Platform é via [Adobe Experience Platform Launch](https://launch.adobe.com/).
1. O SDK da Web da Adobe Experience Platform também está disponível em uma rede de entrega de conteúdo (CDN) para você usar.
1. Use a biblioteca NPM que exporta módulos EcmaScript 5 e EcmaScript 2015 (ES6).

## Opção 1: Instalação da extensão Adobe Experience Platform Launch

Para obter a documentação sobre a extensão Adobe Experience Platform Launch, consulte a [documentação de inicialização](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)

## Opção 2: Instalação da versão independente pré-criada

A versão pré-criada está disponível em um CDN. Você pode fazer referência à biblioteca no CDN diretamente na sua página ou baixá-la e hospedá-la em sua própria infraestrutura. Ele está disponível em formatos minificados e não minificados. A versão não minificada é útil para fins de depuração.

Estrutura do URL: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OU alloy.js para a versão não minificada.

Por exemplo:


* Minificado: [https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js)
* Não minificado: [https://cdn1.adoberesources.net/alloy/2.4.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.4.0/alloy.js)


### Adicionar o código {#adding-the-code}

A versão independente pré-criada requer um &quot;código base&quot; adicionado diretamente à página. Copie e cole o seguinte &quot;código base&quot; o mais alto possível na tag `<head>` do seu HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js" async></script>
```

O &quot;código base&quot; cria uma função global chamada `alloy`. Use essa função para interagir com o SDK. Se você quiser nomear a função global como outra coisa, altere o nome `alloy` da seguinte maneira:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js" async></script>
```

Neste exemplo, a função global é renomeada como `mycustomname`, em vez de `alloy`.

>[!IMPORTANT]
>
>Para evitar possíveis problemas, use um nome que contenha pelo menos um caractere que não seja um dígito e que não entre em conflito com o nome de uma propriedade já encontrada em `window`.

Esse código base, além de criar uma função global, também carrega um código adicional contido em um arquivo externo \(`alloy.js`\) hospedado em um servidor. Por padrão, esse código é carregado de forma assíncrona para permitir que sua página da Web tenha o maior desempenho possível. Essa é a implementação recomendada.

### Suporte ao Internet Explorer {#support-internet-explore}

Esse SDK usa promessas, que são um método de comunicar a conclusão de tarefas assíncronas. A implementação [Promessa](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) usada pelo SDK é nativamente compatível com todos os navegadores de destino, exceto [!DNL Internet Explorer]. Para usar o SDK em [!DNL Internet Explorer], você deve ter `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar se você já tem `window.Promise` polyfill:

1. Abra o site em [!DNL Internet Explorer].
1. Abra o console de depuração do navegador.
1. Digite `window.Promise` no console e pressione Enter.

Se algo diferente de `undefined` for exibido, você provavelmente já terá preenchido `window.Promise` em polyfill. Outra maneira de determinar se `window.Promise` está em polyfill é carregando seu site após ter concluído as instruções de instalação acima. Se o SDK gerar um erro mencionando algo sobre uma promessa, você provavelmente não terá preenchido `window.Promise` em polyfill.

Caso tenha determinado que você deve preencher o `window.Promise`, inclua a seguinte tag de script acima do código base fornecido anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Essa tag carrega um script que garante que `window.Promise` seja uma implementação Promessa válida.

>[!NOTE]
>
>Se optar por carregar uma implementação de Promessa diferente, certifique-se de que ela seja compatível com `Promise.prototype.finally`.

### Carregamento sincronizado do arquivo JavaScript {#loading-javascript-synchronously}

Conforme explicado na seção [Adicionar o código](#adding-the-code), o código base que você copiou e colou no HTML do site carrega um arquivo externo. O arquivo externo contém a funcionalidade principal do SDK. Qualquer comando que você tente executar enquanto esse arquivo é carregado está na fila e é processado depois que o arquivo é carregado. Carregar o arquivo de forma assíncrona é o método de instalação mais eficiente.

Em determinadas circunstâncias, no entanto, você pode querer carregar o arquivo de forma síncrona \(mais detalhes sobre essas circunstâncias serão documentados posteriormente\). Isso impede que o restante do documento HTML seja analisado e renderizado pelo navegador até que o arquivo externo seja carregado e executado. Normalmente, esse atraso adicional antes de exibir o conteúdo principal para os usuários é desencorajado, mas pode fazer sentido dependendo das circunstâncias.

Para carregar o arquivo de forma síncrona, em vez de assíncrona, remova o atributo `async` da segunda tag `script` conforme mostrado abaixo:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js"></script>
```

## Opção 3: Uso do pacote NPM

O SDK da Web da Adobe Experience Platform também está disponível como um pacote NPM. [](https://www.npmjs.com) NPMé o gerenciador de pacotes do JavaScript. A instalação do pacote NPM permite ter controle do processo de build do JavaScript do SDK da Web da Adobe Experience Platform. O pacote NPM expõe módulos EcmaScript versão 5 ou módulos EcmaScript versão 2015 (ES6) destinados a serem executados no navegador.

```bash
npm install @adobe/alloy
```

O pacote NPM do SDK da Web da Adobe Experience Platform expõe uma função `createInstance` . Essa função é usada para criar uma instância. A opção name passada para a função controla o prefixo usado no registro. Abaixo estão exemplos de uso do pacote .

### Uso do pacote como um módulo ECMAScript 2015 (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>O pacote NPM depende de módulos CommonJS; portanto, ao usar um pacote, verifique se o pacote suporta módulos CommonJS. Alguns pacotes, como [Rollup](https://rollupjs.org), exigem um [plug-in](https://www.npmjs.com/package/@rollup/plugin-commonjs) que fornece suporte a CommonJS.

### Uso do pacote como um módulo ECMAScript 5

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Suporte ao Internet Explorer

O Adobe Experience Platform SDK usa promessas, que são um método de comunicar a conclusão de tarefas assíncronas. A implementação [Promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) usada pelo SDK é nativamente compatível com todos os navegadores de destino, exceto [!DNL Internet Explorer]. Para usar o SDK em [!DNL Internet Explorer], você deve ter `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Uma biblioteca que você poderia usar para cumprir a promessa de polyfill é a promessa de polyfill. Consulte a [documentação de promessa-polyfill](https://www.npmjs.com/package/promise-polyfill) para obter mais informações sobre como instalar com o NPM.

>[!NOTE]
>
>Se optar por carregar uma implementação de Promessa diferente, certifique-se de que ela seja compatível com `Promise.prototype.finally`.
