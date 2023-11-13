---
title: Uso de eventos na parte superior e inferior da página
description: Este artigo explica como usar os eventos principais e inferiores da página no SDK da Web.
source-git-commit: 5322156774388a19788529aee554424b2fb5d91b
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 2%

---


# Utilização de eventos de parte superior e inferior da página no SDK da Web

Quando você quiser proporcionar experiências personalizadas aos seus clientes, o tempo de carregamento de uma página da Web é essencial.

Para otimizar os tempos de carregamento e fornecer personalização o mais rápido possível, o SDK da Web é compatível com a configuração dos eventos na parte superior e inferior da página.

Os eventos na parte superior e inferior da página descrevem um método de carregar de forma assíncrona vários elementos na página, mantendo o tempo de carregamento da página no mínimo.

Essa configuração minimiza o tempo que um usuário tem para esperar até que o conteúdo personalizado seja carregado.

Em termos de precisão das métricas, o Adobe Analytics pode ignorar os eventos de topo de página, o que resulta em métricas mais precisas de registro, já que apenas uma ocorrência de página é registrada (a parte inferior do evento da página).

## Casos de uso {#use-cases}

Um varejista de vestuário esportivo deseja oferecer experiências personalizadas aos seus compradores, minimizando o atrito do usuário ao visitar seu site, tudo isso enquanto consegue coletar com precisão as métricas do visitante.

Ao usar os eventos de parte superior e inferior da página no SDK da Web, a equipe de marketing pode configurar a entrega de personalização da melhor maneira:

* O SDK da Web envia uma solicitação de personalização que é carregada assim que a página começa a carregar. Este é um evento de início de página.
* Quando a página terminar de carregar, um evento de exibição de página será registrado. Isso acontece posteriormente no processo de carregamento da página. Este é um evento de fim de página.

## Exemplo de evento do início da página {#top-of-page}

A amostra de código abaixo exemplifica uma configuração de evento de parte superior da página que solicita personalização, mas não envia notificações de exibição para propostas renderizadas automaticamente. As notificações de exibição serão enviadas como parte do evento de fim de página.

>[!BEGINTABS]

>[!TAB Evento do início da página]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Parâmetro | Obrigatório / Opcional | Descrição |
|---|---|---|
| `type` | Obrigatório | Defina esse parâmetro como `decisioning.propositionFetch`. Esse tipo de evento especial instrui o Adobe Analytics a eliminar esse evento. Ao usar o Customer Journey Analytics, também é possível configurar um filtro para eliminar esses eventos. |
| `renderDecisions` | Obrigatório | Defina esse parâmetro como `true`. Esse parâmetro informa ao SDK da Web para renderizar as decisões retornadas pela Rede de borda. |
| `personalization.sendDisplayEvent` | Obrigatório | Defina esse parâmetro como `false`. Isso interrompe o envio de notificações de exibição. |

>[!ENDTABS]

## Exemplos de evento na parte inferior da página {#bottom-of-page}

>[!BEGINTABS]

>[!TAB Proposições renderizadas automaticamente]

A amostra de código abaixo exemplifica uma configuração de evento da parte inferior da página, que envia notificações de exibição para propostas que foram renderizadas automaticamente na página, mas para as quais as notificações de exibição foram suprimidas no [parte superior da página](#top-of-page) evento.

>[!NOTE]
>
>Nesse cenário, é necessário chamar o evento de fim de página _após_ na parte superior da página um. No entanto, o evento de parte inferior da página não precisa aguardar até que a parte superior da página um seja concluída.

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parâmetro | Obrigatório / Opcional | Descrição |
|---|---|---|
| `personalization.includeRenderedPropositions` | Obrigatório | Defina esse parâmetro como `true`. Isso permite o envio de notificações de exibição que foram suprimidas no evento da parte superior da página. |
| `xdm` | Opcional | Use esta seção para incluir todos os dados necessários para o evento de fim de página. |

>[!TAB Proposições renderizadas manualmente]

A amostra de código abaixo exemplifica uma parte inferior da configuração do evento da página, que envia notificações de exibição para propostas que foram renderizadas manualmente na página (ou seja, para escopos ou superfícies de decisão personalizados).

>[!NOTE]
>
>Nesse cenário, o evento de parte inferior da página deve aguardar até que o evento de parte superior da página seja concluído para renderizar as propostas e registrar o evento de parte inferior da página.

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



| Parâmetro | Obrigatório / Opcional | Descrição |
|---|---|---|
| `xdm._experience.decisioning.propositions` | Obrigatório | Esta seção define as apresentações renderizadas manualmente. Você deve incluir a proposta `ID`, `scope`, e `scopeDetails`. Consulte a documentação sobre como [renderizar personalização manualmente](../personalization/rendering-personalization-content.md#manually) para obter mais informações sobre como registrar notificações de exibição para conteúdo renderizado manualmente. A personalização renderizada manualmente deve ser incluída na parte inferior da ocorrência da página. |
| `xdm._experience.decisioning.propositionEventType` | Obrigatório | Defina esse parâmetro como `display: 1`. |
| `xdm` | Opcional | Use esta seção para incluir todos os dados necessários para o evento de fim de página. |

>[!ENDTABS]


## Aplicativo de página única com ocorrências de página superior e inferior {#spa-example}


>[!BEGINTABS]

>[!TAB Primeira exibição de página]

O exemplo abaixo inclui a adição do obrigatório `xdm.web.webPageDetails.viewName` parâmetro. É isso que o torna um aplicativo de página única. A variável `viewName` neste exemplo, é a exibição carregada no carregamento da página.

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

// Bottom of page, send display notifications for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

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

>[!TAB Segunda exibição de página (Opção 1)]

Neste exemplo, não há necessidade de fazer uma divisão de página de cima/baixo porque a personalização da página já foi buscada.

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


>[!TAB Segunda exibição de página (Opção 2)]

Se ainda precisar atrasar a parte inferior da ocorrência da página, você pode usar `applyPropositions` para a parte superior da ocorrência da página. Como nenhuma personalização precisa ser buscada e nenhum dado do Analytics precisa ser gravado, não há necessidade de fazer uma solicitação à Rede de borda.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display notifications for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
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

>[!ENDTABS]

## Amostra do GitHub {#github-sample}

A amostra encontrada em [este endereço](https://github.com/adobe/alloy-samples/tree/main/top-and-bottom) demonstra como usar o Experience Platform e o SDK da Web para solicitar personalização na parte superior da página e enviar métricas de análise na parte inferior. Você pode baixar a amostra e executá-la localmente para entender como os eventos na parte superior e inferior da página funcionam.
