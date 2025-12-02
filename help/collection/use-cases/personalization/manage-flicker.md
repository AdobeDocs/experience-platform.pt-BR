---
title: Gerenciar cintilação para experiências personalizadas usando o Adobe Experience Platform Web SDK
description: Saiba como usar o Adobe Experience Platform Web SDK para gerenciar a cintilação nas experiências do usuário.
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Gerenciar cintilação

Ao tentar renderizar o conteúdo de personalização, o SDK precisa garantir que não haja cintilação. A cintilação, também chamada de FOOC (Flash of Original Content), ocorre quando um conteúdo original é exibido brevemente antes de a alternativa aparecer durante o teste/personalização. O SDK tenta aplicar estilos CSS aos elementos da página para garantir que esses elementos estejam ocultos até que o conteúdo de personalização seja renderizado com sucesso.

A maneira como você gerencia a cintilação depende da implantação do Web SDK de forma síncrona ou assíncrona. Verifique a marca `<head>` onde você implantou o `alloy.js` ou o carregador de marcas. A presença do atributo `async` na marca `<script>` determina se o Web SDK é carregado de forma assíncrona.

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

Durante a **fase de pré-ocultação**, o SDK usa a propriedade de configuração [`prehidingStyle`](../../js/commands/configure/prehidingstyle.md) para criar uma marca de estilo do HTML e anexá-la ao DOM para garantir que as seções desejadas da página estejam ocultas. Se não tiver certeza de quais partes da página serão personalizadas, é recomendável definir `prehidingStyle` como `body { opacity: 0 !important }`. Isso garante que a página inteira fique oculta. No entanto, isso tem o lado negativo de levar ao pior desempenho de renderização da página relatado por ferramentas como Lighthouse, Testes de página da Web etc. Para ter o melhor desempenho de renderização da página, é recomendável definir `prehidingStyle` como uma lista de elementos de contêiner que contenham as partes da página que serão personalizadas.

Supondo que você tenha uma página do HTML como a abaixo e saiba que somente os elementos de contêiner `bar` e `bazz` serão personalizados:

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

Depois que o SDK receber conteúdo personalizado do servidor, a **fase de pré-processamento** será iniciada. Durante essa fase, a resposta é pré-processada, garantindo que os elementos que precisam conter conteúdo personalizado estejam ocultos. Depois que esses elementos estiverem ocultos, a marca de estilo HTML que foi criada com base na opção de configuração `prehidingStyle` será removida e o corpo do HTML ou os elementos de contêiner ocultos serão exibidos.

Depois que todo o conteúdo de personalização for renderizado com êxito, ou se houver algum erro, a **fase de renderização** será iniciada. Todos os elementos ocultos anteriormente são mostrados para garantir que não haja elementos ocultos na página ocultos pela SDK.

## Gerenciar cintilação para implantações assíncronas

A recomendação é sempre carregar o SDK de forma assíncrona para obter o melhor desempenho de renderização da página. No entanto, isso tem algumas implicações para a renderização de conteúdo personalizado. Quando o SDK é carregado de forma assíncrona, é necessário usar o trecho pré-ocultação. O trecho pré-ocultação deve ser adicionado antes da SDK na página do HTML. Este é um exemplo de trecho que oculta o corpo inteiro:

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

Para garantir que o corpo da HTML ou os elementos do contêiner não fiquem ocultos por um longo período de tempo, o trecho pré-ocultação usa um temporizador que, por padrão, remove o trecho após `3000` milissegundos. O tempo máximo de espera de `3000` milissegundos. Se a resposta do servidor tiver sido recebida e processada antes, a tag de estilo do HTML pré-ocultação será removida o mais rápido possível.
