---
title: Gerenciar eventos de exibição no Web SDK
description: Explica o que são eventos de exibição e como usá-los no Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Gerenciar eventos de exibição no Web SDK

Os eventos de exibição são usados pelo Web SDK para informar seu serviço de personalização ou análise quando um conteúdo de personalização específico é exibido em uma página. O envio de eventos de exibição melhora a precisão das métricas de personalização e fornece uma visão geral precisa do que os usuários veem na sua página.

>[!NOTE]
>
>Eventos de exibição não são enviados automaticamente ao chamar a função `applyPropositions`.

## Enviar eventos de exibição automaticamente

O envio de eventos de exibição fornece automaticamente métricas de análise mais precisas, já que o evento é enviado imediatamente após o carregamento da personalização. Essa implementação também tem um método de implementação mais simplificado.

Para enviar eventos de exibição automaticamente depois que o conteúdo personalizado for renderizado na página, você deve configurar os seguintes parâmetros:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` ou não especificado

O Web SDK envia os eventos de exibição imediatamente após qualquer personalização ser renderizada como resultado de uma chamada `sendEvent`.

## Enviar eventos de exibição em chamadas sendEvent subsequentes

Comparado ao envio automático de eventos de exibição, ao incluí-los nas chamadas subsequentes do `sendEvent`, você também tem a oportunidade de incluir mais informações sobre o carregamento da página na chamada. Pode se tratar de informações adicionais, que não estavam disponíveis ao solicitar o conteúdo personalizado.

Além disso, o envio de eventos de exibição em chamadas `sendEvent` minimiza erros de taxa de devolução ao usar o Adobe Analytics.

>[!IMPORTANT]
>
>Ao usar apresentações renderizadas manualmente, os eventos de exibição só têm suporte por meio de chamadas `sendEvent`. Nesse caso, não é possível enviar eventos de exibição automaticamente.

### Enviar eventos de exibição para apresentações renderizadas automaticamente

Para enviar eventos de exibição para apresentações renderizadas automaticamente, você deve configurar os seguintes parâmetros na chamada `sendEvent`:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` para o início da ocorrência da página

Para enviar os eventos de exibição, chame `sendEvent` com `personalization.includeRenderedPropositions: true`

### Enviar eventos de exibição para apresentações renderizadas manualmente

Para enviar eventos de exibição para propostas renderizadas manualmente, você deve incluí-los no campo XDM `_experience.decisioning.propositions`, incluindo os campos `id`, `scope` e `scopeDetails` das propostas.

Além disso, defina o campo `include _experience.decisioning.propositionEventType.display` como `1`.
