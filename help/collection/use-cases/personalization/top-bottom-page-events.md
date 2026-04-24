---
title: Configurar os eventos de início e fim da página no Web SDK
description: Este artigo explica como usar os eventos principais e inferiores da página no Web SDK.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# Configurar os eventos de início e fim da página no Web SDK

Ao fornecer experiências personalizadas, o tempo de carregamento de uma página da Web é essencial. Para minimizar o tempo que um usuário aguarda pelo conteúdo personalizado, o Web SDK é compatível com a configuração de eventos na parte superior e inferior da página.

Os eventos na parte superior e inferior da página descrevem um método de carregar de forma assíncrona vários elementos na página, mantendo o tempo de carregamento da página no mínimo:

* O evento da parte superior da página solicita personalização assim que a página começa a carregar.
* O evento da parte inferior da página registra uma exibição de página quando a página termina de carregar.

O Adobe Analytics ignora a parte superior dos eventos de página, o que resulta em métricas mais precisas de gravação, pois apenas uma ocorrência de página é registrada (a parte inferior do evento da página).

Você pode configurar os eventos na parte superior e inferior da página de duas maneiras: chamando a biblioteca JavaScript do Web SDK (`alloy()`) diretamente ou usando a extensão de tag do Web SDK na interface do usuário de tags do Adobe Experience Platform. A ação [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) da extensão de marca inclui uma opção &#39;[!UICONTROL Use guided events]&#39; que pré-configura valores de campo para os cenários &#39;[!UICONTROL Request personalization]&#39; (parte superior da página) e &#39;[!UICONTROL Collect analytics]&#39; (parte inferior da página). Cada exemplo abaixo mostra ambas as implementações.

## Evento do início da página {#top-of-page}

O exemplo abaixo configura um evento de início de página que solicita personalização, mas suprime [eventos de exibição](display-events.md) para apresentações renderizadas automaticamente. Esses eventos de exibição são enviados com o final do evento da página.

>[!BEGINTABS]

>[!TAB biblioteca JavaScript]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Parâmetro | Obrigatório/Opcional | Descrição |
| --- | --- | --- |
| `type` | Obrigatório | Defina este parâmetro como `decisioning.propositionFetch`. Esse tipo de evento especial instrui o Adobe Analytics a eliminar esse evento. Ao usar o Customer Journey Analytics, você também pode configurar um filtro para soltar esses eventos. Consulte [Tipos de evento do Edge Network no Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types) para obter mais informações. |
| `renderDecisions` | Obrigatório | Defina este parâmetro como `true`. Esse parâmetro informa ao Web SDK para renderizar as decisões retornadas pela Edge Network. |
| `personalization.sendDisplayEvent` | Obrigatório | Defina este parâmetro como `false`. Esse parâmetro interrompe o envio de eventos de exibição. |

>[!TAB Extensão de tag do Web SDK]

Configure uma ação [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) na regra que é acionada na parte superior da página. Habilite **[!UICONTROL Use guided events]** e selecione **[!UICONTROL Request personalization]**. Esta opção bloqueia &#39;[!UICONTROL Type]&#39; para &#39;[!UICONTROL Decisioning Proposition Fetch]&#39;, &#39;[!UICONTROL Render visual personalization decisions]&#39; para habilitado e &#39;[!UICONTROL Automatically send a display event]&#39; para desabilitado.

Para definir esses campos manualmente, deixe **[!UICONTROL Use guided events]** desabilitado e configure cada campo você mesmo.

>[!ENDTABS]

## Exemplos de evento na parte inferior da página {#bottom-of-page}

### Proposições renderizadas automaticamente {#bottom-auto-rendered}

O exemplo abaixo configura um evento de parte inferior da página que envia eventos de exibição para propostas que foram renderizadas automaticamente na página, mas suprimidas no evento [parte superior da página](#top-of-page).

>[!BEGINTABS]

>[!TAB biblioteca JavaScript]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parâmetro | Obrigatório/Opcional | Descrição |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | Obrigatório | Defina este parâmetro como `true`. Esse parâmetro permite o envio de eventos de exibição que foram suprimidos no início da página. |
| `xdm` | Opcional | Use esse objeto para incluir todos os dados desejados para o evento da parte inferior da página. |

>[!TAB Extensão de tag do Web SDK]

Configure uma ação [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) na regra que é acionada na parte inferior da página. Habilite **[!UICONTROL Use guided events]** e selecione **[!UICONTROL Collect analytics]**. Esta opção bloqueia &#39;[!UICONTROL Include rendered propositions]&#39; para habilitado.

Para definir este campo manualmente, deixe **[!UICONTROL Use guided events]** desabilitado e habilite **[!UICONTROL Include rendered propositions]** diretamente. Opcionalmente, preencha o campo **[!UICONTROL XDM]** com um elemento de dados [objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) que transporta os dados da página.

>[!ENDTABS]

### Proposições renderizadas manualmente {#bottom-manually-rendered}

O exemplo abaixo configura um evento de parte inferior da página que envia eventos de exibição para propostas que foram renderizadas manualmente na página (ou seja, para escopos ou superfícies de decisão personalizados).

>[!NOTE]
>
>Nesse cenário, o evento de parte inferior da página deve aguardar até que o evento de parte superior da página seja concluído, para que as propostas possam ser renderizadas e registradas.

>[!BEGINTABS]

>[!TAB biblioteca JavaScript]

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```

| Parâmetro | Obrigatório/Opcional | Descrição |
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | Obrigatório | Esta seção define as apresentações renderizadas manualmente. Você deve incluir a proposta `id`, `scope` e `scopeDetails`. Consulte [Gerenciar eventos de exibição](display-events.md) para obter mais informações. O conteúdo de personalização renderizado manualmente deve ser incluído no final do evento da página. |
| `xdm._experience.decisioning.propositionEventType` | Obrigatório | Defina este parâmetro como `display: 1`. |
| `xdm` | Opcional | Use esse objeto para incluir todos os dados desejados para o evento da parte inferior da página. |

>[!TAB Extensão de tag do Web SDK]

A opção &#39;[!UICONTROL Use guided events]&#39; não abrange esse cenário, portanto, configure a ação manualmente:

1. Crie um elemento de dados [objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) (ou [Variável](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)) que preencha `_experience.decisioning.propositions` com cada `id`, `scope` e `scopeDetails` de proposta renderizada e defina `_experience.decisioning.propositionEventType.display` como `1`. Consulte [Gerenciar eventos de exibição](display-events.md) para obter mais informações.
1. Na ação [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) da parte inferior da regra de página, deixe **[!UICONTROL Use guided events]** desabilitado e faça referência ao elemento de dados do campo **[!UICONTROL XDM]**.

>[!ENDTABS]

## Aplicativo de página única com eventos de parte superior e inferior da página {#spa-example}

Em um aplicativo de página única, você deve especificar o nome da exibição em cada alteração de exibição para que o Web SDK renderize a personalização correta na parte superior da página e registre a exibição correta na parte inferior da página.

### Primeira exibição de página {#spa-first-view}

Neste exemplo, `home` é a exibição carregada no carregamento da página inicial.

>[!BEGINTABS]

>[!TAB biblioteca JavaScript]

A chamada superior solicita personalização para a exibição `home` sem gravar uma ocorrência do Analytics ou disparar eventos de exibição. A chamada inferior registra a exibição de página e aciona os eventos de exibição suprimidos. Inclua o mesmo `viewName` em ambas as chamadas para que a exibição seja registrada de forma consistente.

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB Extensão de tag do Web SDK]

1. Crie um elemento de dados [objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) que defina `web.webPageDetails.viewName` como o nome da exibição (por exemplo, `home`).
1. Configure uma ação de início de página [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): habilite **[!UICONTROL Use guided events]**, selecione **[!UICONTROL Request personalization]** e faça referência ao elemento de dados no campo **[!UICONTROL XDM]**.
1. Configure uma parte inferior da ação **[!UICONTROL Send event]** da página: habilite **[!UICONTROL Use guided events]**, selecione **[!UICONTROL Collect analytics]** e faça referência ao mesmo elemento de dados no campo **[!UICONTROL XDM]** para que `viewName` corresponda em ambos os eventos.

>[!ENDTABS]

### Segunda visualização de página — opção 1 {#spa-second-view-option-1}

Neste exemplo, um único evento é suficiente porque a personalização da página já foi buscada.

>[!BEGINTABS]

>[!TAB biblioteca JavaScript]

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

>[!TAB Extensão de tag do Web SDK]

1. Crie um elemento de dados [objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) que defina `web.webPageDetails.viewName` como o nome da nova exibição (por exemplo, `cart`).
1. Na alteração de exibição, configure uma única ação de [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): deixe **[!UICONTROL Use guided events]** desabilitado, habilite **[!UICONTROL Render visual personalization decisions]** e referencie o elemento de dados no campo **[!UICONTROL XDM]**.

>[!ENDTABS]

### Segunda visualização de página — opção 2 {#spa-second-view-option-2}

Use essa abordagem quando precisar atrasar o evento da parte inferior da página (por exemplo, quando os dados de análise da página não estiverem prontos no momento da alteração de exibição). Manipule a alteração de exibição em duas etapas:

1. Na parte superior da página, renderize as apresentações já buscadas sem fazer uma chamada de Edge Network.
1. Quando os dados do Analytics estiverem prontos, envie o evento da parte inferior da página.

Inclua o mesmo `viewName` em ambas as chamadas para que a exibição seja registrada de forma consistente.

>[!BEGINTABS]

>[!TAB biblioteca JavaScript]

Chame [`applyPropositions`](/help/collection/js/commands/applypropositions.md) na parte superior da página para renderizar as apresentações armazenadas em cache para a nova exibição. Em seguida, chame `sendEvent` na parte inferior da página com `includeRenderedPropositions: true` para que os eventos de exibição suprimidos sejam acionados.

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!TAB Extensão de tag do Web SDK]

1. Crie um elemento de dados [objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) que defina `web.webPageDetails.viewName` como o nome da nova exibição (por exemplo, `cart`).
1. Para o evento de início de página, configure uma ação [[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) e defina o campo **[!UICONTROL View name]** como o nome da exibição (por exemplo, `cart`). Essa ação renderiza as apresentações já buscadas sem entrar em contato com a Edge Network.
1. Para o evento da parte inferior da página, configure uma ação [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): habilite **[!UICONTROL Use guided events]**, selecione **[!UICONTROL Collect analytics]** e faça referência ao elemento de dados no campo **[!UICONTROL XDM]**.

>[!ENDTABS]

## Amostra do GitHub {#github-sample}

A [amostra superior e inferior no repositório alloy-samples](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) demonstra como solicitar personalização na parte superior da página e enviar métricas de análise na parte inferior. Baixe a amostra e execute-a localmente para ver como os eventos na parte superior e inferior da página funcionam. A amostra usa a biblioteca JavaScript diretamente; os mesmos padrões se aplicam quando você configura regras equivalentes na extensão de tag da Web SDK.
