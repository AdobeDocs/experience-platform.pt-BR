---
title: Renderizar automaticamente propostas de ação DOM
description: Use o Web SDK para renderizar automaticamente propostas de ação DOM qualificadas e lidar com cenários comuns de renderização de SPA.
keywords: personalização;renderDecisions;dom-action;sendEvent;applyPropositions;single page application;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Renderizar propostas de ação do DOM automaticamente

Use esse padrão quando a resposta de personalização incluir itens de proposta com o schema:

**`https://ns.adobe.com/personalization/dom-action`**

Normalmente, esses itens incluem um seletor e um tipo de ação (por exemplo, `setHtml`) que o Web SDK pode aplicar automaticamente quando `renderDecisions` está habilitado.

## &#x200B;1. Gerenciar cintilação (opcional)

Se você precisar evitar a cintilação enquanto o conteúdo personalizado for aplicado, use a abordagem de gerenciamento de cintilação recomendada para sua implementação. Consulte [Gerenciar cintilação](manage-flicker.md) para ver as opções disponíveis.

## &#x200B;2. Pedido e decisão de processamento anotadas para processamento automático

Defina `renderDecisions` como `true` ao chamar o comando `sendEvent`. O padrão da propriedade `renderDecisions` é false quando omitida.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

Opcionalmente, se precisar solicitar disposições específicas, inclua `personalization.decisionScopes`:

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

Consulte o objeto [`personalization`](/help/collection/js/commands/sendevent/personalization.md) no comando [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) para obter mais informações.

## &#x200B;3. Exibir eventos

Se você definir `renderDecisions` como `true` e definir `personalization.sendDisplayEvent` como `true` ou omiti-lo, o Web SDK enviará eventos de exibição imediatamente após a personalização ser renderizada.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

Consulte [Gerenciar eventos de exibição](display-events.md) para obter opções alternativas que atendam às suas necessidades de implementação, como ao usar os [Eventos de página superior e inferior](top-bottom-page-events.md).

## &#x200B;4. Alterações de exibição e renderização de SPA

Para aplicativos de página única, inclua um `viewName` sobre eventos que alteram a visualização.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

Se o SPA renderizar novamente a interface do usuário para a mesma exibição sem uma nova busca de decisão, você poderá reaplicar as propostas retornadas anteriormente:

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

Consulte [`applyPropositions`](/help/collection/js/commands/applypropositions.md) para obter mais informações.

>[!NOTE]
>
>O comando `applyPropositions` não envia eventos de exibição automaticamente. Se você precisar gravar &quot;exibição&quot; para cenários de nova renderização, consulte [Gerenciar eventos de exibição](display-events.md).
