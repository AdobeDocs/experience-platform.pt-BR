---
title: autoCollectPropositionInteractions
description: Coletar dados automaticamente ao clicar em um link.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

A propriedade `autoCollectPropositionInteractions` é uma configuração opcional que determina se o Web SDK coleta automaticamente interações de apresentação. O valor é um mapa de provedores de decisão, cada um com um valor que indica como as interações automáticas de apresentação devem ser tratadas.

Quando você habilita o rastreamento automático da interação de apresentação, os cliques em um elemento de apresentação renderizado para o DOM são automaticamente coletados pelo Web SDK. Esta coleção inclui quaisquer experiências renderizadas automaticamente ao DOM pelo Web SDK e experiências renderizadas ao DOM usando o comando [`applyPropositions`](../applypropositions.md).

Se você omitir essa propriedade ao configurar o Web SDK, o padrão será `{"AJO": "always", "TGT": "never"}`. Se preferir não rastrear automaticamente as interações de apresentação, defina o valor como `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

As propriedades suportadas neste objeto incluem:

| Propriedade | Descrição |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer. |
| **`TGT`** | Adobe Target. |

Os valores possíveis para cada propriedade incluem:

| Valor | Descrição |
| --- | --- |
| **`always`** | Sempre colete automaticamente `interact` eventos para qualquer elemento associado a uma proposta. |
| **`never`** | Nunca colete automaticamente `interact` eventos para elementos associados a uma proposta. |
| **`decoratedElementsOnly`** | Colete automaticamente `interact` eventos para elementos associados a uma proposta se o elemento incluir atributos de dados especificando um rótulo ou token. |

## Atributos de dados {#data-attributes}

Você pode usar atributos de dados em elementos para adicionar especificidade a uma interação.

| Nome | Atributo de dados | Descrição |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | Quando o atributo de dados do rótulo estiver presente em um elemento clicado, ele será incluído nos detalhes da interação enviados para a Edge Network. O Web SDK procura um atributo de dados de rótulo começando com o elemento clicado e subindo a árvore DOM. O Web SDK usa o primeiro rótulo encontrado. |
| **[!UICONTROL Token]** | `data-aep-click-token` | Use este token ao utilizar as políticas de decisão em [campanhas baseadas em código do Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Você pode usar o token para distinguir qual item de política de decisão foi clicado. Quando o atributo de dados token estiver presente em um elemento clicado, ele será incluído nos detalhes de interação enviados para a Edge Network. O Web SDK procura um atributo de dados de token começando com o elemento clicado e subindo na árvore DOM. O Web SDK usa o primeiro token encontrado. |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | O Web SDK adiciona automaticamente esse identificador exclusivo aos elementos do container ao renderizar propostas. O Web SDK usa essa ID para correlacionar elementos DOM com propostas. Como essa é uma ID exigida pelo Web SDK, você não deve alterá-la de forma alguma. Você pode ignorá-lo com segurança. |

## Exemplo

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### Usando `autoCollectPropositionInteractions` com o comando `applyPropositions` {#apply-propositions}

O comando [`applyPropositions`](../applypropositions.md) é uma maneira conveniente de renderizar apresentações para o DOM. No entanto, no caso de campanhas baseadas em código com JSON, você pode usar esse comando para correlacionar um elemento DOM existente (ou o elemento do seu aplicativo renderizado na tela com base nos valores JSON) com uma proposta.

Essa correlação ativa o rastreamento automático de interação para esse elemento e atribui a esse elemento a apresentação apropriada. Para fazer isso, defina o `actionType` como `track`.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Configurar interações automáticas de apresentação para a extensão de tag do Web SDK

Os dois menus suspensos a seguir ao configurar a extensão de tag do Web SDK são o equivalente a esse objeto:

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
