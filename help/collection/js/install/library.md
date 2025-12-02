---
title: Instale o Web SDK usando a biblioteca JavaScript
description: Faça referência à biblioteca do Web SDK usando um arquivo CDN independente.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Instale o Web SDK usando a biblioteca JavaScript

Uma alternativa para instalar o Web SDK sem [usar a extensão de tag](/help/tags/extensions/client/web-sdk/overview.md) é fazer referência à biblioteca de JavaScript hospedada em um CDN. Você pode fazer referência à biblioteca diretamente ou baixá-la e hospedá-la em sua própria infraestrutura. Ele está disponível em formatos minificados e completos.

A biblioteca do Web SDK está disponível usando a seguinte estrutura de URL:

* **Minificado**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Cheio**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Consulte as [notas de versão](../release-notes.md) para obter a versão mais recente a ser incluída na URL. Por exemplo, a URL para a versão completa da versão 2.19.1 é `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Adição do código

Adicione o seguinte bloco de código o mais alto possível na tag `<head>` da sua HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Esse código cria de forma assíncrona um objeto `alloy` que permite chamar qualquer comando do Web SDK. Se quiser carregar o Web SDK de forma síncrona, você pode remover o atributo `async` na última linha do bloco de código. A remoção do atributo `async` impede que o restante do documento do HTML seja analisado e renderizado pelo navegador até que a biblioteca seja carregada e executada. Normalmente, esse atraso adicional antes de exibir o conteúdo principal aos usuários não é recomendado, mas pode fazer sentido, dependendo das necessidades da empresa.
