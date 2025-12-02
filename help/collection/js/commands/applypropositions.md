---
title: applyPropositions
description: Renderize novamente as apresentações que já foram renderizadas com sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# `applyPropositions`

O comando `applyPropositions` permite renderizar novamente apresentações que já foram renderizadas usando o comando [`sendEvent`](sendevent/overview.md). Esse comando é útil ao trabalhar com aplicativos de página única em que partes da página são renderizadas novamente, substituindo potencialmente qualquer personalização já aplicada à página.

Esse comando oferece suporte aos seguintes campos:

* **Propositions**: uma matriz de objetos de proposta que você deseja renderizar novamente.
* **Nome da exibição**: o nome da exibição a ser renderizada. As notificações de exibição para essas decisões são armazenadas em cache e podem ser incluídas em um comando `sendEvent` subsequente usando a opção `personalization.includeRenderedPropositions`.
* **Dados do Meta**: um objeto que determina como as ofertas do HTML podem ser aplicadas. Ele contém as seguintes propriedades:
   * Escopo
   * Seletor
   * Tipo de ação

Execute o comando `applyPropositions` ao chamar a instância configurada do Web SDK. O objeto que contém opções de configuração é compatível com os seguintes campos:

* **`propositions`**: uma matriz de objetos de proposta que você deseja renderizar novamente. Normalmente, esse objeto não é usado, pois o campo `propositionScopes` geralmente determina quais escopos ou superfícies você deseja renderizar novamente.
* **`metadata`**: determina como as ofertas do HTML são aplicadas. É um mapa em que a chave é um escopo ou uma superfície, e o valor é um objeto que contém as chaves `selector` e `actionType`.
   * `selector`: uma cadeia de caracteres que contém um seletor de CSS de onde aplicar a HTML.
   * `actionType`: A ação a ser executada com a HTML. Os valores válidos incluem `setHtml`, `replaceHtml` e `appendHtml`.
* **`viewName`**: O nome da exibição a ser renderizada em um aplicativo de página única. As notificações de exibição para essas decisões são armazenadas em cache e podem ser incluídas em um comando `sendEvent` subsequente usando `personalization.includeRenderedPropositions`.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## Aplicar apresentações usando a extensão de tag do Web SDK

A extensão de tag do Web SDK equivalente a este comando é a ação [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md).
