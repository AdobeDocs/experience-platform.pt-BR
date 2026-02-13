---
title: Renderizar apresentações manualmente
description: Renderize o conteúdo da apresentação usando sua própria lógica da interface do usuário (HTML, JSON ou esquemas personalizados) e, em seguida, registre os eventos de exibição.
keywords: personalização;propostas;renderização manual;sendEvent;decisionScopes;exibir eventos;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Renderizar apresentações manualmente

Use esse padrão quando precisar de controle total sobre como os itens de proposta são aplicados. Por exemplo, você está compondo uma interface complexa de conteúdo JSON ou deseja aplicar regras de negócios personalizadas antes da renderização.

## &#x200B;1. Solicitar apresentações

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Consulte o objeto [`personalization`](/help/collection/js/commands/sendevent/personalization.md) no comando [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) para obter mais informações.

## &#x200B;2. Renderizar itens de apresentação (exemplo)

Ao renderizar apresentações manualmente, elas podem ter muitas formas ou formas diferentes. O exemplo a seguir é um mínimo que encontra uma proposta por escopo e, em seguida, aplica o primeiro item de conteúdo do HTML encontrado.

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>Se você renderizar o HTML, verifique se ele é seguro para o seu ambiente. Trate a renderização de conteúdo como um limite de segurança (limpeza, fontes confiáveis e considerações sobre a CSP).

## &#x200B;3. Registrar eventos de exibição para o que você renderizou

Para propostas renderizadas manualmente, os eventos de exibição são gravados por meio de `sendEvent` chamadas que fazem referência às propostas renderizadas.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

Consulte [Gerenciar eventos de exibição](display-events.md) para obter mais informações.

## &#x200B;4. Renderização

Quando as alterações na interface do usuário exigirem uma nova renderização, execute novamente a lógica de renderização manual com base nos dados de proposta que você armazenou em cache (ou busque novamente, se necessário). Se precisar gravar uma exibição para cenários de nova renderização, consulte [Gerenciar eventos de exibição](display-events.md).
