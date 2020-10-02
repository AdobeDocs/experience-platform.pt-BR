---
title: Uso do IAB TCF 2.0 sem lançamento
seo-title: Configurar o consentimento do IAB TCF 2.0 com o SDK da Web da Adobe Experience Platform
description: Saiba como configurar o consentimento do IAB TCF 2.0 com o Adobe Experience Platform Web SDK
seo-description: Saiba como configurar o consentimento do IAB TCF 2.0 com o Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 48cebe994b450b0dac5e6f256ab81827a7e8a0d5
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Uso do IAB TCF 2.0 com a extensão do Adobe Experience Platform Web SDK

Este guia mostra como integrar o Interative Advertising Bureau Transparency &amp; Consent Framework, versão 2.0 (IAB TCF 2.0) com o SDK da Web da Adobe Experience Platform sem usar o Experience Platform Launch. Para obter uma visão geral da integração com o IAB TCF 2.0, leia a [visão geral](./overview.md). Para obter um guia sobre como fazer a integração com o Experience Platform Launch, leia o guia [IAB TCF 2.0 para o Experience Platform Launch](./with-launch.md).

## Introdução

Este guia usa a `__tcfapi` interface para acessar as informações de consentimento. Pode ser mais fácil para você se integrar diretamente ao seu provedor de gerenciamento de nuvem (CMP). No entanto, as informações neste guia ainda podem ser úteis porque os CMPs geralmente fornecem funcionalidade semelhante à API TCF.

>[!NOTE]
>
>Esses exemplos pressupõem que, quando o código for executado, `window.__tcfapi` seja definido na página. Os CMPs podem fornecer um gancho onde você pode executar essas funções quando o `__tcfapi` objeto estiver pronto.

Para usar o IAB TCF 2.0 com Experience Platform Launch e a extensão AEP Web SDK, é necessário ter um schema XDM disponível. Se você não configurou nenhuma dessas opções, consulte o guia [do start rápido JavaScript do](../../getting-started/quick-start-without-launch.md) Adobe Experience Platform Web SDK antes de continuar.

Além disso, este guia exige que você tenha uma compreensão funcional do SDK da Web da Adobe Experience Platform. Para obter uma atualização rápida, leia a visão geral [do SDK da Web da](../../home.md) Adobe Experience Platform e a documentação de perguntas [](../../getting-started/web-sdk-faq.md) frequentes.

## Ativação do consentimento padrão

Se quiser tratar todos os usuários desconhecidos da mesma forma, você pode definir o consentimento padrão como `pending`. Isso enfileira Eventos de experiência até que as preferências de consentimento sejam recebidas.

Para obter mais informações sobre o consentimento padrão, consulte a seção [consentimento](../../fundamentals/configuring-the-sdk.md#default-consent) padrão na documentação de configuração do SDK da Web da plataforma.

### Definir o consentimento padrão com base em `gdprApplies`

Alguns CMPs fornecem a capacidade de determinar se o Regulamento Geral de Proteção de Dados (RGPD) se aplica ao cliente. Se você quiser supor consentimento para clientes nos quais o RGPD não se aplica, você pode usar o `gdprApplies` sinalizador na chamada da API TCF.

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

Neste exemplo, o `configure` comando é chamado depois que `tcData` é obtido da API TCF. Se `gdprApplies` for verdadeiro, o consentimento padrão será definido como `pending`. Se `gdprApplies` for falso, o consentimento padrão será definido como `in`. Certifique-se de preencher a `alloyConfiguration` variável com sua configuração.

>[!NOTE]
>
>Quando o consentimento padrão é definido como `in`, o `setConsent` comando ainda pode ser usado para registrar as preferências de consentimento dos clientes.

## Uso do evento setConsent

A API IAB TCF 2.0 fornece uma evento para quando o consentimento é atualizado pelo cliente. Isso ocorre quando o cliente define inicialmente suas preferências e quando atualiza suas preferências.

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

Este bloco de código escuta o `useractioncomplete` evento e, em seguida, define o consentimento, transmitindo a string de consentimento e o `gdprApplies` sinalizador. Se você tiver identidades personalizadas para seus clientes, preencha a `identityMap` variável. Consulte o guia sobre o consentimento [de](../../fundamentals/supporting-consent.md) suporte para obter mais informações sobre chamada `setConsent`.

## Incluindo informações de consentimento em sendEvent

Em schemas XDM, você pode armazenar informações de preferência de consentimento dos Eventos de experiência. Há duas maneiras de adicionar essas informações a cada evento.

Primeiro, você pode fornecer o schema XDM relevante em cada `sendEvent` chamada. O exemplo a seguir mostra uma maneira de fazer isso:

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

Este exemplo obtém as informações de consentimento para a API TCF e envia um evento com as informações de consentimento adicionadas ao schema XDM. Consulte o guia de eventos [de](../../fundamentals/tracking-events.md) rastreamento para entender o que deve estar nas opções de `sendEvent` comando.

A outra maneira de adicionar as informações de consentimento a cada solicitação é com o `onBeforeEventSend` retorno de chamada. Leia a seção sobre como [modificar eventos globalmente](../../fundamentals/tracking-events.md#modifying-events-globally) na documentação de eventos de rastreamento para obter mais informações sobre como fazer isso.

## Próximas etapas

Agora que você aprendeu a usar o IAB TCF 2.0 com a extensão Adobe Experience Platform Web SDK, também pode optar por integrar com outras soluções de Adobe, como a Adobe Analytics ou a plataforma Dados do cliente em tempo real. Consulte a visão geral [do](./overview.md) IAB Transparency &amp; Consent Framework 2.0 para obter mais informações.
