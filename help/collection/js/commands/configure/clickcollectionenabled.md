---
title: clickCollectionEnabled
description: Saiba como configurar o Web SDK para determinar se os dados de cliques em links são coletados automaticamente.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# `clickCollectionEnabled`

A propriedade `clickCollectionEnabled` é um booliano que determina se o Web SDK coleta dados de link automaticamente. Se você não definir essa variável, seu valor padrão será `true`, o que significa que os dados de rastreamento de link serão coletados automaticamente por padrão. Configurar essa propriedade como `false` é importante nos casos em que você prefere rastrear os dados do link manualmente.

Quando `clickCollectionEnabled` está habilitado, os seguintes elementos XDM são preenchidos automaticamente com dados:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Links internos, links de download e links de saída são rastreados automaticamente por padrão quando esse booleano é ativado. Se você quiser ter mais controle sobre o rastreamento automático de links, a Adobe recomenda usar o objeto [`clickCollection`](clickcollection.md).

## Lógica de rastreamento de link automático

O Web SDK rastreia todos os cliques nos elementos HTML `<a>` e `<area>` se não tiver um atributo `onClick`. Os cliques são capturados com um ouvinte de eventos de clique [capture](https://www.w3.org/TR/uievents/#capture-phase) anexado ao documento. Quando um link válido é clicado, a seguinte lógica é executada em ordem:

1. Se o link corresponder aos critérios com base nos valores em [`downloadLinkQualifier`](downloadlinkqualifier.md), ou se o link contiver um atributo do HTML `download`, `xdm.web.webInteraction.type` será definido como `"download"` (se `clickCollection.downloadLinkEnabled` estiver habilitado).
1. Se o domínio de destino do link for diferente do atual `window.location.hostname`, `xdm.web.webInteraction.type` está definido como `"exit"` (se `clickCollection.exitLinkEnabled` estiver habilitado).
1. Se o link não se qualificar para `"download"` ou `"exit"`, `xdm.web.webInteraction.type` está definido como `"other"`.

Em todos os casos, `xdm.web.webInteraction.name` está definido como o rótulo de texto do link e `xdm.web.webInteraction.URL` está definido como a URL de destino do link. Se você quiser definir o nome do link para a URL também, poderá substituir esse campo XDM usando o retorno de chamada `filterClickDetails` no objeto `clickCollection`.

Defina o booleano `clickCollectionEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o Web SDK, o padrão será `true`. Defina este valor como `false` se preferir definir `xdm.web.webInteraction.type` e `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```

## Suporte para elementos [!DNL Shadow DOM] abertos

O Web SDK oferece suporte ao rastreamento automático de cliques para links dentro de **elementos DOM** de sombra aberta.

Muitos sites modernos usam [Componentes Web](https://developer.mozilla.org/en-US/docs/Web/Web_Components) para criar elementos de interface do usuário reutilizáveis e encapsulados. Esses componentes geralmente usam uma tecnologia chamada [**DOM de sombra**](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) para manter sua estrutura interna e estilos separados do restante da página.

Há dois tipos de DOM de sombra:

* **Abrir DOM Sombra:** A estrutura interna é acessível ao JavaScript em execução na página. Outros scripts podem interagir com o componente ou inspecioná-lo.
* **DOM de Sombra Fechada:** A estrutura interna está oculta do JavaScript fora do componente, tornando-a inacessível para rastreamento ou manipulação.

O Web SDK rastreia automaticamente os cliques nos elementos `<a>` e `<area>` dentro dos **DOMs de Sombra Aberta**, da mesma forma que faz para os links no documento principal. Esse rastreamento garante que os cliques em links dentro de componentes da Web que usam o [!DNL Shadow DOM] aberto sejam incluídos nos dados de análise. Os cliques dentro de **DOMs de sombra fechados** não são rastreados, pois sua estrutura interna está oculta do código JavaScript que opera fora do componente.

## Ativar ou desativar a coleção de cliques para a extensão de tag do Web SDK

Consulte [Configurações da coleta de dados](/help/tags/extensions/client/web-sdk/configure/data-collection.md) na documentação da extensão do Web SDK para saber como executar essas ações usando tags.
