---
title: Gerenciar cintilação para experiências personalizadas usando o SDK da Web da Adobe Experience Platform
description: Saiba como usar o SDK da Web da Adobe Experience Platform para gerenciar a cintilação nas experiências do usuário.
keywords: target; cintilação; pré-ocultaçãoStyle; assíncrono; assíncrono;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Gerenciar cintilação

Ao tentar renderizar o conteúdo de personalização, o SDK deve garantir que não haja cintilação. A cintilação, também chamada de FOOC (Flash de Conteúdo Original), é quando um conteúdo original é exibido brevemente antes que a alternativa seja exibida durante o teste/personalização. O SDK tenta aplicar estilos de CSS a elementos da página para garantir que esses elementos estejam ocultos até que o conteúdo de personalização seja renderizado com êxito.

A funcionalidade de gerenciamento de cintilação tem algumas fases:

1. Pré-ocultar
1. Pré-processamento
1. Renderização

## Pré-ocultar

Durante a fase de pré-ocultação, o SDK usa o `prehidingStyle` opção de configuração para criar uma tag de estilo HTML e anexá-la ao DOM para garantir que grandes partes da página estejam ocultas. Se não tiver certeza de quais partes da página serão personalizadas, é recomendável definir `prehidingStyle` para `body { opacity: 0 !important }`. Isso garante que toda a página fique oculta. No entanto, isso tem o lado negativo de levar a um desempenho de renderização de página pior relatado por ferramentas como Lighthouse, Web Page Tests, etc. Para ter o melhor desempenho de renderização da página, é recomendável definir `prehidingStyle` para obter uma lista de elementos de contêiner que contêm as partes da página que serão personalizadas.

Supondo que você tenha uma HTML page como a abaixo e saiba que somente `bar` e `bazz` os elementos do contêiner serão personalizados:

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

Em seguida, `prehidingStyle` deve ser definido como algo como `#bar, #bazz { opacity: 0 !important }`.

## Pré-processamento

A fase de pré-processamento é iniciada assim que o SDK recebe o conteúdo personalizado do servidor. Durante essa fase, a resposta é pré-processada, garantindo que os elementos que precisam conter conteúdo personalizado estejam ocultos. Depois que esses elementos são ocultos, a tag de estilo de HTML é criada com base na `prehidingStyle` a opção de configuração é removida e os elementos HTML body ou the hidden container são mostrados.

## Renderização

Depois que todo o conteúdo de personalização tiver sido renderizado com êxito, ou se houver algum erro, todos os elementos ocultos anteriormente serão mostrados para garantir que não haja elementos ocultos na página que tenham sido ocultos pelo SDK.

## Gerenciamento de cintilação quando o SDK é carregado de forma assíncrona

A recomendação é sempre carregar o SDK de forma assíncrona para obter o melhor desempenho de renderização da página. No entanto, isso tem algumas implicações para a renderização do conteúdo personalizado. Quando o SDK é carregado de forma assíncrona, é necessário usar o trecho pré-ocultação. O trecho pré-ocultação deve ser adicionado antes do SDK na página do HTML. Este é um trecho de exemplo que oculta o corpo inteiro:

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

Para garantir que o corpo do HTML ou os elementos do contêiner não estejam ocultos por um longo período de tempo, o trecho pré-ocultação usa um temporizador que, por padrão, remove o trecho após `3000` milissegundos. O `3000` milissegundos é o tempo máximo de espera. Se a resposta do servidor tiver sido recebida e processada antes, a tag HTML de pré-ocultação será removida assim que possível.
