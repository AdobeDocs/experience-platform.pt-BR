---
title: Instalação do Adobe Experience Platform Web SDK
seo-title: Adobe Experience Platform Web SDK instalando o SDK
description: Saiba como instalar o SDK da Web do Experience Platform
seo-description: Saiba como instalar o SDK da Web do Experience Platform
translation-type: tm+mt
source-git-commit: 075d71353877045e12985b3914aaeeb478ed46d6
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Instalação do SDK {#installing-the-sdk}

A maneira preferida de usar o Adobe Experience Platform Web SDK é através do [Launch](http://launch.adobe.com/). Procure pelo `AEP Web SDK` no catálogo de extensões, instale e configure a extensão.

O SDK da Web AEP também está disponível em um CDN para você usar. Você pode fazer referência a esse arquivo ou baixá-lo e hospedá-lo em sua própria infraestrutura. Ele está disponível em uma versão minified e não-minified. A versão não minified é útil para fins de depuração.

Estrutura do URL: https://cdn1.adoberesources.net/alloy/[VERSÃO]/alloy.min.js OU liga.js para a versão não minified.

Por exemplo:

* Miniado: [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js)
* Não minified: [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js)

## Adicionar o código {#adding-the-code}

A primeira etapa na implementação do Adobe Experience Platform [!DNL Web SDK] é copiar e colar o seguinte &quot;código base&quot; o mais alto possível na `<head>` tag do seu HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

O código base cria uma função global chamada `alloy`. Use essa função para interagir com o SDK. Se desejar nomear a função global como outra coisa, você pode alterar o `alloy` nome da seguinte maneira:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Neste exemplo, a função global é renomeada `mycustomname`, em vez de `alloy`.

>[!IMPORTANT]
>
>Para evitar possíveis problemas, use um nome que contenha pelo menos um caractere que não seja um dígito e que não entre em conflito com o nome de uma propriedade já encontrada em `window`.

Esse código base, além de criar uma função global, também carrega um código adicional contido em um arquivo externo \(`alloy.js`\) hospedado em um servidor. Por padrão, esse código é carregado de forma assíncrona para permitir que sua página da Web seja o mais eficiente possível. Esta é a implementação recomendada.

## Suporte ao Internet Explorer {#support-internet-explore}

Esse SDK utiliza promessas, que é um método de comunicar a conclusão de tarefas assíncronas. A implementação [Promise](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) usada pelo SDK é nativamente compatível com todos os navegadores de públicos alvos, exceto [!DNL Internet Explorer]. Para usar o SDK em [!DNL Internet Explorer], é necessário ter o `window.Promise` polifill [](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar se você já tem `window.Promise` polifill:

1. Abra seu site em [!DNL Internet Explorer].
1. Abra o console de depuração do navegador.
1. Digite `window.Promise` no console e pressione Enter.

Se algo diferente de `undefined` aparecer, você provavelmente já está polipreenchido `window.Promise`. Outra maneira de determinar se `window.Promise` está em polim é carregando seu site depois de concluir as instruções de instalação acima. Se o SDK gerar um erro ao mencionar algo sobre uma promessa, você provavelmente não terá preenchido `window.Promise`.

Se você tiver determinado que precisa preencher politicamente `window.Promise`, inclua a seguinte tag de script acima do código base fornecido anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Isso carrega um script que garante que `window.Promise` seja uma implementação Promise válida.

>[!NOTE]
>
>Se você optar por carregar uma implementação Promise diferente, verifique se ela suporta `Promise.prototype.finally`.

## Carregamento sincronizado do arquivo JavaScript {#loading-javascript-synchronously}

Conforme explicado na seção [Adicionando o código](#adding-the-code), o código base que você copiou e colou no HTML de seu site carrega um arquivo externo com código adicional. Esse código adicional contém a funcionalidade principal do SDK. Qualquer comando que você tentar executar enquanto este arquivo estiver sendo carregado será colocado na fila e processado depois que o arquivo for carregado. Este é o método de instalação mais eficiente.

Em determinadas circunstâncias, no entanto, talvez você queira carregar o arquivo sincronicamente \(mais detalhes sobre essas circunstâncias serão documentados posteriormente\). Isso impede que o restante do documento HTML seja analisado e renderizado pelo navegador até que o arquivo externo seja carregado e executado. Esse atraso adicional antes da exibição do conteúdo primário para os usuários geralmente é desencorajado, mas pode fazer sentido dependendo das circunstâncias.

Para carregar o arquivo de forma síncrona em vez de assíncrona, remova o `async` atributo da segunda `script` tag, como mostrado abaixo:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js"></script>
```
