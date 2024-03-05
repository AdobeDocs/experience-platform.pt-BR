---
title: Usar o Adobe Target com SDK da Web para personalização
description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK usando o Adobe Target
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 5%

---

# Uso [!DNL Adobe Target] e [!DNL Web SDK] para personalização

[!DNL Adobe Experience Platform] [!DNL Web SDK] podem fornecer e renderizar experiências personalizadas gerenciadas no [!DNL Adobe Target] ao canal da web. Você pode usar um editor WYSIWYG, chamado de [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou uma interface não visual, o [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para criar, ativar e entregar suas atividades e experiências de personalização.

>[!IMPORTANT]
>
>Saiba como migrar sua implementação do Target para o SDK da Web da plataforma com o [Migração do Target da at.js 2.x para o SDK da Web da plataforma](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=pt-BR) tutorial.
>
>Saiba como implementar o Target pela primeira vez com o [Implementar o Adobe Experience Cloud com o SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR) tutorial. Para obter informações específicas do Target, consulte a seção tutorial intitulada [Configurar o Target com o SDK da Web da plataforma](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


Os seguintes recursos foram testados e são atualmente compatíveis com o [!DNL Target]:

* [Testes A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Relatórios de impressão e conversão do A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=pt-BR)
* [Atividades do Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Atividades de direcionamento de experiência](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Testes multivariados (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Atividades do Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Relatórios de impressão e conversão do Target nativo](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Suporte do VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] diagrama do sistema

O diagrama a seguir ajuda a entender o fluxo de trabalho do [!DNL Target] e [!DNL Web SDK] edge decisioning.

![Diagrama da decisão de borda do Adobe Target com o SDK da Web da plataforma](./assets/target-platform-web-sdk.png)

| Chama | Detalhes |
| --- | --- |
| 1 | O dispositivo carrega o [!DNL Web SDK]. A variável [!DNL Web SDK] O envia uma solicitação para a rede de borda com dados XDM, a ID de ambiente dos fluxos de dados, os parâmetros transmitidos e a ID do cliente (opcional). A página (ou containers) é pré-oculta. |
| 2 | A rede de borda envia a solicitação aos serviços de borda para enriquecê-la com a ID do visitante, o consentimento e outras informações de contexto do visitante, como geolocalização e nomes amigáveis ao dispositivo. |
| 3 | A rede de borda envia a solicitação de personalização enriquecida para o [!DNL Target] com a ID do visitante e os parâmetros transmitidos. |
| 4 | Os scripts de perfil executam e, em seguida, fazem o feed no [!DNL Target] armazenamento de perfil. O armazenamento de perfil busca segmentos do [!UICONTROL Biblioteca de público-alvo] (por exemplo, segmentos compartilhados de [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], o [!DNL Adobe Experience Platform]). |
| 5 | Com base nos parâmetros de solicitação de URL e dados de perfil, [!DNL Target] determina quais atividades e experiências exibir para o visitante na exibição de página atual e para exibições futuras previamente buscadas. [!DNL Target] em seguida, o envia de volta para a rede de borda. |
| 6 | a. A rede de borda envia a resposta de personalização de volta para a página, incluindo, opcionalmente, valores de perfil para personalização adicional. O conteúdo personalizado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.<br>b. O conteúdo personalizado de exibições que são mostradas como resultado das ações do usuário em um Aplicativo de página única (SPA) é armazenado em cache para que possa ser aplicado instantaneamente, sem uma chamada de servidor adicional, quando as exibições forem acionadas. <br>. A Rede de borda envia a ID do visitante e outros valores em cookies, como consentimento, ID da sessão, identidade, verificação de cookie e personalização. |
| 7 | A rede de borda encaminha [!UICONTROL Analytics for Target] (A4T) detalhes (atividade, experiência e metadados de conversão) para o [!DNL Analytics] borda. |

## Ativando [!DNL Adobe Target]

Para habilitar [!DNL Target], faça o seguinte:

1. Ativar [!DNL Target] no seu [sequência de dados](../../../datastreams/overview.md) com o código de cliente apropriado.
1. Adicione o `renderDecisions` aos seus eventos.

Em seguida, opcionalmente, você também pode adicionar as seguintes opções:

* **`decisionScopes`**: recupere atividades específicas (úteis para atividades criadas com o compositor baseado em formulário) adicionando essa opção aos seus eventos.
* **[Pré-ocultação de trecho](../manage-flicker.md)**: ocultar apenas determinadas partes da página.

## Uso do VEC do Adobe Target

Para usar o VEC com uma [!DNL Web SDK] implementação, instale e ative o [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Cromo](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) Extensão do VEC Helper.

Para obter mais informações, consulte [Extensão auxiliar do Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) no *Guia do Adobe Target*.

## Renderização de conteúdo personalizado

Consulte [Renderização do conteúdo de personalização](../rendering-personalization-content.md) para obter mais informações.

## Públicos-alvo no XDM

Ao definir públicos-alvo para seus [!DNL Target] atividades que são entregues por meio do [!DNL Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR) devem ser definidas e usadas. Depois de definir esquemas XDM, classes e grupos de campos de esquema, você pode criar um [!DNL Target] regra de público-alvo definida pelos dados XDM para direcionamento. Dentro de [!DNL Target], os dados XDM são exibidos no [!UICONTROL Audience Builder] como um parâmetro personalizado. O XDM é serializado usando notação de pontos (por exemplo, `web.webPageDetails.name`).

Se você tiver [!DNL Target] atividades com públicos predefinidos que usam parâmetros personalizados ou um perfil de usuário não são entregues corretamente pelo SDK. Em vez de usar parâmetros personalizados ou o perfil do usuário, você deve usar o XDM. No entanto, há campos de direcionamento de público prontos para uso compatíveis por meio do [!DNL Web SDK] que não exigem XDM. Esses campos estão disponíveis no [!DNL Target] Interface do usuário que não requer XDM:

* Biblioteca do Target
* Geografia
* Rede
* Sistema operacional
* Páginas do site
* Navegador
* Fontes de Tráfego
* Intervalo de tempo

Para obter mais informações, consulte [Categorias para públicos](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) no *Guia do Adobe Target*.

### Tokens de resposta

Os tokens de resposta são usados para enviar metadados a terceiros, como Google ou Facebook. Os tokens de resposta são retornados no `meta` campo dentro de `propositions` -> `items`. Aqui está uma amostra:

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

Para coletar os tokens de resposta, é necessário assinar o `alloy.sendEvent` promessa, iterar até `propositions`e extraia os detalhes de `items` -> `meta`.

A cada `proposition` tem um `renderAttempted` campo booleano que indica se a variável `proposition` foi renderizado ou não. Consulte a amostra abaixo:

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
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

Quando a renderização automática está ativada, a matriz de apresentações contém:

#### No carregamento da página:

* Compositor baseado em formulário `propositions` com `renderAttempted` sinalizador definido como `false`
* Proposições baseadas no Visual Experience Composer com `renderAttempted` sinalizador definido como `true`
* Proposições baseadas no Visual Experience Composer para uma exibição de aplicativo de página única com `renderAttempted` sinalizador definido como `true`

#### Em Exibição - alterar (para exibições em cache):

* Proposições baseadas no Visual Experience Composer para uma exibição de aplicativo de página única com `renderAttempted` sinalizador definido como `true`

Quando a renderização automática está desativada, a matriz de apresentações contém:

#### No carregamento da página:

* [!DNL Form-based Composer]baseado em `propositions` com `renderAttempted` sinalizador definido como `false`
* [!DNL Visual Experience Composer]apresentações com base em `renderAttempted` sinalizador definido como `false`
* [!DNL Visual Experience Composer]propostas com base em para uma visualização de Aplicativo de página única com `renderAttempted` sinalizador definido como `false`

#### Em Exibição - alterar (para exibições em cache):

* Proposições baseadas no Visual Experience Composer para uma exibição de aplicativo de página única com `renderAttempted` sinalizador definido como `false`

### Atualização de perfil único

A variável [!DNL Web SDK] permite atualizar o perfil para a variável [!DNL Target] e para o [!DNL Web SDK] como um evento de experiência.

Para atualizar uma [!DNL Target] , verifique se os dados do perfil foram transmitidos com o seguinte:

* Em `"data {"`
* Em `"__adobe.target"`
* Prefixo `"profile."`

| Chave | Tipo | Descrição |
| --- | --- | --- |
| `renderDecisions` | Booleano | Instrui o componente de personalização sobre se ele deve interpretar ações DOM |
| `decisionScopes` | Matriz `<String>` | Uma lista de escopos para os quais recuperar decisões |
| `xdm` | Objeto | Dados formatados no XDM que chega ao SDK da Web como um evento de experiência |
| `data` | Objeto | Pares de valor/chave arbitrários enviados para o [!DNL Target] soluções na classe target. |

Típica [!DNL Web SDK] o código que usa esse comando é semelhante ao seguinte:

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
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Solicitar recomendações

A tabela a seguir lista [!DNL Recommendations] atributos e se cada um é compatível por meio da variável [!DNL Web SDK]:

| Categoria | Atributo | Status do suporte |
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
| Página ou categoria de item para afinidade de categorias | user.categoryId | Suportado |

**Como enviar atributos do Recommendations para o Adobe Target:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Depuração

mboxTrace e mboxDebug foram descontinuados. Use um método de [Depuração do SDK da Web](/help/web-sdk/use-cases/debugging.md) em vez disso.

## Terminologia

__Apresentações:__ Entrada [!DNL Adobe Target], as apresentações se correlacionam com a experiência selecionada em uma Atividade.

__Esquema:__ O schema de uma decisão é o tipo de oferta em [!DNL Adobe Target].

__Escopo:__ O escopo da decisão. Entrada [!DNL Adobe Target], o escopo é a mBox. A mBox global é a `__view__` âmbito de aplicação.

__XDM:__ O XDM é serializado em notação de pontos e, em seguida, colocado em [!DNL Adobe Target] como parâmetros mBox.
