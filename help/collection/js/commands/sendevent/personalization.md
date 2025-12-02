---
title: personalização
description: Renderize conteúdo diferente para usuários diferentes, criando uma experiência personalizada para eles.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

O objeto `personalization` configura quais decisões de personalização (ofertas ou propostas) são solicitadas e como elas são tratadas na solicitação e resposta. Ele é especialmente valioso em implementações do Adobe Target ou do Adobe Journey Optimizer, pois é a força motriz que permite personalizar o conteúdo exibido por usuário.

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

O objeto `personalization` contém as seguintes propriedades:

## `personalization.decisionScopes`

A propriedade `decisionScopes` é uma matriz de cadeias de caracteres que instrui o Web SDK a recuperar e retornar decisões de personalização. Cada item no array identifica um local, contexto ou posicionamento lógico onde o conteúdo personalizado é desejado.

Essa propriedade é útil quando você deseja buscar explicitamente conteúdo personalizado para áreas específicas ou componentes de uma página. Ela é especialmente valiosa em aplicativos de página única que podem exigir diferentes conjuntos de ofertas, conforme a navegação do usuário ou as alterações de exibição. Também é possível usar essa propriedade para otimizar o desempenho, recuperando apenas ofertas para os elementos da interface relevantes para o usuário.

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

No Adobe Target, cada escopo de decisão é mapeado para uma mbox ou atividade. No Adobe Journey Optimizer, cada escopo de decisão é mapeado para inserções de conteúdo ou campanhas da Web com base em decisões. No Offer Decisioning, os escopos de decisão mapeiam para quais ofertas ou propostas o visitante deve receber.

>[!TIP]
>
>Se você deseja solicitar (ou bloquear) o escopo global, use [`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled) em vez de especificá-lo aqui em `decisionScopes`.

## `personalization.surfaces`

A propriedade `surfaces` é uma matriz de cadeias de caracteres de [URI de superfície](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri) que definem manualmente o canal, dispositivo ou contexto para o qual a personalização é solicitada. Eles permitem distinguir entre diferentes experiências digitais, como domínios, aplicativos ou plataformas de dispositivos em seu ecossistema entre canais. Por padrão, a biblioteca infere a superfície padrão da página atual. Você pode usar essa propriedade para substituir a superfície inferida automaticamente para a página atual.

Essa propriedade é importante quando você deseja usar a personalização entre canais e deve distinguir como a personalização funciona entre canais separados. Ele permite criar ofertas distintas para sites diferentes na mesma organização da Adobe Experience Platform.

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

Essa propriedade é usada basicamente com o Adobe Journey Optimizer, pois corresponde às superfícies configuradas nas campanhas do Journey Optimizer e no gerenciamento de superfícies.

## `personalization.schemas`

A propriedade `schemas` é uma matriz de cadeias de caracteres de URI de esquema que filtram os tipos de conteúdo de personalização solicitados da Edge Network. Definir essa propriedade restringe a resposta recebida do Adobe para incluir apenas ofertas que correspondam às definições de tipo de conteúdo especificadas. Se for omitida, a biblioteca solicitará ofertas de todos os esquemas disponíveis para os escopos ou superfícies correspondentes.

Essa propriedade ajuda a otimizar o tamanho da resposta e garante que seu site ou aplicativo receba apenas tipos de oferta que possa lidar. Também é útil quando usado com aplicativos de página única que renderizam o conteúdo personalizado de uma maneira específica (como usar somente ações DOM ou objetos JSON).

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

Os seguintes URIs de esquema são compatíveis:

* **`https://ns.adobe.com/personalization/dom-action`**: Ofertas que são ações DOM diretas, normalmente geradas pelo Visual Experience Composer no Adobe Target. Eles contêm instruções para manipular automaticamente os elementos na página sem código adicional. É o padrão para a personalização da Web renderizada automaticamente.
* **`https://ns.adobe.com/personalization/html-content-item`**: ofertas que contêm HTML bruto entregues como uma cadeia de caracteres. Sua implementação normalmente insere esse conteúdo no local desejado na página, dando a você mais controle do que as ações DOM. Normalmente usado para banners, trechos ou conteúdo modal.
* **`https://ns.adobe.com/personalization/json-content-item`**: Ofertas formatadas como objeto JSON. Usado com mais frequência em implementações baseadas em API ou front-ends que esperam dados estruturados em vez de alterações no HTML ou DOM.
* **`https://ns.adobe.com/personalization/redirect-item`**: Ofertas que redirecionam para uma URL diferente. Usado para levar o usuário para uma nova página com base no direcionamento ou na lógica de decisão, como páginas de aterrissagem ou fluxos de integração.
* **`https://ns.adobe.com/personalization/ruleset-item`**: fornece um bloco de lógica de negócios para habilitar um mecanismo de regras do lado do cliente. Contém um conjunto de regras com versão que define condições lógicas e consequências (se/então lógica de personalização).
* **`https://ns.adobe.com/personalization/message/in-app`**: Ofertas formatadas especificamente para mensagens no aplicativo do Adobe Journey Optimizer, normalmente renderizadas como modais, banners, pop-ups ou sobreposições.
* **`https://ns.adobe.com/personalization/message/content-card`**: ofertas formatadas especificamente para cartões de conteúdo do Adobe Journey Optimizer, criados para feeds persistentes ou de estilo de caixa de entrada em aplicativos da Web ou móveis.
* **`https://ns.adobe.com/personalization/message/native-alert`**: Ofertas formatadas especificamente para alertas nativos do Adobe Journey Optimizer, acionando caixas de diálogo de notificação nativas da plataforma.
* **`https://ns.adobe.com/personalization/measurement`**: usado para rastrear cliques e interações em ofertas personalizadas. Não contém conteúdo que possa ser renderizado.
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**: esquema para alterar o histórico de eventos de um visitante no armazenamento local. Usado internamente pelos SDKs para rastrear quais experiências foram entregues ou bloqueadas. Não contém conteúdo que possa ser renderizado.
* **`https://ns.adobe.com/personalization/default-content-item`**: Fallback ou conteúdo padrão, normalmente quando nenhuma oferta personalizada está qualificada. Ela garante que os usuários não qualificados ainda recebam conteúdo, mantendo a experiência consistente.

## `personalization.sendDisplayEvent`

A propriedade `sendDisplayEvent` é um booleano que determina se um evento de notificação de exibição é enviado automaticamente para a Edge Network imediatamente após o conteúdo personalizado ser renderizado na página. Se omitido, seu valor padrão é `true`. Defina essa variável como `false` se você não quiser indicar que o conteúdo personalizado foi renderizado para rastreamento de impressão.

O caso de uso mais comum para definir essa variável como `false` é quando você planeja enviar outro comando em outro lugar na implementação que sinaliza um evento de exibição. Algumas implementações têm eventos de impressão e Analytics; essa propriedade oferece controle total sobre quais comandos `sendEvent` incrementam impressões.

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>As versões anteriores do Web SDK (versões 2.12.0 e anteriores) usam `sendDisplayNotifications`.

## `personalization.includePendingDisplayNotifications`

A propriedade `includePendingDisplayNotifications` é um booliano que controla se qualquer notificação de exibição pendente é agrupada na chamada `sendEvent` atual. As notificações de exibição pendentes são impressões para conteúdo personalizado que foram renderizados, mas ainda não relatados ao Edge Network como um evento de exibição. Essa propriedade é útil ao usar aplicativos de página única, pois a renderização do conteúdo personalizado e as chamadas de `sendEvent` podem ser assíncronas entre si.

O valor padrão para esta propriedade é `false`. Defina essa propriedade como `true` se desejar agrupar e liberar quaisquer notificações de exibição pendentes para que suas impressões sejam registradas com precisão. A implementação síncrona, como sites tradicionais, normalmente não precisa definir essa propriedade.

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

A propriedade `defaultPersonalizationEnabled` é um booleano que oferece controle explícito sobre como o Web SDK solicita o escopo de personalização padrão de toda a página (`__view__`) e a superfície para esse comando `sendEvent`. Por padrão, no primeiro comando `sendEvent` após um carregamento de página, o Web SDK solicita ofertas para o escopo de personalização padrão em toda a página e superfícies associadas. Os comandos `sendEvent` subsequentes não solicitam personalização padrão. Você pode usar essa propriedade para substituir esse comportamento. Isso é importante em implementações de aplicativos de página única, nas quais você pode solicitar a personalização padrão novamente enquanto o usuário navega em seu site. Você também pode usar essa propriedade quando quiser _somente_ enviar um evento de exibição sem duplicar a recuperação da oferta.

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

Essa propriedade usa a seguinte lógica, dependendo de como é definida:

* **Não definido**: solicitar personalização padrão quando ainda não tiver sido solicitado. Normalmente, a personalização padrão é solicitada no(a) primeiro(a) `sendEvent` após um carregamento de página, em seguida, não é solicitada novamente nas chamadas subsequentes de `sendEvent` na mesma página. A definição dessa propriedade substitui esse comportamento.
* **`true`**: solicitar explicitamente o escopo e a superfície padrão da página, mesmo que esse comando `sendEvent` não seja o primeiro após um carregamento de página. Os momentos ideais para definir esta propriedade como `true` são quando você precisa forçar uma solicitação de personalização padrão, como em cenários de aplicativo de página única.
* **`false`**: Suprimir explicitamente a solicitação para o escopo de página e superfície padrão, mesmo se este comando `sendEvent` for o primeiro após um carregamento de página. Os momentos ideais para definir essa propriedade como `false` são quando você deseja que determinado comando `sendEvent` não solicite novas ofertas e, em vez disso, apenas envie dados para o Analytics ou envie um evento de exibição.

## Componentes do Personalization usando a extensão de tag da Web SDK

O equivalente da extensão de marca Web SDK dessa propriedade é a seção [**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) ao configurar uma ação &#39;[!UICONTROL Send event]&#39;.
