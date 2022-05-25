---
title: Uso do Adobe Target com o SDK da Web da plataforma
description: Saiba como renderizar conteúdo personalizado com o SDK da Web do Experience Platform usando o Adobe Target
keywords: target; adobe target; activity.id; experience.id; renderDecisões; decisionScopes; pré-ocultar trecho; vec; Experience Composer baseado em formulário; xdm; públicos-alvo; decisões; escopo; esquema; diagrama do sistema; diagrama
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 5%

---

# Usando [!DNL Adobe Target] com o [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] O pode entregar e renderizar experiências personalizadas gerenciadas no [!DNL Adobe Target] para o canal da Web. Você pode usar um editor WYSIWYG, chamado de [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou uma interface não visual, a variável [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para criar, ativar e entregar suas atividades e experiências de personalização.

>[!IMPORTANT]
>
>O [Documentação do Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en) O inclui tópicos que contêm informações específicas para o SDK da Web da plataforma, pois estão relacionados aos recursos e funcionalidades do Target.

Os seguintes recursos foram testados e atualmente são compatíveis com o [!DNL Target]:

* [Testes A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Relatórios de impressão e conversão do A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=pt-BR)
* [Atividades do Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Atividades de Direcionamento de experiência](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Testes multivariados (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* Atividades do [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Relatório de impressão e conversão do Target nativo](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Suporte ao VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] diagrama do sistema

O diagrama a seguir ajuda você a entender o fluxo de trabalho do [!DNL Target] e [!DNL Platform Web SDK] decisão de borda.

![Diagrama da decisão de borda do Adobe Target com o SDK da Web da plataforma](./assets/target-platform-web-sdk.png)

| Chame | Detalhes |
| --- | --- |
| 1 | O dispositivo carrega o [!DNL Platform Web SDK]. O [!DNL Platform Web SDK] envia uma solicitação para a rede de borda com dados XDM, a ID do ambiente do datastreams, parâmetros transmitidos e a ID do cliente (opcional). A página (ou contêineres) é pré-oculta. |
| 2 | A rede de borda envia a solicitação aos serviços de borda para enriquecê-la com a ID do visitante, o consentimento e outras informações de contexto do visitante, como localização geográfica e nomes amigáveis ao dispositivo. |
| 3 | A rede de borda envia a solicitação de personalização enriquecida para o [!DNL Target] com a ID do visitante e os parâmetros transmitidos. |
| 4 | Os scripts de perfil executam e, em seguida, fazem o feed [!DNL Target] armazenamento de perfil. O armazenamento de perfil busca segmentos do [!UICONTROL Biblioteca de público-alvo] (por exemplo, segmentos compartilhados de [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], o [!DNL Adobe Experience Platform]). |
| 5 | Com base nos parâmetros de solicitação de URL e dados de perfil, [!DNL Target] determina quais atividades e experiências serão exibidas para o visitante na exibição de página atual e para futuras exibições pré-buscadas. [!DNL Target] em seguida, envia isso de volta para a rede de borda. |
| 6 | a. A rede de borda envia a resposta de personalização de volta para a página, incluindo, opcionalmente, valores de perfil para personalização adicional. O conteúdo personalizado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.<br>b. O conteúdo personalizado para exibições que são mostradas como resultado das ações do usuário em um Aplicativo de página única (SPA) é armazenado em cache para que possa ser aplicado instantaneamente, sem uma chamada de servidor adicional, quando as exibições forem acionadas. <br>c. A rede de borda envia a ID do visitante e outros valores em cookies, como consentimento, ID da sessão, identidade, verificação de cookie, personalização e assim por diante. |
| 7 | A rede de borda avança [!UICONTROL Analytics para Target] (A4T) detalhes (metadados de atividade, experiência e conversão) para a [!DNL Analytics] borda. |

## Habilitar [!DNL Adobe Target]

Para ativar [!DNL Target], faça o seguinte:

1. Habilitar [!DNL Target] em seu [datastream](../../datastreams/overview.md) com o código de cliente apropriado.
1. Adicione o `renderDecisions` aos seus eventos.

Em seguida, opcionalmente, também é possível adicionar as seguintes opções:

* **`decisionScopes`**: Recupere atividades específicas (úteis para atividades criadas com o compositor baseado em formulário) adicionando essa opção aos eventos.
* **[Pré-ocultar trecho](../manage-flicker.md)**: Ocultar apenas determinadas partes da página.

## Uso do VEC do Adobe Target

Para usar o VEC com um [!DNL Platform Web SDK] implementação, instalar e ativar a variável [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Cromo](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) Extensão do VEC Helper.

Para obter mais informações, consulte [Extensão de assistente do Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) no *Guia do Adobe Target*.

## Renderização de conteúdo personalizado

Consulte [Renderização do conteúdo de personalização](../rendering-personalization-content.md) para obter mais informações.

## Públicos-alvo no XDM

Ao definir públicos para [!DNL Target] atividades fornecidas por meio da variável [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR) deve ser definida e usada. Após definir esquemas, classes e grupos de campos de esquema XDM, você pode criar um [!DNL Target] regra de público-alvo definida pelos dados XDM para direcionamento. Within [!DNL Target], os dados XDM são exibidos na variável [!UICONTROL Construtor de público-alvo] como parâmetro personalizado. O XDM é serializado usando a notação de pontos (por exemplo, `web.webPageDetails.name`).

Se tiver [!DNL Target] atividades com públicos-alvo predefinidos que usam parâmetros personalizados ou um perfil de usuário, elas não são entregues corretamente por meio do SDK. Em vez de usar parâmetros personalizados ou o perfil do usuário, você deve usar o XDM. No entanto, há campos de direcionamento de público-alvo prontos para uso com o suporte do [!DNL Platform Web SDK] que não exigem XDM. Esses campos estão disponíveis na variável [!DNL Target] Interface do usuário que não requer XDM:

* Biblioteca do Target
* Geografia
* Rede
* Operating System
* Páginas do site
* Navegador
* Fontes de Tráfego
* Intervalo de tempo

Para obter mais informações, consulte [Categorias para públicos](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) no *Guia do Adobe Target*.

### Tokens de resposta

Os tokens de resposta são usados principalmente para enviar metadados a terceiros, como Google, Facebook etc. Os tokens de resposta são retornados no `meta` no campo `propositions` -> `items`. Esta é uma amostra:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Para coletar os tokens de resposta, é necessário assinar `alloy.sendEvent` promessa, repita `propositions`
e extrair os detalhes de `items` -> `meta`. Cada `proposition` tem um `renderAttempted` campo booleano indicando se a variável `proposition` foi renderizado ou não. Consulte a amostra abaixo:

```js
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Quando a renderização automática é ativada, a matriz de propostas contém:

#### No carregamento da página:

* Composer baseado em formulário `propositions` com `renderAttempted` sinalizador definido como `false`
* Apresentações baseadas no Visual Experience Composer com `renderAttempted` sinalizador definido como `true`
* Apresentações baseadas no Visual Experience Composer para uma visualização de Aplicativo de página única com `renderAttempted` sinalizador definido como `true`

#### Na Exibição - alteração (para exibições em cache):

* Apresentações baseadas no Visual Experience Composer para uma visualização de Aplicativo de página única com `renderAttempted` sinalizador definido como `true`

Quando a renderização automática está desativada, a matriz de propostas contém:

#### No carregamento da página:

* Composer baseado em formulário `propositions` com `renderAttempted` sinalizador definido como `false`
* Apresentações baseadas no Visual Experience Composer com `renderAttempted` sinalizador definido como `false`
* Apresentações baseadas no Visual Experience Composer para uma visualização de Aplicativo de página única com `renderAttempted` sinalizador definido como `false`

#### Na Exibição - alteração (para exibições em cache):

* Apresentações baseadas no Visual Experience Composer para uma visualização de Aplicativo de página única com `renderAttempted` sinalizador definido como `false`

### Atualização de perfil único

O [!DNL Platform Web SDK] permite atualizar o perfil para a [!DNL Target] e à [!DNL Platform Web SDK] como um evento de experiência.

Para atualizar uma [!DNL Target] , certifique-se de que os dados do perfil sejam transmitidos com o seguinte:

* Em `“data {“`
* Em `“__adobe.target”`
* Prefixo `“profile.”` por exemplo, como abaixo

| Chave | Tipo | Descrição |
| --- | --- | --- |
| `renderDecisions` | Booleano | Instrui o componente de personalização se ele deve interpretar ações DOM |
| `decisionScopes` | Matriz `<String>` | Uma lista de escopos para recuperar decisões de |
| `xdm` | Objeto | Dados formatados no XDM que chegam ao SDK da Web da plataforma como um evento de experiência |
| `data` | Objeto | Pares de chave/valor arbitrários enviados para [!DNL Target] na classe de destino. |

Típica [!DNL Platform Web SDK] o código que usa esse comando é semelhante ao seguinte:

**`sendEvent`com dados de perfil**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Como enviar atributos de perfil para o Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Solicitar recomendações

A tabela a seguir lista [!DNL Recommendations] e se cada um é compatível com o [!DNL Platform Web SDK]:

| Categoria | Atributo | Status de suporte |
| --- | --- | --- |
| Recommendations - Atributos de entidade padrão | entity.id | Suportado |
|  | entity.name | Suportado |
|  | entity.categoryId | Suportado |
|  | entity.pageUrl | Suportado |
|  | entity.thumbnailUrl | Suportado |
|  | entity.message | Suportado |
|  | entity.value | Suportado |
|  | entity.inventory | Suportado |
|  | entity.brand | Suportado |
|  | entity.margin | Suportado |
|  | entity.event.detailsOnly | Suportado |
| Recommendations - Atributos de entidade personalizados | entity.yourCustomAttributeName | Suportado |
| Recommendations - Parâmetros de mbox/página reservados | excludedIds | Suportado |
|  | cartIds | Suportado |
|  | productPurchasedId | Suportado |
| Página ou categoria do item para afinidade de categorias | user.categoryId | Suportado |

**Como enviar atributos do Recommendations para o Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Depuração

mboxTrace e mboxDebug foram descontinuadas. Use [[!DNL Platform Web SDK] depuração](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologia

__Propostas:__ Em [!DNL Target], as apresentações estão correlacionadas à experiência selecionada em uma Atividade.

__Esquema:__ O schema de uma decisão é o tipo de oferta em [!DNL Target].

__Âmbito de aplicação:__ O âmbito da decisão. Em [!DNL Target], o escopo é a mBox. A mBox global é a `__view__` escopo.

__XDM:__ O XDM é serializado em notação de pontos e, em seguida, colocado em [!DNL Target] como parâmetros mBox.
