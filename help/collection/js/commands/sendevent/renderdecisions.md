---
title: renderDecision
description: Renderize conteúdo personalizado que esteja qualificado para renderização automática.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

A propriedade `renderDecisions` permite forçar o Web SDK a renderizar qualquer conteúdo personalizado que esteja qualificado para renderização automática.

Defina o booleano `renderDecisions` ao executar o comando `sendEvent`. Se omitida, essa propriedade assumirá `false` como padrão. Defina essa propriedade como `true` se desejar renderizar automaticamente o conteúdo personalizado.

>[!IMPORTANT]
>
>Propriedade `renderDecisions` incompatível com propriedade [`documentUnloading`](documentunloading.md). Evite definir ambas as propriedades como `true` simultaneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

Ao definir esta propriedade como `true`, inclua também escopos ou superfícies associados. Esses escopos ou superfícies podem ser solicitados automaticamente (como no primeiro comando `sendEvent` em uma página) ou explicitamente (usando [`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes) ou [`personalization.surfaces`](personalization.md#personalizationsurfaces)). Um problema comum ao renderizar a personalização é o seguinte cenário:

1. Um comando `sendEvent` é executado antecipadamente na página que solicita a personalização padrão com `renderDecisions` não definido (o padrão é `false`). As propostas são buscadas, mas não renderizadas.
1. Mais tarde na página, outro `sendEvent` aciona com `renderDecisions` definido como `true`, mas não inclui escopos ou superfícies. Como não há escopos ou superfícies nesta segunda chamada, nada é renderizado.

Você pode evitar esse problema ao:

* Definindo `renderDecisions` como `true` na primeira chamada `sendEvent`; ou
* Definindo explicitamente `decisionScopes` ou `surfaces` em uma chamada `sendEvent` subsequente ao definir `renderDecisions` como `true`.

## Renderizar decisões usando a extensão de tag do Web SDK

O equivalente da extensão de marca Web SDK desta propriedade é a caixa de seleção [**Renderizar decisões de personalização visual**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) na ação &#39;[!UICONTROL Send event]&#39;.
