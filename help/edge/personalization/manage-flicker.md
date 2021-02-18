---
title: Gerenciar o Flicker para experiências personalizadas usando o Adobe Experience Platform Web SDK
description: Saiba como usar o Adobe Experience Platform Web SDK para gerenciar oscilações nas experiências do usuário.
keywords: público alvo;flicker;prehideStyle;assíncrono;assíncrono;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Gerenciar oscilação

Ao tentar renderizar o conteúdo de personalização, o SDK deve garantir que não haja oscilação. Flicker, também chamado de FOOC (Flash do conteúdo original), é quando um conteúdo original é exibido brevemente antes que a alternativa apareça durante o teste/personalização. O SDK tenta aplicar estilos CSS a elementos da página para garantir que esses elementos fiquem ocultos até que o conteúdo de personalização seja renderizado com êxito.

A funcionalidade de gerenciamento de oscilação tem algumas fases:

1. Pré-ocultar
1. Pré-processamento
1. Renderização

## Pré-ocultar

Durante a fase de pré-ocultação, o SDK usa a opção de configuração `prehidingStyle` para criar uma tag de estilo HTML e anexá-la ao DOM para garantir que partes grandes da página estejam ocultas. Se não tiver certeza de quais partes da página serão personalizadas, é recomendável definir `prehidingStyle` como `body { opacity: 0 !important }`. Isso garante que a página inteira esteja oculta. No entanto, isso tem o lado negativo de levar a um desempenho pior de renderização de página relatado por ferramentas como Lighthouse, Testes de página da Web etc. Para ter o melhor desempenho de renderização de página, é recomendável definir `prehidingStyle` como uma lista de elementos de container que contêm as partes da página que serão personalizadas.

Supondo que você tenha uma página HTML como a abaixo e que somente os elementos de container `bar` e `bazz` serão sempre personalizados:

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

Em seguida, `prehidingStyle` deve ser definido para algo como `#bar, #bazz { opacity: 0 !important }`.

## Pré-processamento

A fase de pré-processamento é iniciada assim que o SDK recebe o conteúdo personalizado do servidor. Durante essa fase, a resposta é pré-processada, garantindo que os elementos que precisam conter conteúdo personalizado estejam ocultos. Depois que esses elementos estiverem ocultos, a tag de estilo HTML que foi criada com base na opção de configuração `prehidingStyle` será removida e o corpo HTML ou os elementos de container ocultos serão exibidos.

## Renderização

Depois que todo o conteúdo de personalização for renderizado com êxito, ou se houver algum erro, todos os elementos anteriormente ocultos serão mostrados para garantir que não haja elementos ocultos na página que foram ocultos pelo SDK.

## Gerenciar oscilação quando o SDK é carregado de forma assíncrona

A recomendação é sempre carregar o SDK de forma assíncrona para obter o melhor desempenho de renderização da página. No entanto, isso tem algumas implicações na renderização de conteúdo personalizado. Quando o SDK é carregado de forma assíncrona, é necessário usar o trecho de pré-ocultação. O trecho de pré-ocultação deve ser adicionado antes do SDK na página HTML. Este é um exemplo de trecho que oculta o corpo inteiro:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Para garantir que o corpo HTML ou os elementos do container não fiquem ocultos por um longo período de tempo, o trecho de pré-ocultação usa um timer que, por padrão, remove o trecho após `3000` milissegundos. Os milissegundos `3000` são o tempo máximo de espera. Se a resposta do servidor tiver sido recebida e processada antes, a tag de estilo HTML pré-ocultada será removida assim que possível.
