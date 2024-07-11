---
title: clickCollectionEnabled
description: Saiba como configurar o SDK da Web para determinar se os dados de cliques em links são coletados automaticamente.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

A variável `clickCollectionEnabled` é uma propriedade do tipo booleano que determina se o SDK da Web coleta automaticamente dados de links. Se você não definir essa variável, seu valor padrão será `true` o que significa que os dados de rastreamento de link são coletados automaticamente por padrão. Configurando esta propriedade para `false` O é importante nos casos em que você prefere rastrear os dados do link manualmente.

Quando `clickCollectionEnabled` estiver ativado, os seguintes elementos XDM serão preenchidos automaticamente com dados:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Links internos, links de download e links de saída são rastreados automaticamente por padrão quando esse booleano é ativado. Se quiser ter mais controle sobre o rastreamento automático de links, o Adobe recomenda usar o [`clickCollection`](clickcollection.md) objeto.

## Lógica de rastreamento de link automático

O SDK da Web rastreia todos os cliques em `<a>` e `<area>` elementos HTML se não tiver um `onClick` atributo. Os cliques são capturados com um [capturar](https://www.w3.org/TR/uievents/#capture-phase) clique em ouvinte de eventos anexado ao documento. Quando um link válido é clicado, a seguinte lógica é executada em ordem:

1. Se o link corresponder aos critérios com base nos valores em [`downloadLinkQualifier`](downloadlinkqualifier.md)ou se o link contiver um `download` atributo HTML, `xdm.web.webInteraction.type` está definida como `"download"` (se `clickCollection.downloadLinkEnabled` está ativado).
1. Se o domínio de destino do link for diferente do atual `window.location.hostname`, `xdm.web.webInteraction.type` está definida como `"exit"` (se `clickCollection.exitLinkEnabled` está ativado).
1. Se o link não se qualificar para `"download"` ou `"exit"`, `xdm.web.webInteraction.type` está definida como `"other"`.

Em todos os casos, `xdm.web.webInteraction.name` está definido como o rótulo de texto do link e `xdm.web.webInteraction.URL` está definido para o URL de destino do link. Se você quiser definir o nome do link para o URL também, poderá substituir esse campo XDM usando o `filterClickDetails` retorno de chamada na `clickCollection` objeto.

## Ativar o rastreamento automático de links usando a extensão de tag do SDK da Web {#tag-extension}

Selecione o **[!UICONTROL Ativar a coleta de dados de cliques]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Coleta de dados] e marque a caixa de seleção **[!UICONTROL Ativar a coleta de dados de cliques]**.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Ativar o rastreamento automático de links usando a biblioteca JavaScript do SDK da Web {#library}

Defina o `clickCollectionEnabled` booleano ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `true`. Defina esse valor como `false` se preferir definir `xdm.web.webInteraction.type` e `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
