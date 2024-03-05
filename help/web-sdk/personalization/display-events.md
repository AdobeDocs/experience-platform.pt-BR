---
title: Gerenciar eventos de exibição no SDK da Web
description: Este artigo explica o que são eventos de exibição e como usá-los no SDK da Web.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Gerenciar eventos de exibição no SDK da Web

O SDK da Web usa eventos de exibição para informar seu serviço de personalização ou análise quando um conteúdo de personalização específico é exibido em uma página.

O envio de eventos de exibição melhora a precisão das métricas de personalização e fornece uma visão geral precisa do que os usuários veem na sua página.

O SDK da Web permite enviar eventos de exibição de duas maneiras:

* [Automaticamente](#send-automatically), imediatamente após o conteúdo personalizado ser renderizado na página. Consulte a documentação sobre como [renderizar conteúdo personalizado](rendering-personalization-content.md) para obter mais informações.
* [Manualmente](#send-sendEvent-calls), por meio de subsequentes `sendEvent` chamadas.

>[!NOTE]
>
>Os eventos de exibição não são enviados automaticamente ao chamar o `applyPropositions` função.

## Enviar eventos de exibição automaticamente {#send-automatically}

O envio de eventos de exibição fornece automaticamente métricas de análise mais precisas, já que o evento é enviado imediatamente após o carregamento da personalização. Essa implementação também tem um método de implementação mais simplificado.

Para enviar eventos de exibição automaticamente depois que o conteúdo personalizado for renderizado na página, você deve configurar os seguintes parâmetros:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` ou não especificado

O SDK da Web envia os eventos de exibição imediatamente após qualquer personalização ser renderizada como resultado de um `sendEvent` chame.

## Enviar eventos de exibição em chamadas sendEvent subsequentes {#send-sendEvent-calls}

Comparado a [automaticamente](#send-automatically) enviar eventos de exibição, ao incluí-los em eventos subsequentes `sendEvent` As chamadas do também têm a oportunidade de incluir mais informações sobre o carregamento de página na chamada do. Pode se tratar de informações adicionais, que não estavam disponíveis ao solicitar o conteúdo personalizado.

Além disso, o envio de eventos de exibição no `sendEvent` As chamadas do minimizam os erros de taxa de rejeição ao usar o Adobe Analytics.

>[!IMPORTANT]
>
>Ao usar apresentações renderizadas manualmente, os eventos de exibição só são compatíveis por meio de `sendEvent` chamadas. Nesse caso, não é possível enviar eventos de exibição automaticamente.

### Enviar eventos de exibição para apresentações renderizadas automaticamente {#auto-rendered-propositions}

Para enviar eventos de exibição para apresentações renderizadas automaticamente, você deve configurar os seguintes parâmetros no `sendEvent` ligue para:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` para o início da ocorrência da página

Para enviar os eventos de exibição, chame `sendEvent` com `personalization.includePendingDisplayNotifications: true`

### Enviar eventos de exibição para apresentações renderizadas manualmente {#manually-rendered-propositions}

Para enviar eventos de exibição para apresentações renderizadas manualmente, você deve incluí-los na `_experience.decisioning.propositions` Campo XDM, incluindo o `id`, `scope`, e `scopeDetails` nas apresentações.

Além disso, defina o `include _experience.decisioning.propositionEventType.display` campo para `1`.
