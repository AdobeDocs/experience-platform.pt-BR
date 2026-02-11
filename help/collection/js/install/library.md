---
title: Instalar a biblioteca JavaScript do Web SDK
description: Faça referência à biblioteca do Web SDK usando um arquivo CDN independente.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Instalar a biblioteca JavaScript do Web SDK

Se você optar por não usar a [extensão de tag do Web SDK](/help/tags/extensions/client/web-sdk/overview.md), poderá instalar o Web SDK fazendo referência à biblioteca independente do JavaScript hospedada no CDN da Adobe. Você pode fazer referência à biblioteca diretamente ou baixá-la e hospedá-la em sua própria infraestrutura. Ele está disponível em formatos minificados e completos.

A biblioteca do Web SDK está disponível usando a seguinte estrutura de URL:

* **Minificado**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **Cheio**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

Consulte as [notas de versão do Web SDK](../release-notes.md) para obter a versão mais recente a ser incluída na URL. Por exemplo, a URL para a versão completa da versão 2.19.1 é `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Adição do código base e do carregador de biblioteca

O código a ser adicionado consiste em duas seções:

* **Código base**: permite a inicialização enfileirando comandos enquanto o Web SDK é carregado de forma assíncrona. Consulte [Código base](base-code.md) para obter mais informações. A Adobe recomenda usar o código base ao carregar a biblioteca de forma assíncrona para evitar condições de corrida ao chamar comandos do Web SDK durante o carregamento da página.
* **Carregador da biblioteca**: carrega a biblioteca completa do JavaScript.

Adicione o seguinte bloco de código o mais alto possível na tag `<head>`, antes que qualquer script que possa chamar o Web SDK:

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

Se quiser carregar o Web SDK de forma síncrona, você poderá remover o atributo `async` ao carregar a biblioteca. A remoção do atributo `async` bloqueia a análise do HTML enquanto o navegador busca e executa a biblioteca. Normalmente, esse atraso adicional antes de exibir o conteúdo principal aos usuários não é recomendado, mas pode fazer sentido, dependendo das necessidades da empresa.
