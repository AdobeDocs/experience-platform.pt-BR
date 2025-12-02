---
title: edgeConfigOverrides
description: Configure substituições de fluxo de dados apenas para o comando sendEvent.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides` (`sendEvent` comando)

O objeto `edgeConfigOverrides` permite substituir as definições de configuração apenas para o comando `sendEvent` atual. Esse objeto é útil quando você tem comandos específicos na mesma página que deseja executar com definições de configuração diferentes do restante da implementação do Web SDK. Se quiser substituir as definições de configuração de todos os comandos em uma determinada página, considere usar o objeto [`edgeConfigOverrides` no comando `configure`](../configure/edgeconfigoverrides.md).

O processo de substituição da configuração de sequência de dados abrangente consiste em duas etapas principais:

1. Primeiro, você deve definir a substituição da configuração da sequência de dados ao [configurar uma sequência de dados](/help/datastreams/configure.md) na interface dos fluxos de dados. Consulte [Substituições de configuração de sequência de dados](/help/datastreams/overrides.md) na documentação de sequências de dados para obter instruções sobre como configurar substituições.
1. Depois de configurar a substituição da sequência de dados na interface dos fluxos de dados, você pode configurar o objeto `edgeConfigOverrides`.

Observe que o comando `configure` também suporta um objeto `edgeConfigOverrides`; consulte [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) sob o comando `configure`. O objeto `edgeConfigOverrides` no comando `sendEvent` tem precedência sobre o objeto `edgeConfigOverrides` no comando `configure`, se ambos estiverem definidos.

## Exemplo

Se a configuração da sequência de dados tiver todos os serviços com suporte habilitados, a amostra abaixo substituirá essa configuração e desabilitará todos os serviços (consulte a configuração `enabled: false` em cada serviço). Este objeto oferece suporte às mesmas propriedades que o objeto [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) no comando `configure`.

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## Substituições da configuração da sequência de dados usando a extensão de tag do Web SDK

O equivalente da extensão de marca Web SDK deste objeto é a seção [Substituições de configuração de sequência de dados](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides) ao configurar a ação &#39;[!UICONTROL Send event]&#39;.
