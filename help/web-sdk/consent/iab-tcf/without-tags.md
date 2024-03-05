---
title: Integrar o suporte ao IAB TCF 2.0 usando o SDK da Web da Adobe Experience Platform
description: Saiba como configurar o suporte IAB TCF 2.0 para seu site sem usar tags.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Integrar o suporte ao IAB TCF 2.0 com o SDK da Web da plataforma

Este guia mostra como integrar a Estrutura de transparência e consentimento do Interative Advertising Bureau, versão 2.0 (IAB TCF 2.0) com o SDK da Web da Adobe Experience Platform sem usar tags. Para obter uma visão geral da integração com a TCF 2.0 do IAB, leia o [visão geral](./overview.md). Para obter um guia sobre como integrar o com tags, leia o [Guia do IAB TCF 2.0 para tags](./with-tags.md).

## Introdução

Este guia usa o `__tcfapi` para acessar as informações de consentimento. Pode ser mais fácil integrar diretamente com seu provedor de gerenciamento de nuvem (CMP). No entanto, as informações neste guia ainda podem ser úteis, pois os CMPs geralmente fornecem funcionalidade semelhante à API TCF.

>[!NOTE]
>
>Esses exemplos presumem que, quando o código for executado, `window.__tcfapi` é definido na página. Os CMPs podem fornecer um gancho em que você pode executar essas funções quando a variável `__tcfapi` objeto está pronto.

Para usar o IAB TCF 2.0 com tags e a extensão SDK da Web da Adobe Experience Platform, é necessário ter um esquema XDM disponível. Se você não tiver configurado nenhum deles, comece visualizando esta página antes de continuar.

Além disso, este guia requer que você tenha uma compreensão funcional do SDK da Web da Adobe Experience Platform. Para uma atualização rápida, leia o [Visão geral do SDK da Web do Adobe Experience Platform](../../home.md) e a variável [Perguntas frequentes](../../faq.md) documentação.

## Ativação do consentimento padrão

Se quiser tratar todos os usuários desconhecidos da mesma forma, defina [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) para `pending` ou `out`. Isso enfileira ou descarta os Eventos de experiência até que as preferências de consentimento sejam recebidas.

### Definir o consentimento padrão com base em `gdprApplies`

Algumas CMPs fornecem a capacidade de determinar se o Regulamento Geral sobre a Proteção de Dados (GDPR) se aplica ao cliente. Se você quiser assumir o consentimento para clientes aos quais o GDPR não se aplica, poderá usar o `gdprApplies` na chamada à API TCF.

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

Neste exemplo, a variável `configure` é chamado depois que a variável `tcData` é obtido da API TCF. Se `gdprApplies` é true, o consentimento padrão está definido como `pending`. Se `gdprApplies` é falso, o consentimento padrão está definido como `in`. Certifique-se de preencher o `alloyConfiguration` com sua configuração.

>[!NOTE]
>
>Quando o consentimento padrão é definido como `in`, o `setConsent` O comando ainda pode ser usado para registrar as preferências de consentimento dos clientes.

## Uso do evento setConsent

A API da TCF do IAB 2.0 fornece um evento para quando o consentimento é atualizado pelo cliente. Isso ocorre quando o cliente define inicialmente suas preferências e quando o cliente atualiza suas preferências.

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

Este bloco de código escuta a `useractioncomplete` evento e, em seguida, define o consentimento, transmitindo a cadeia de consentimento e a variável `gdprApplies` sinalizador. Se você tiver identidades personalizadas para seus clientes, preencha o `identityMap` variável. Consulte o guia em [consentimento de suporte](../../consent/supporting-consent.md) para obter mais informações sobre como chamar `setConsent`.

## Inclusão de informações de consentimento em sendEvent

Nos esquemas XDM, você pode armazenar informações de preferência de consentimento de Eventos de experiência. Há duas maneiras de adicionar essas informações a cada evento.

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

Esse exemplo obtém as informações de consentimento da API TCF e envia um evento com as informações de consentimento adicionadas ao esquema XDM.

A outra maneira de adicionar as informações de consentimento a cada solicitação é com o [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) retorno de chamada.

## Próximas etapas

Agora que você aprendeu a usar o IAB TCF 2.0 com a extensão SDK da Web da plataforma, também é possível optar por integrar com outras soluções de Adobe, como Adobe Analytics ou Adobe Real-time Customer Data Platform. Consulte a [Visão geral da Estrutura de transparência e consentimento 2.0 do IAB](./overview.md) para obter mais informações.
