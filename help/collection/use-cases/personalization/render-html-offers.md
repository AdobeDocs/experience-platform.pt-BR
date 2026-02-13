---
title: Renderizar ofertas do HTML sem seletores
description: Renderize itens de apresentação do HTML que não incluem seletores fornecendo metadados para applyPropositions e registrando os eventos de exibição.
keywords: personalização;aplicarProposições;metadados;tipoAção;escoposDecisão;exibir eventos;personalization;applyPropositions;metadata;actionType;decisionScope;display events;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Renderizar ofertas do HTML sem seletores

Use esse padrão quando suas propostas incluírem conteúdo HTML, mas você deve fornecer onde aplicá-lo (seletor) e como aplicá-lo (tipo de ação). Você pode fazer isso chamando [`applyPropositions`](/help/collection/js/commands/applypropositions.md) com um objeto `metadata` digitado por escopo. Os valores de `actionType` com suporte são `setHtml`, `replaceHtml` e `appendHtml`.

## &#x200B;1. Gerenciar cintilação (opcional)

Se ocultar o conteúdo durante a renderização, você será responsável por revelá-lo após a conclusão da renderização. Consulte [Gerenciar cintilação](manage-flicker.md) para obter mais informações.

## &#x200B;2. Solicitar apresentações para os escopos que você pretende renderizar

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Consulte [`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md) para obter mais informações.

## &#x200B;3. Renderizar ofertas com `applyPropositions` metadados

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## &#x200B;4. Registrar eventos de exibição para apresentações renderizadas

Eventos de exibição não são enviados automaticamente ao chamar `applyPropositions`. Depois que a renderização for concluída, use uma chamada `sendEvent` que faça referência às propostas renderizadas:

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

Consulte [Gerenciar eventos de exibição](display-events.md) para obter mais informações.

>[!TIP]
>
>Se você usar [Eventos de página superior e inferior](top-bottom-page-events.md), essa chamada de &quot;exibição de registro&quot; geralmente será implementada na chamada de `sendEvent` inferior.

## &#x200B;5. Renderização

Se sua implementação exigir uma renderização posterior (como em aplicativos de página única), chame `applyPropositions` novamente com as mesmas propostas e metadados:

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

Se você precisar gravar um evento de exibição para essa nova renderização, consulte [Gerenciar eventos de exibição](display-events.md).
