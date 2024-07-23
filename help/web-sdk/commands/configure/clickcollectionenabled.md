---
title: clickCollectionEnabled
description: Saiba como configurar o SDK da Web para determinar se os dados de cliques em links são coletados automaticamente.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# `clickCollectionEnabled`

A propriedade `clickCollectionEnabled` é um booliano que determina se o SDK da Web coleta automaticamente dados de link. Se você não definir essa variável, seu valor padrão será `true`, o que significa que os dados de rastreamento de link serão coletados automaticamente por padrão. Configurar essa propriedade como `false` é importante nos casos em que você prefere rastrear os dados do link manualmente.

Quando `clickCollectionEnabled` está habilitado, os seguintes elementos XDM são preenchidos automaticamente com dados:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Links internos, links de download e links de saída são rastreados automaticamente por padrão quando esse booleano é ativado. Se você quiser ter mais controle sobre o rastreamento automático de links, o Adobe recomenda usar o objeto [`clickCollection`](clickcollection.md).

## Lógica de rastreamento de link automático

O SDK da Web rastreia todos os cliques nos elementos HTML `<a>` e `<area>` se não tiver um atributo `onClick`. Os cliques são capturados com um ouvinte de eventos de clique [capture](https://www.w3.org/TR/uievents/#capture-phase) anexado ao documento. Quando um link válido é clicado, a seguinte lógica é executada em ordem:

1. Se o link corresponder aos critérios com base nos valores em [`downloadLinkQualifier`](downloadlinkqualifier.md), ou se o link contiver um atributo HTML `download`, `xdm.web.webInteraction.type` será definido como `"download"` (se `clickCollection.downloadLinkEnabled` estiver habilitado).
1. Se o domínio de destino do link for diferente do atual `window.location.hostname`, `xdm.web.webInteraction.type` está definido como `"exit"` (se `clickCollection.exitLinkEnabled` estiver habilitado).
1. Se o link não se qualificar para `"download"` ou `"exit"`, `xdm.web.webInteraction.type` está definido como `"other"`.

Em todos os casos, `xdm.web.webInteraction.name` está definido como o rótulo de texto do link e `xdm.web.webInteraction.URL` está definido como a URL de destino do link. Se você quiser definir o nome do link para a URL também, poderá substituir esse campo XDM usando o retorno de chamada `filterClickDetails` no objeto `clickCollection`.

## Ativar o rastreamento automático de links usando a extensão de tag do SDK da Web {#tag-extension}

Essa variável é gerenciada automaticamente pela extensão de tag; não é necessário defini-la explicitamente. Se qualquer um dos itens a seguir for selecionado ao [configurar a extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md), os dados de rastreamento de link aplicáveis serão coletados:

* [!UICONTROL Coletar cliques internos em links]
* [!UICONTROL Coletar cliques em links externos]
* [!UICONTROL Coletar cliques no link de download]

Consulte [`clickCollection`](clickcollection.md) para obter mais informações.

## Ativar o rastreamento automático de links usando a biblioteca JavaScript do SDK da Web {#library}

Defina o booleano `clickCollectionEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `true`. Defina este valor como `false` se preferir definir `xdm.web.webInteraction.type` e `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
