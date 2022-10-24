---
title: Integrar o suporte do IAB TCF 2.0 usando o Adobe Experience Platform Web SDK
description: Saiba como configurar o suporte do IAB TCF 2.0 para seu site sem usar tags.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Integrar o suporte do IAB TCF 2.0 ao SDK da Web da plataforma

Este guia mostra como integrar a Estrutura de transparência e consentimento do Interative Advertising Bureau, versão 2.0 (TCF 2.0 do IAB) ao SDK da Web da Adobe Experience Platform sem usar tags. Para obter uma visão geral da integração com o IAB TCF 2.0, leia a seção [visão geral](./overview.md). Para obter um guia sobre como integrar com tags, leia o [Guia TCF 2.0 do IAB para tags](./with-launch.md).

## Introdução

Este guia usa o `__tcfapi` interface para acessar as informações de consentimento. Pode ser mais fácil para você se integrar diretamente ao seu provedor de gerenciamento de nuvem (CMP). No entanto, as informações neste guia ainda podem ser úteis porque as CMPs geralmente fornecem funcionalidade semelhante à API TCF.

>[!NOTE]
>
>Esses exemplos pressupõem que, quando o código for executado, `window.__tcfapi` é definido na página. As CMPs podem fornecer um gancho onde você pode executar essas funções quando o `__tcfapi` O objeto está pronto.

Para usar o IAB TCF 2.0 com tags e a extensão Adobe Experience Platform Web SDK, é necessário ter um esquema XDM disponível. Se você não tiver definido qualquer um desses itens, comece visualizando esta página antes de continuar.

Além disso, este guia requer que você tenha uma compreensão funcional do SDK da Web da Adobe Experience Platform. Para um atualizador rápido, leia o [Visão geral do SDK da Web da Adobe Experience Platform](../../home.md) e [Perguntas frequentes](../../web-sdk-faq.md) documentação.

## Ativação do consentimento padrão

Se quiser tratar todos os usuários desconhecidos da mesma forma, defina o consentimento padrão para `pending` ou `out`. Isso enfileira ou descarta os Eventos de experiência até que as preferências de consentimento sejam recebidas.

Para obter mais informações sobre o consentimento padrão, consulte [seção de consentimento padrão](../../fundamentals/configuring-the-sdk.md#default-consent) na documentação de configuração do SDK da Web da plataforma.

### Definir o consentimento padrão com base em `gdprApplies`

Algumas CMPs fornecem a capacidade de determinar se o Regulamento Geral sobre a Proteção de Dados (GDPR) se aplica ao cliente. Se você quiser supor consentimento para clientes onde o GDPR não se aplica, poderá usar a variável `gdprApplies` na chamada da API TCF.

O exemplo a seguir mostra uma maneira de fazer isso:

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

Neste exemplo, a variável `configure` é chamado após a `tcData` é obtida da API TCF. If `gdprApplies` é true, o consentimento padrão é definido como `pending`. If `gdprApplies` é falso, o consentimento padrão é definido como `in`. Preencha os campos `alloyConfiguration` com sua configuração.

>[!NOTE]
>
>Quando o consentimento padrão é definido como `in`, o `setConsent` ainda pode ser usado para registrar as preferências de consentimento dos clientes.

## Uso do evento setConsent

A API TCF 2.0 do IAB fornece um evento para quando o consentimento é atualizado pelo cliente. Isso ocorre quando o cliente define inicialmente suas preferências e quando atualiza suas preferências.

O exemplo a seguir mostra uma maneira de fazer isso:

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Este bloco de código escuta o `useractioncomplete` e, em seguida, define o consentimento, transmitindo a cadeia de consentimento e a variável `gdprApplies` sinalizador. Se você tiver identidades personalizadas para seus clientes, preencha o `identityMap` variável. Consulte o guia em [consentimento prévio](../../consent/supporting-consent.md) para obter mais informações sobre chamada `setConsent`.

## Inclusão de informações de consentimento em sendEvent

Em esquemas XDM, você pode armazenar informações de preferência de consentimento dos Eventos de experiência. Há duas maneiras de adicionar essas informações a cada evento.

Primeiro, você pode fornecer o esquema XDM relevante em cada `sendEvent` chame. O exemplo a seguir mostra uma maneira de fazer isso:

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

Esse exemplo obtém as informações de consentimento da API TCF e envia um evento com as informações de consentimento adicionadas ao esquema XDM. Consulte a [rastreamento de eventos](../../fundamentals/tracking-events.md) guia para entender o que deve estar no `sendEvent` opções de comando.

A outra maneira de adicionar as informações de consentimento a cada solicitação é com o `onBeforeEventSend` retorno de chamada. Leia a seção em [modificar eventos globalmente](../../fundamentals/tracking-events.md#modifying-events-globally) na documentação de eventos de rastreamento para obter mais informações sobre como fazer isso.

## Próximas etapas

Agora que você aprendeu a usar o IAB TCF 2.0 com a extensão SDK da Web da plataforma, também pode optar por integrar com outras soluções do Adobe, como Adobe Analytics ou Adobe Real-time Customer Data Platform. Consulte a [Visão geral da Estrutura de transparência e consentimento 2.0 do IAB](./overview.md) para obter mais informações.
