---
title: clickCollectionEnabled
description: Saiba como configurar o SDK da Web para determinar se os dados de cliques em links são coletados automaticamente.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
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

Marque a caixa de seleção **[!UICONTROL Habilitar coleta de dados de cliques]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Coleção de dados] e marque a caixa de seleção **[!UICONTROL Habilitar coleta de dados de cliques]**.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Ativar o rastreamento automático de links usando a biblioteca JavaScript do SDK da Web {#library}

Defina o booleano `clickCollectionEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `true`. Defina este valor como `false` se preferir definir `xdm.web.webInteraction.type` e `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
