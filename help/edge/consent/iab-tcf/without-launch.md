---
title: Integrar o suporte da TCF 2.0 do IAB usando o SDK da Web da Adobe Experience Platform
description: Saiba como configurar o suporte do IAB TCF 2.0 para o seu site sem usar o Adobe Experience Platform Launch.
seo-description: Saiba como configurar o consentimento do IAB TCF 2.0 com o SDK da Web da Adobe Experience Platform
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Integrar o suporte do IAB TCF 2.0 ao SDK da Web da plataforma

Este guia mostra como integrar a Estrutura de transparência e consentimento do Interative Advertising Bureau, versão 2.0 (IAB TCF 2.0) com o SDK da Web da Adobe Experience Platform sem usar o Experience Platform Launch. Para obter uma visão geral da integração com o IAB TCF 2.0, leia a [visão geral](./overview.md). Para obter um guia sobre como fazer a integração com o Experience Platform Launch, leia o [Guia TCF do IAB 2.0 para o Experience Platform Launch](./with-launch.md).

## Introdução

Este guia usa a interface `__tcfapi` para acessar as informações de consentimento. Pode ser mais fácil para você se integrar diretamente ao seu provedor de gerenciamento de nuvem (CMP). No entanto, as informações neste guia ainda podem ser úteis porque as CMPs geralmente fornecem funcionalidade semelhante à API TCF.

>[!NOTE]
>
>Esses exemplos presumem que, quando o código é executado, `window.__tcfapi` é definido na página. As CMPs podem fornecer um gancho onde você pode executar essas funções quando o objeto `__tcfapi` estiver pronto.

Para usar o IAB TCF 2.0 com o Experience Platform Launch e a extensão Adobe Experience Platform Web SDK, é necessário ter um esquema XDM disponível. Se você não tiver definido qualquer um desses itens, comece visualizando esta página antes de continuar.

Além disso, este guia requer que você tenha uma compreensão funcional do SDK da Web da Adobe Experience Platform. Para obter um atualizado rápido, leia a [Visão geral do SDK da Web da Adobe Experience Platform](../../home.md) e a documentação de [Perguntas frequentes](../../web-sdk-faq.md).

## Ativação do consentimento padrão

Se quiser tratar todos os usuários desconhecidos da mesma maneira, você pode definir o consentimento padrão como `pending` ou `out`. Isso enfileira ou descarta os Eventos de experiência até que as preferências de consentimento sejam recebidas.

Para obter mais informações sobre o consentimento padrão, consulte a [seção de consentimento padrão](../../fundamentals/configuring-the-sdk.md#default-consent) na documentação de configuração do SDK da Web da plataforma.

### Definir o consentimento padrão com base em `gdprApplies`

Algumas CMPs fornecem a capacidade de determinar se o Regulamento Geral sobre a Proteção de Dados (GDPR) se aplica ao cliente. Se desejar supor o consentimento para clientes onde o GDPR não se aplica, você pode usar o sinalizador `gdprApplies` na chamada da API TCF.

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
>Quando o consentimento padrão é definido como `in`, o comando `setConsent` ainda pode ser usado para registrar as preferências de consentimento dos clientes.

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

Esse bloco de código escuta o evento `useractioncomplete` e, em seguida, define o consentimento, transmitindo a cadeia de consentimento e o sinalizador `gdprApplies`. Se você tiver identidades personalizadas para seus clientes, preencha a variável `identityMap`. Consulte o guia em [consentimento de suporte](../../consent/supporting-consent.md) para obter mais informações sobre como chamar `setConsent`.

## Inclusão de informações de consentimento em sendEvent

Em esquemas XDM, você pode armazenar informações de preferência de consentimento dos Eventos de experiência. Há duas maneiras de adicionar essas informações a cada evento.

Primeiro, você pode fornecer o esquema XDM relevante em cada chamada `sendEvent`. O exemplo a seguir mostra uma maneira de fazer isso:

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

Esse exemplo obtém as informações de consentimento da API TCF e envia um evento com as informações de consentimento adicionadas ao esquema XDM. Consulte o guia [eventos de rastreamento](../../fundamentals/tracking-events.md) para entender o que deve estar nas opções de comando `sendEvent`.

A outra maneira de adicionar as informações de consentimento a cada solicitação é com o retorno de chamada `onBeforeEventSend`. Leia a seção sobre [modificar eventos globalmente](../../fundamentals/tracking-events.md#modifying-events-globally) na documentação de eventos de rastreamento para obter mais informações sobre como fazer isso.

## Próximas etapas

Agora que você aprendeu a usar o IAB TCF 2.0 com a extensão SDK da Web da plataforma, também pode optar por integrar com outras soluções da Adobe, como o Adobe Analytics ou a Plataforma de dados do cliente em tempo real. Consulte a [Visão geral da Estrutura de transparência e consentimento 2.0 do IAB](./overview.md) para obter mais informações.
