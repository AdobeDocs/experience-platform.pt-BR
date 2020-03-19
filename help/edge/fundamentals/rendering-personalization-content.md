---
title: Renderização de conteúdo personalizado
seo-title: Adobe Experience Platform Web SDK Renderização de conteúdo personalizado
description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK
seo-description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Renderizando conteúdo personalizado

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

O SDK renderiza automaticamente o conteúdo personalizado quando você envia um evento para o servidor e define `viewStart` como uma opção `true` no evento.

```javascript
alloy("event", {
  "viewStart": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

A renderização de conteúdo personalizado é assíncrona, portanto, não deve haver nenhuma suposição sobre quando um determinado conteúdo faz parte da página.

## Gerenciamento de oscilação

Ao tentar renderizar o conteúdo de personalização, o SDK deve garantir que não haja oscilação. O Flicker, também chamado de FOOC (Flash of Original Content), é quando um conteúdo original é brevemente exibido antes que a alternativa apareça durante testes ou personalização. O SDK tenta aplicar estilos CSS a elementos da página para garantir que esses elementos fiquem ocultos até que o conteúdo de personalização seja renderizado com êxito.

A funcionalidade de gerenciamento de oscilação tem algumas fases:

1. Pré-ocultar
1. Pré-processamento
1. Renderização

### Pré-ocultar

Durante a fase de pré-ocultação, o SDK usa a opção de `prehidingStyle` configuração para criar uma tag de estilo HTML e anexá-la ao DOM para garantir que partes grandes da página estejam ocultas. Se não tiver certeza de quais partes da página serão personalizadas, é recomendável definir `prehidingStyle` como `body { opacity: 0 !important }`. Isso garante que a página inteira esteja oculta. No entanto, isso tem a desvantagem de levar a um desempenho pior de renderização de página relatado por ferramentas como Lighthouse, Testes de página da Web etc. Para ter o melhor desempenho de renderização de página, é recomendável definir `prehidingStyle` para uma lista de elementos de contêiner que contêm as partes da página que serão personalizadas.

Supondo que você tenha uma página HTML como a abaixo e saiba que somente os elementos `bar` e `bazz` contêineres serão personalizados:

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

Então, `prehidingStyle` deveria ser definido como algo como `#bar, #bazz { opacity: 0 !important }`.

### Pré-processamento

A fase de pré-processamento começa assim que o SDK recebe o conteúdo personalizado do servidor. Durante essa fase, a resposta é pré-processada, garantindo que os elementos que precisam conter conteúdo personalizado estejam ocultos. Depois que esses elementos estiverem ocultos, a tag de estilo HTML que foi criada com base na opção de `prehidingStyle` configuração será removida e o corpo HTML ou os elementos de contêiner ocultos serão exibidos.

### Renderização

Depois que todo o conteúdo de personalização for renderizado com êxito, ou se houver algum erro, todos os elementos anteriormente ocultos serão mostrados para garantir que não haja elementos ocultos na página que foram ocultos pelo SDK.

## Gerenciar oscilação quando o SDK é carregado de forma assíncrona

A recomendação é sempre carregar o SDK de forma assíncrona para obter o melhor desempenho de renderização da página. No entanto, isso tem algumas implicações na renderização de conteúdo personalizado. Quando o SDK é carregado de forma assíncrona, é necessário usar o snippet de pré-ocultação. O trecho de pré-ocultação deve ser adicionado antes do SDK na página HTML. Este é um exemplo de trecho que oculta o corpo inteiro:

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

Para garantir que o corpo HTML ou os elementos de contêiner não estejam ocultos por um longo período de tempo, o trecho de pré-ocultação usa um timer que, por padrão, remove o trecho após `3000` milissegundos. Os `3000` milissegundos são o tempo máximo de espera. Se a resposta do servidor tiver sido recebida e processada antes, a tag de estilo HTML pré-ocultada será removida assim que possível.
