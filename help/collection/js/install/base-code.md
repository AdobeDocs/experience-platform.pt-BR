---
title: Código base
description: Enfileire comandos (inicialização) enquanto a biblioteca de coleta de dados é carregada de forma assíncrona.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Código base

O código base permite a inicialização enfileirando comandos enquanto o Adobe Experience Platform Web SDK é carregado de forma assíncrona. Depois que o código base for executado, você poderá chamar imediatamente qualquer comando como [`configure`](../commands/configure/overview.md) ou [`sendEvent`](../commands/sendevent/overview.md) sem se preocupar com as condições de corrida ou o tempo de carregamento da biblioteca quando ela terminar. Quando o Web SDK termina o carregamento, os comandos em fila são executados em uma ordem primeiro a entrar, primeiro a sair (na mesma ordem em que foram enfileirados).

Os comandos retornam Promessas, mesmo quando enfileirados. Se um comando estiver na fila, a Promessa será resolvida ou rejeitada depois que o comando for executado quando o Web SDK terminar de ser carregado. Se o Web SDK nunca terminar de carregar (por exemplo, a biblioteca falha ao carregar), as Promessas em fila permanecerão pendentes.

## Adicionar o código base

Coloque o código base o mais alto possível na tag `<head>`, antes de qualquer script que possa chamar o Web SDK.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Depois de adicionar o código base, carregue o Web SDK usando o método escolhido ([carregador da biblioteca JavaScript](library.md) ou [código de inserção de marcas](/help/tags/extensions/client/web-sdk/getting-started.md)). Para implementações baseadas em tags, o código base é compatível com a extensão de tag 2.34.0 e posterior do Web SDK.

Este código base **não** é necessário nos seguintes cenários:

* Se você carregar a biblioteca do JavaScript de forma síncrona. O carregamento síncrono bloqueia a análise enquanto a biblioteca é buscada e executada.
* Se estiver usando a extensão de tag, todas as chamadas para o Web SDK serão feitas nas regras de tag ou ações. Você só precisará incluir o código base se sua implementação fizer referência à Web SDK fora da biblioteca de tags. A maioria das implementações de tags normalmente não chama a Web SDK fora da biblioteca de tags. Portanto, a maioria das implementações de tags não requer o código base.

## Exemplos

Consulte os comentários neste exemplo de código para entender o tempo de enfileiramento e resolução de comandos. Este exemplo se aplica à biblioteca de JavaScript e à extensão de tag:

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## Renomear instância do SDK

Você pode renomear a função global chamada modificando a última linha do código base. Alterar:

```js
(window,["alloy"]);
```

Para:

```js
(window,["ingot"]);
```

Esta alteração permite que você chame comandos usando `ingot` em vez de `alloy`:

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## Várias instâncias do SDK

Opcionalmente, é possível usar o código base para configurar mais de uma instância do SDK em uma página. Consulte [Usar várias instâncias do Web SDK](../../use-cases/multiple-instances.md) para obter mais informações.
