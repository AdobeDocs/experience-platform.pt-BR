---
title: edgeConfigOverrides
description: Configurar substituições de fluxo de dados para sua implementação.
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` (`configure` comando)

O objeto `edgeConfigOverrides` permite substituir as definições de configuração para comandos executados na página atual. Esse objeto é útil quando você tem sites ou subdomínios diferentes para países diferentes ou se tem várias sandboxes da Experience Platform para armazenar dados específicos de diferentes unidades de negócios. Se você quiser substituir as definições de configuração de apenas um único comando na página, considere usar o objeto [`edgeConfigOverrides` no comando `sendEvent`](../sendevent/edgeconfigoverrides.md).

O processo de substituição da configuração do fluxo de dados consiste em duas etapas principais:

1. Primeiro, você deve definir a substituição da configuração da sequência de dados ao [configurar uma sequência de dados](/help/datastreams/configure.md) na interface dos fluxos de dados. Consulte [Substituições de configuração de sequência de dados](/help/datastreams/overrides.md) na documentação de sequências de dados para obter instruções sobre como configurar substituições.
1. Depois de configurar a substituição da sequência de dados na interface dos fluxos de dados, você pode configurar o objeto `edgeConfigOverrides`.

Ao definir o objeto `edgeConfigOverrides` no comando `configure`, ele se aplica a todos os dados enviados para o Adobe. Os seguintes comandos _também_ oferecem suporte ao objeto `edgeConfigOverrides`:

* [&quot;sendEvent&quot;](../sendevent/edgeconfigoverrides.md)
* [`setConsent`](../setconsent.md)
* [&quot;getIdentity&quot;](../getidentity.md)
* [&quot;appendIdentityToUrl&quot;](../appendidentitytourl.md)

A configuração `edgeConfigOverrides` em qualquer um dos comandos acima tem precedência sobre o objeto `edgeConfigOverrides` no comando `configure`, se ambos estiverem definidos. Se qualquer um desses comandos não contiver um objeto `edgeConfigOverrides`, o objeto `edgeConfigOverrides` no comando `configure` será usado.

## Exemplo

Se a configuração da sequência de dados tiver todos os serviços compatíveis ativados, o exemplo abaixo substituirá essa configuração e desativará todos os serviços.

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| Parâmetro | Tipo | Descrição |
| --- | --- | --- |
| **`orgId`** | `string` | ID da organização IMS da sua empresa. |
| **`datastreamId`** | `string` | A ID da sequência de dados para a qual enviar dados. |
| **`com_adobe_experience_platform`** | `object` | Define a configuração da sequência de dados dinâmica para serviços da Adobe Experience Platform. |
| **`com_adobe_experience_platform.enabled`** | `boolean` | Determina se o evento é enviado para o Adobe Experience Platform. |
| **`com_adobe_experience_platform.datasets`** | `object` | Define os conjuntos de dados usados para o evento. |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | Determina se o evento é enviado para o Offer Decisioning. |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | Determina se o evento é enviado para a Segmentação do Edge. |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | Determina se o evento é enviado para o Edge Destinations. |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | Determina se o evento será enviado para o Adobe Journey Optimizer. |
| **`com_adobe_analytics.enabled`** | `boolean` | Determina se o evento é enviado para o Adobe Analytics. |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | Uma matriz de sequências de caracteres que determina para quais conjuntos de relatórios enviar dados do Analytics. |
| **`com_adobe_audience_manager.enabled`** | `boolean` | Determina se o evento é enviado para o Adobe Audience Manager. |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | O contêiner de sincronização de ID de terceiros que você deseja usar no Audience Manager. Requer `com_adobe_audience_manager.enabled` definido como `true`. Caso contrário, o serviço Audience Manager será desativado. |
| **`com_adobe_target.enabled`** | `boolean` | Determina se o evento é enviado para o Adobe Target. |
| **`com_adobe_target.propertyToken`** | `string` | O token da propriedade de destino do Adobe Target. |
| **`com_adobe_launch_ssf`** | `boolean` | Determina se o evento é enviado para o encaminhamento do lado do servidor. |

## Substituições de configuração usando a extensão de tag do Web SDK

O equivalente da extensão de tag do Web SDK deste campo está em [Substituições de configuração](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) ao configurar a extensão de tag.
