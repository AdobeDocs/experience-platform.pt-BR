---
title: Instale o SDK da Web usando a biblioteca do JavaScript
description: Faça referência à biblioteca do SDK da Web usando um arquivo CDN independente.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Instale o SDK da Web usando a biblioteca do JavaScript

Uma alternativa para instalar o SDK da Web sem [usar a extensão de tag](extension.md) é fazer referência à biblioteca de JavaScript hospedada em um CDN. Você pode fazer referência à biblioteca diretamente ou baixá-la e hospedá-la em sua própria infraestrutura. Ele está disponível em formatos minificados e completos.

A biblioteca do SDK da Web está disponível usando a seguinte estrutura de URL:

* **Minificado**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Cheio**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Consulte as [notas de versão](../release-notes.md) para obter a versão mais recente a ser incluída na URL. Por exemplo, a URL para a versão completa da versão 2.19.1 é `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Adição do código

Adicione o seguinte bloco de código o mais alto possível na tag `<head>` do seu HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Esse código cria de forma assíncrona um objeto `alloy` que permite chamar qualquer comando do SDK da Web. Se quiser carregar o SDK da Web de forma síncrona, você pode remover o atributo `async` na última linha do bloco de código. A remoção do atributo `async` impede que o restante do documento HTML seja analisado e renderizado pelo navegador até que a biblioteca seja carregada e executada. Normalmente, esse atraso adicional antes de exibir o conteúdo principal aos usuários não é recomendado, mas pode fazer sentido, dependendo das necessidades da empresa.
