---
title: Integrar suporte IAB TCF 2.0 usando o SDK da Web da Adobe Experience Platform
description: Saiba como configurar o suporte do IAB TCF 2.0 para seu site sem usar o Adobe Experience Platform Launch.
seo-description: Saiba como configurar o consentimento do IAB TCF 2.0 com o Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---


# Integrar o suporte IAB TCF 2.0 ao SDK da Web da plataforma

Este guia mostra como integrar o Interative Advertising Bureau Transparency &amp; Consent Framework, versão 2.0 (IAB TCF 2.0) com o Adobe Experience Platform Web SDK sem usar o Experience Platform Launch. Para obter uma visão geral da integração com IAB TCF 2.0, leia a [visão geral](./overview.md). Para obter um guia sobre como se integrar ao Experience Platform Launch, leia o guia [IAB TCF 2.0 para Experience Platform Launch](./with-launch.md).

## Introdução

Este guia usa a interface `__tcfapi` para acessar as informações de consentimento. Pode ser mais fácil para você se integrar diretamente ao seu provedor de gerenciamento de nuvem (CMP). No entanto, as informações neste guia ainda podem ser úteis porque os CMPs geralmente fornecem funcionalidade semelhante à API TCF.

>[!NOTE]
>
>Estes exemplos presumem que quando o código é executado, `window.__tcfapi` é definido na página. Os CMPs podem fornecer um gancho onde você pode executar essas funções quando o objeto `__tcfapi` estiver pronto.

Para usar o IAB TCF 2.0 com Experience Platform Launch e a extensão AEP Web SDK, é necessário ter um schema XDM disponível. Se você não configurou nenhum desses, start exibindo esta página antes de continuar.

Além disso, este guia exige que você tenha uma compreensão funcional do Adobe Experience Platform Web SDK. Para obter uma atualização rápida, leia a [visão geral do Adobe Experience Platform Web SDK](../../home.md) e a documentação [Perguntas frequentes](../../web-sdk-faq.md).

## Ativação do consentimento padrão

Se quiser tratar todos os usuários desconhecidos da mesma forma, você pode definir o consentimento padrão para `pending`. Isso enfileira Eventos de experiência até que as preferências de consentimento sejam recebidas.

Para obter mais informações sobre o consentimento padrão, consulte a [seção de consentimento padrão](../../fundamentals/configuring-the-sdk.md#default-consent) na documentação de configuração do SDK da Web da plataforma.

### Definir o consentimento padrão com base em `gdprApplies`

Alguns CMPs fornecem a capacidade de determinar se o Regulamento Geral de Proteção de Dados (RGPD) se aplica ao cliente. Se você quiser supor consentimento para clientes nos quais o RGPD não se aplica, você pode usar o sinalizador `gdprApplies` na chamada da API TCF.

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

Neste exemplo, o comando `configure` é chamado depois que `tcData` é obtido da API TCF. Se `gdprApplies` for verdadeiro, o consentimento padrão será definido como `pending`. Se `gdprApplies` for falso, o consentimento padrão será definido como `in`. Preencha a variável `alloyConfiguration` com sua configuração.

>[!NOTE]
>
>Quando o consentimento padrão é definido como `in`, o comando `setConsent` ainda pode ser usado para registrar suas preferências de consentimento do cliente.

## Uso do evento setConsent

A API TCF 2.0 da IAB fornece uma evento para quando o consentimento é atualizado pelo cliente. Isso ocorre quando o cliente define inicialmente suas preferências e quando atualiza suas preferências.

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

Este bloco de código escuta o evento `useractioncomplete` e, em seguida, define o consentimento, transmitindo a cadeia de caracteres de consentimento e o sinalizador `gdprApplies`. Se você tiver identidades personalizadas para seus clientes, certifique-se de preencher a variável `identityMap`. Consulte o guia em [support agreement](../../consent/supporting-consent.md) para obter mais informações sobre como chamar `setConsent`.

## Incluindo informações de consentimento em sendEvent

Em schemas XDM, você pode armazenar informações de preferência de consentimento dos Eventos de experiência. Há duas maneiras de adicionar essas informações a cada evento.

Primeiro, você pode fornecer o schema XDM relevante em cada chamada `sendEvent`. O exemplo a seguir mostra uma maneira de fazer isso:

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

Este exemplo obtém as informações de consentimento para a API TCF e envia um evento com as informações de consentimento adicionadas ao schema XDM. Consulte o guia [eventos de rastreamento](../../fundamentals/tracking-events.md) para entender o que deve estar nas opções de comando `sendEvent`.

A outra maneira de adicionar as informações de consentimento a cada solicitação é com o retorno de chamada `onBeforeEventSend`. Leia a seção sobre [modificar eventos globalmente](../../fundamentals/tracking-events.md#modifying-events-globally) na documentação dos eventos de rastreamento para obter mais informações sobre como fazer isso.

## Próximas etapas

Agora que você aprendeu a usar o IAB TCF 2.0 com a extensão AEP Web SDK, também é possível optar por integrar com outras soluções de Adobe, como a Adobe Analytics ou a plataforma Dados do cliente em tempo real. Consulte a [visão geral do IAB Transparency &amp; Consent Framework 2.0](./overview.md) para obter mais informações.
