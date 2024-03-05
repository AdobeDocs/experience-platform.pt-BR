---
title: applyPropositions
description: Renderize novamente as apresentações que já foram renderizadas com sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# `applyPropositions`

A variável `applyPropositions` permite renderizar novamente as apresentações que já foram renderizadas usando o [`sendEvent`](sendevent/overview.md) comando. Esse comando é útil ao trabalhar com aplicativos de página única em que partes da página são renderizadas novamente, substituindo potencialmente qualquer personalização já aplicada à página.

Esse comando oferece suporte aos seguintes campos:

* **Apresentações**: uma matriz de objetos de proposta que você deseja renderizar novamente.
* **Exibir nome**: o nome da exibição a ser renderizada. As notificações de exibição para essas decisões são armazenadas em cache e podem ser incluídas em uma `sendEvent` usando o `personalization.includePendingDisplayNotifications` opção.
* **Metadados**: um objeto que determina como as ofertas de HTML podem ser aplicadas. Ele contém as seguintes propriedades:
   * Escopo
   * Seletor
   * Tipo de ação

## Aplicar apresentações usando a extensão de tag do SDK da Web

A aplicação de apresentações é executada como uma ação em uma regra na interface das tags da Coleção de dados da Adobe Experience Platform.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Aplicar apresentações]**.
1. Defina os campos desejados à direita.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Aplicar apresentações usando a biblioteca JavaScript do SDK da Web

Execute o `applyPropositions` ao chamar a instância configurada do SDK da Web. O objeto que contém opções de configuração é compatível com os seguintes campos:

* **`propositions`**: uma matriz de objetos de proposta que você deseja renderizar novamente. Normalmente, esse objeto não é usado, pois `propositionScopes` normalmente determina quais escopos ou superfícies você deseja renderizar novamente.
* **`metadata`**: determina como as ofertas de HTML são aplicadas. É um mapa em que a chave é um escopo ou uma superfície, e o valor é um objeto que contém as chaves `selector` e `actionType`.
   * `selector`: uma cadeia de caracteres que contém um seletor de CSS de onde aplicar o HTML.
   * `actionType`: A ação a ser executada com o HTML. Os valores válidos incluem `setHtml`, `replaceHtml` e `appendHtml`.
* **`viewName`**: o nome da exibição a ser renderizada em um aplicativo de página única. As notificações de exibição para essas decisões são armazenadas em cache e podem ser incluídas em uma `sendEvent` comando usando `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
