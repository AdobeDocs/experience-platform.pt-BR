---
title: autoTrackPropositionInteractionsEnabled
description: Saiba como configurar o SDK da Web do Experience Platform para coletar automaticamente dados de links.
source-git-commit: ec5fd1c8228388ced96f58476e0174c8a0ff00df
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---


# `autoTrackPropositionInteractionsEnabled`

A propriedade `autoTrackPropositionInteractionsEnabled` é uma configuração opcional que determina se o SDK da Web deve coletar automaticamente interações de apresentação.

O valor é um mapa de provedores de decisão, cada um com um valor que indica como as interações automáticas de apresentação devem ser tratadas.

## Valores compatíveis {#supported-values}

Por padrão, as interações automáticas de apresentação são _sempre_ coletadas para Adobe Journey Optimizer (`AJO`) e _nunca_ coletadas para Adobe Target (`TGT`).

O valor padrão de `autoTrackPropositionInteractions` é mostrado abaixo.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

Consulte a tabela abaixo para obter os valores de configuração compatíveis com cada provedor de decisão.

| Valor | Descrição |
| --- | --- |
| `always` | [!DNL Web SDK] sempre coletará automaticamente `interact` eventos para qualquer elemento associado a uma proposta. |
| `never` | [!DNL Web SDK] nunca coletará automaticamente `interact` eventos para elementos associados a uma proposta. |
| `decoratedElementsOnly` | [!DNL Web SDK] coletará automaticamente `interact` eventos para elementos associados a uma proposta, mas somente se o elemento incluir atributos de dados especificando um rótulo ou token. |

## Rastreamento automático da interação da apresentação {#logic}

Ao habilitar o rastreamento automático de interação de apresentação, os cliques em um elemento de apresentação renderizado para o DOM serão coletados automaticamente pelo [!DNL Web SDK]. Isso inclui quaisquer experiências renderizadas automaticamente para o DOM por [!DNL Web SDK] e experiências renderizadas para o DOM usando o comando [`applyPropositions`](../applypropositions.md).

### Atributos de dados {#data-attributes}

Você pode usar atributos de dados em elementos para adicionar especificidade a uma interação.

| Nome | Atributo de dados | Descrição |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | Quando o atributo de dados de rótulo estiver presente em um elemento clicado, ele será incluído com os detalhes de interação enviados para o [!DNL Edge Network]. O [!DNL Web SDK] procura um atributo de dados de rótulo começando com o elemento clicado e subindo na árvore DOM. O [!DNL Web SDK] usa o primeiro rótulo encontrado. |
| [!DNL Token] | `data-aep-click-token` | Use este token ao utilizar as políticas de decisão em [campanhas baseadas em código do Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Você pode usar o token para distinguir qual item de política de decisão foi clicado. Quando o atributo de dados token estiver presente em um elemento clicado, ele será incluído nos detalhes de interação enviados para o Edge Network. O [!DNL Web SDK] procura um atributo de dados de token começando com o elemento clicado e subindo na árvore DOM. O [!DNL Web SDK] usa o primeiro token encontrado. |
| [!DNL Interact ID] | `data-aep-interact-id` | O [!DNL Web SDK] adiciona automaticamente essa ID exclusiva aos elementos do contêiner ao renderizar propostas. O SDK da Web usa essa ID para correlacionar [!DNL DOM] elementos com propostas. Como essa é uma ID exigida pela [!DNL Web SDK], você não deve alterá-la de forma alguma. Você pode ignorá-lo com segurança. |

**Exemplo**

Consulte o trecho de código abaixo para ver um exemplo do uso de atributos de dados.

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### O comando `applyPropositions` {#apply-propositions}

Consulte a documentação do [`applyPropositions`](../applypropositions.md) para saber como esse comando funciona.

O comando `applyPropositions` é uma maneira conveniente de renderizar apresentações para o [!DNL DOM]. No entanto, no caso de campanhas baseadas em código com `JSON`, você pode usar este comando para correlacionar um elemento [!DNL DOM] existente (ou aquele que seu código de aplicativo renderizou para a tela com base nos valores `JSON`) com uma proposta.

Essa correlação ativa o rastreamento automático de interação para esse elemento e atribui a esse elemento a apresentação apropriada. Para fazer isso, defina o `actionType` como `track`.

**Exemplo**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Ativar o rastreamento de cliques de apresentações e interações automáticas por meio da extensão de tag do SDK da Web {#tag-extension}

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando sua credencial da Adobe ID.
2. Navegue até **Coleção de dados** > **Marcas**.
3. Selecione a propriedade de tag desejada.
4. Navegue até **Extensões** e selecione **Configurar** no cartão do SDK da Web da Adobe Experience Platform.
5. Role para baixo até a seção **[!UICONTROL Coleção de dados]** e marque a caixa de seleção **Habilitar propostas e rastreamento de link de interação**.
6. Selecione **Salvar** e publique suas alterações.

## Ativar o rastreamento de links de propostas e interações automáticas por meio da biblioteca JavaScript do SDK da Web {#library}

O rastreamento de apresentações é habilitado por padrão em [!DNL Web SDK]. No entanto, você pode configurá-lo ainda mais usando o valor `autoTrackPropositionInteractionsEnabled` ao executar o comando [`configure`](../configure/overview.md).

Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `{"AJO": "always", "TGT": "never"}`. Se preferir não rastrear automaticamente as interações de apresentação, defina o valor como `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoTrackPropositionInteractionsEnabled": {"AJO": "always", "TGT": "never"}
});
```
