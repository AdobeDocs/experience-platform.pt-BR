---
title: Gerenciar cintilação para experiências personalizadas usando o SDK da Web da Adobe Experience Platform
description: Saiba como usar o Adobe Experience Platform Web SDK para gerenciar a cintilação nas experiências do usuário.
keywords: destino;cintilação;estiloPré-ocultação;assíncrono;assíncrono;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Gerenciar cintilação

Ao tentar renderizar o conteúdo de personalização, o SDK precisa garantir que não haja cintilação. A cintilação, também chamada de FOOC (Flash do conteúdo original), ocorre quando um conteúdo original é exibido brevemente antes de a alternativa aparecer durante o teste/personalização. O SDK tenta aplicar estilos CSS a elementos da página, a fim de garantir que esses elementos estejam ocultos até que o conteúdo de personalização seja renderizado com êxito.

A maneira como você gerencia a cintilação depende de você implantar o SDK da Web de forma síncrona ou assíncrona. Verifique a `<head>` tag onde você implanta `alloy.js` ou o carregador de tags. A presença da `async` atributo no `<script>` determina se o SDK da Web é carregado de forma assíncrona.

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## Gerenciar cintilação para implantações síncronas

O gerenciamento de cintilação síncrona é dividido em três fases:

1. Pré-ocultação
1. Pré-processando
1. Renderização

Durante a **fase de pré-ocultação**, o SDK usa o [`prehidingStyle`](../commands/configure/prehidingstyle.md) propriedade de configuração para criar uma tag de estilo HTML e anexá-la ao DOM para garantir que as seções desejadas da página estejam ocultas. Se não tiver certeza de quais partes da página serão personalizadas, é recomendável definir `prehidingStyle` para `body { opacity: 0 !important }`. Isso garante que a página inteira fique oculta. No entanto, isso tem o lado negativo de levar ao pior desempenho de renderização da página relatado por ferramentas como Lighthouse, Testes de página da Web etc. Para ter o melhor desempenho de renderização da página, é recomendável definir `prehidingStyle` para obter uma lista de elementos de contêiner que contêm as partes da página que serão personalizadas.

Supondo que você tenha uma página de HTML como a abaixo e saiba que somente `bar` e `bazz` os elementos do contêiner serão sempre personalizados:

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

Em seguida, o `prehidingStyle` deve ser definido como algo como `#bar, #bazz { opacity: 0 !important }`.

Depois que o SDK receber conteúdo personalizado do servidor, a variável **fase de pré-processamento** O é iniciado. Durante essa fase, a resposta é pré-processada, garantindo que os elementos que precisam conter conteúdo personalizado estejam ocultos. Depois que esses elementos estiverem ocultos, a tag de estilo HTML que foi criada com base no `prehidingStyle` a opção de configuração é removida e o corpo da HTML ou os elementos de contêiner ocultos são mostrados.

Depois que todo o conteúdo de personalização for renderizado com sucesso ou se houver algum erro, a variável **fase de processamento** O é iniciado. Todos os elementos ocultos anteriormente são mostrados para garantir que não haja elementos ocultos na página ocultos pelo SDK.

## Gerenciar cintilação para implantações assíncronas

A recomendação é sempre carregar o SDK de forma assíncrona para obter o melhor desempenho de renderização da página. No entanto, isso tem algumas implicações para a renderização de conteúdo personalizado. Quando o SDK é carregado de forma assíncrona, é necessário usar o trecho pré-ocultação. O trecho pré-ocultação deve ser adicionado antes do SDK na página do HTML. Este é um exemplo de trecho que oculta o corpo inteiro:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Para garantir que o corpo da HTML ou os elementos do contêiner não fiquem ocultos por um longo período, o trecho pré-ocultação usa um cronômetro que, por padrão, remove o trecho após `3000` milissegundos. A variável `3000` milissegundos é o tempo máximo de espera. Se a resposta do servidor tiver sido recebida e processada antes, a tag de estilo HTML pré-ocultação será removida o mais rápido possível.
