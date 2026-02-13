---
title: Gerenciar eventos de exibição no Web SDK
description: Explica o que são eventos de exibição e como usá-los no Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: personalização;exibir eventos;sendEvent;renderDecisions;applyPropositions;propositions;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Gerenciar eventos de exibição no Web SDK

Os eventos de exibição informam aos serviços de personalização ou análise que um conteúdo personalizado específico foi exibido para o usuário. O envio de eventos de exibição melhora a precisão dos relatórios, ajudando os sistemas downstream a distinguir entre o conteúdo que foi *solicitado* e o conteúdo que foi *realmente exibido*.

## Enviar eventos de exibição automaticamente

Os eventos de exibição automática geralmente são a opção mais simples. Eles são enviados imediatamente depois que o Web SDK terminar de renderizar o conteúdo qualificado da resposta `sendEvent`, o que pode melhorar a precisão dos relatórios.

Para enviar eventos de exibição automaticamente, use uma chamada `sendEvent` que defina `renderDecisions` como `true` e defina `personalization.sendDisplayEvent` como `true` (ou omita, já que `true` é o padrão):

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>Os eventos de exibição automática dependem da renderização gerenciada pela SDK. Se você renderizar o conteúdo manualmente (inclusive usando `applyPropositions`), deverá enviar eventos de exibição explicitamente usando `sendEvent`.

## Enviar eventos de exibição em `sendEvent` chamadas subsequentes

A inclusão de eventos de exibição em uma chamada `sendEvent` posterior é útil quando você deseja anexar dados adicionais de carregamento de página que não estão disponíveis ao solicitar personalização. Geralmente é usado ao implementar [Eventos de página superior e inferior](/help/collection/use-cases/personalization/top-bottom-page-events.md). A implementação correta dos eventos de exibição dessa maneira ajuda a evitar problemas com [Taxa de rejeição](https://experienceleague.adobe.com/pt-br/docs/analytics/components/metrics/bounce-rate) no Adobe Analytics.

1. Na chamada inicial de `sendEvent` (geralmente na parte superior da página), solicite e renderize o conteúdo, mas suprima os eventos de exibição automáticos definindo `renderDecisions` como `true` e `personalization.sendDisplayEvent` como `false`:

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. Mais tarde (geralmente na parte inferior da página), chame `sendEvent` com uma carga XDM que inclui eventos de exibição para propostas que foram renderizadas desde a solicitação anterior, definindo [`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md) como `true`:

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>Somente propostas renderizadas automaticamente que tiveram exibição suprimida são incluídas ao usar `includeRenderedPropositions`.

## Enviar eventos de exibição para apresentações renderizadas manualmente

Se você mesmo renderizar o conteúdo (renderização totalmente manual ou usando `applyPropositions`), deverá enviar eventos de exibição explicitamente usando o comando `sendEvent`. Chame `sendEvent` com uma carga XDM que inclua as seguintes propriedades:

* `_experience.decisioning.propositions` contendo as propostas renderizadas&#39; `id`, `scope`, e `scopeDetails`
* `_experience.decisioning.propositionEventType.display` definido como `1`

Os dois exemplos a seguir usam essa função auxiliar para criar a carga XDM do evento de exibição:

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

O exemplo a seguir usa renderização manual com eventos de exibição:

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

O exemplo a seguir usa o comando `applyPropositions` com eventos de exibição. Ele acorrenta `sendEvent`, `applyPropositions`, e depois outro `sendEvent`:

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## Erros comuns a serem evitados

* **Enviar eventos de exibição antes da conclusão da renderização**: enviar eventos de exibição após a conclusão da renderização automática, após a resolução de `applyPropositions` ou após a conclusão manual da lógica de renderização.
* **Enviar eventos de exibição para apresentações que você não renderizou**: incluir somente apresentações que foram exibidas ao usuário.
* **Descartando`scopeDetails`**: incluir `scopeDetails` do objeto de proposta ao enviar eventos de exibição.
