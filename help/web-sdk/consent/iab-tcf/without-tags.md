---
title: Integrar o suporte ao IAB TCF 2.0 usando o Adobe Experience Platform Web SDK
description: Saiba como configurar o suporte IAB TCF 2.0 para seu site sem usar tags.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Integrar o suporte ao IAB TCF 2.0 com o Experience Platform Web SDK

Este guia mostra como integrar a Estrutura de transparência e consentimento do Interative Advertising Bureau, versão 2.0 (IAB TCF 2.0) com o Adobe Experience Platform Web SDK sem usar tags. Para obter uma visão geral da integração com a TCF do IAB 2.0, leia a [visão geral](./overview.md). Para obter um guia sobre como integrar com tags, leia o [guia da TCF do IAB 2.0 para tags](./with-tags.md).

## Introdução

Este guia usa a interface `__tcfapi` para acessar as informações de consentimento. Pode ser mais fácil integrar diretamente com seu provedor de gerenciamento de nuvem (CMP). No entanto, as informações neste guia ainda podem ser úteis, pois os CMPs geralmente fornecem funcionalidade semelhante à API TCF.

>[!NOTE]
>
>Esses exemplos presumem que, no momento em que o código for executado, `window.__tcfapi` estará definido na página. Os CMPs podem fornecer um gancho no qual você pode executar essas funções quando o objeto `__tcfapi` estiver pronto.

Para usar o IAB TCF 2.0 com tags e a extensão Adobe Experience Platform Web SDK, é necessário ter um esquema XDM disponível. Se você não tiver configurado nenhum deles, comece visualizando esta página antes de continuar.

Além disso, este guia requer que você tenha uma compreensão funcional do Adobe Experience Platform Web SDK. Para obter uma atualização rápida, leia a [visão geral do Adobe Experience Platform Web SDK](../../home.md) e a documentação de [Perguntas frequentes](../../faq.md).

## Ativação do consentimento padrão

Se quiser tratar todos os usuários desconhecidos da mesma forma, defina [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) como `pending` ou `out`. Isso enfileira ou descarta os Eventos de experiência até que as preferências de consentimento sejam recebidas.

### Definindo o consentimento padrão com base em `gdprApplies`

Algumas CMPs fornecem a capacidade de determinar se o Regulamento Geral sobre a Proteção de Dados (GDPR) se aplica ao cliente. Se você quiser assumir o consentimento para clientes aos quais o GDPR não se aplica, poderá usar o sinalizador `gdprApplies` na chamada de API TCF.

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
>Quando o consentimento padrão estiver definido como `in`, o comando `setConsent` ainda poderá ser usado para registrar as preferências de consentimento dos clientes.

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

Este bloco de código escuta o evento `useractioncomplete` e define o consentimento, transmitindo a cadeia de consentimento e o sinalizador `gdprApplies`. Se você tiver identidades personalizadas para seus clientes, preencha a variável `identityMap`. Consulte o guia em [setConsent](../../../web-sdk/commands/setconsent.md) para obter mais informações.

## Inclusão de informações de consentimento em sendEvent

Nos esquemas XDM, você pode armazenar informações de preferência de consentimento de Eventos de experiência. Há duas maneiras de adicionar essas informações a cada evento.

Primeiro, você pode fornecer o esquema XDM relevante em cada chamada do `sendEvent`. O exemplo a seguir mostra uma maneira de fazer isso:

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

A outra maneira de adicionar as informações de consentimento a cada solicitação é com o retorno de chamada [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md).

## Próximas etapas

Agora que você aprendeu a usar a TCF do IAB 2.0 com a extensão do Experience Platform Web SDK, também é possível optar por integrar a outras soluções da Adobe, como o Adobe Analytics ou o Adobe Real-Time Customer Data Platform. Consulte a [Visão geral da Estrutura de transparência e consentimento 2.0 do IAB](./overview.md) para obter mais informações.
