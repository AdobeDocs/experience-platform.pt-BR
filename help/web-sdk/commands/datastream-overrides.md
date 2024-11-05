---
title: Substituições de configuração da sequência de dados
description: Saiba como configurar substituições de sequência de dados por meio do SDK da Web.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 10%

---

# Configurar substituições de sequência de dados

O objeto `edgeConfigOverrides` permite substituir as definições de configuração para comandos executados na página atual. Esse objeto de substituição não é um comando, mas um objeto que você pode incluir na maioria dos comandos do SDK da Web.

Esse objeto é útil quando você tem sites ou subdomínios diferentes para países diferentes ou se tem várias sandboxes Experience Platform para armazenar dados específicos de diferentes unidades de negócios.

>[!IMPORTANT]
>
>Para obter instruções detalhadas de configuração completa para substituições de sequência de dados, consulte a documentação [substituições de configuração de sequência de dados](../../datastreams/overrides.md#configure-overrides).

A substituição da configuração da sequência de dados é um processo de duas etapas:

1. Primeiro, você deve definir a substituição da configuração da sequência de dados na [página de configuração da sequência de dados](../../datastreams/configure.md), na interface dos fluxos de dados. Consulte a documentação de [substituições de configuração da sequência de dados](../../datastreams/overrides.md#configure-overrides) para obter instruções sobre como configurar substituições.
2. Depois de configurar a substituição do fluxo de dados na interface do usuário, você deve enviar as substituições para o Edge Network de uma das seguintes maneiras:
   * Por meio da [extensão de tag](#tag-extension) do SDK da Web.
   * Por meio dos comandos do SDK da Web [`sendEvent`](../commands/sendevent/overview.md) ou [`configure`](../commands/configure/overview.md).
   * Por meio do comando [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network) do SDK móvel.

Se você definir substituições na configuração do SDK da Web e em um comando específico (como [`sendEvent`](sendevent/overview.md)), as substituições no comando específico terão prioridade.

>[!NOTE]
>
>Se você deseja uma substituição de configuração para *desabilitar* um serviço Experience Cloud, verifique se o serviço está primeiro *habilitado* na configuração da sequência de dados. Consulte a documentação sobre como [configurar sequências de dados](../../datastreams/configure.md#add-services) para obter detalhes sobre como adicionar serviços a uma sequência de dados.

## Enviar substituições de sequência de dados para o Edge Network pela extensão de tag do SDK da Web {#tag-extension}

Consulte a documentação sobre [configuração de substituições de sequência de dados](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) da extensão de tag do SDK da Web para obter instruções detalhadas de configuração.

Se você deseja configurar substituições de sequência de dados da extensão de marca do SDK da Web, defina cada campo desejado em **[!UICONTROL Substituições de configuração de sequência de dados]** ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção **[!UICONTROL Substituições de configuração da sequência de dados]**. Defina cada valor de substituição desejado.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

Se quiser definir substituições apenas para um comando específico, defina cada campo desejado nas ações de uma regra de tag.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Enviar evento]**.
1. Role para baixo até a seção denominada **[!UICONTROL Substituições de configuração da sequência de dados]**.
1. Defina cada campo desta seção com o valor de substituição desejado.
1. Clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

Campos separados são fornecidos para ambientes de [!UICONTROL Desenvolvimento], [!UICONTROL Preparo] e [!UICONTROL Produção]. Preencha cada campo desejado para cada ambiente.

## Envie as sobreposições para o Edge Network pela biblioteca JavaScript do SDK da Web {#library}

Depois de [configurar as substituições da sequência de dados](../../datastreams/overrides.md) na interface da Coleção de dados, você pode enviar as substituições para o Edge Network, por meio da biblioteca JavaScript do SDK da Web.

Se estiver usando o SDK da Web, enviar as substituições para o Edge Network por meio do comando `edgeConfigOverrides` é a segunda e última etapa da ativação das substituições de configuração da sequência de dados.

As substituições de configuração de sequência de dados são enviadas para a rede de borda por meio do comando `edgeConfigOverrides` do SDK da Web. Este comando cria substituições de sequência de dados que são passadas para [!DNL Edge Network] no próximo comando. Se você estiver usando o comando `configure`, as substituições serão passadas para cada solicitação.

O comando `edgeConfigOverrides` cria substituições de sequência de dados que são passadas para [!DNL Edge Network] no próximo comando.

Quando uma substituição de configuração é enviada com o comando `configure`, ela é incluída nos seguintes comandos do SDK da Web.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

As opções definidas globalmente podem ser substituídas pela opção de configuração em comandos individuais.

### Enviar substituições de configuração por meio do comando `sendEvent` do SDK da Web {#send-event}

O exemplo abaixo mostra todas as opções de configuração de sequência de dados dinâmica com suporte em uma chamada `sendEvent`.

Se a configuração da sequência de dados tiver todos os serviços com suporte habilitados, a amostra abaixo substituirá essa configuração e desabilitará todos os serviços (consulte a configuração `enabled: false` em cada serviço).

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
      reportSuites: ["ujslconfigoverrides3"],
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

| Parâmetro | Descrição |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | Use esse parâmetro para permitir que uma única solicitação seja enviada para uma sequência de dados diferente da definida pelo comando `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Define a configuração de sequência de dados dinâmica para o serviço Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Define se o evento será enviado para o serviço Experience Platform ou não. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Define os conjuntos de dados usados para o evento. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Define se o evento é enviado ou não para o serviço do Offer Decisioning. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Define se o evento é enviado ou não para o serviço de segmentação de borda. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Define se os dados do evento são enviados para os destinos de borda do. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Define se os dados do evento são enviados para o serviço Adobe Journey Optimizer ou não. |
| `com_adobe_analytics.enabled` | Define se os dados do evento são enviados para o Adobe Analytics ou não. |
| `com_adobe_analytics.reportSuites[]` | Uma matriz de strings que determina para quais conjuntos de relatórios você deseja enviar dados do Analytics. |
| `com_adobe_identity.idSyncContainerId` | O contêiner de sincronização de ID de terceiros que você deseja usar no Audience Manager. Para que esse contêiner de sincronização de ID funcione, você deve definir `com_adobe_audience_manager.enabled` como `true`. Caso contrário, o serviço Audience Manager será desativado. |
| `com_adobe_target.enabled` | Define se os dados do evento são enviados para o Adobe Target. |
| `com_adobe_target.propertyToken` | O token da propriedade de destino do Adobe Target. |
| `com_adobe_audience_manager.enabled` | Define se os dados do evento são enviados para o serviço Audience Manager. |
| `com_adobe_launch_ssf` | Define se os dados do evento são enviados para o encaminhamento pelo lado do servidor. |

### Enviar substituições de configuração por meio do comando `configure` do SDK da Web {#send-configure}

O exemplo abaixo mostra como seria uma substituição de configuração em um comando `configure`.

Se a configuração da sequência de dados tiver todos os serviços com suporte habilitados, a amostra abaixo substituirá essa configuração e desabilitará todos os serviços (consulte a configuração `enabled: false` em cada serviço).

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
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
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
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

| Parâmetro | Descrição |
|---|---|
| `orgId` | A ID organizacional IMS correspondente à sua conta Adobe. |
| `edgeConfigOverrides.datastreamId` | Use esse parâmetro para permitir que uma única solicitação seja enviada para uma sequência de dados diferente da definida pelo comando `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Define a configuração de sequência de dados dinâmica para o serviço Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Define se o evento será enviado para o serviço Experience Platform ou não. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Define os conjuntos de dados usados para o evento. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Define se o evento é enviado ou não para o serviço do Offer Decisioning. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Define se o evento é enviado ou não para o serviço de segmentação de borda. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Define se os dados do evento são enviados para os destinos de borda do. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Define se os dados do evento são enviados para o serviço Adobe Journey Optimizer ou não. |
| `com_adobe_analytics.enabled` | Define se os dados do evento são enviados para o Adobe Analytics ou não. |
| `com_adobe_analytics.reportSuites[]` | Uma matriz de strings que determina para quais conjuntos de relatórios você deseja enviar dados do Analytics. |
| `com_adobe_identity.idSyncContainerId` | O contêiner de sincronização de ID de terceiros que você deseja usar no Audience Manager. Para que esse contêiner de sincronização de ID funcione, você deve definir `com_adobe_audience_manager.enabled` como `true`. Caso contrário, o serviço Audience Manager será desativado. |
| `com_adobe_target.enabled` | Define se os dados do evento são enviados para o Adobe Target. |
| `com_adobe_target.propertyToken` | O token da propriedade de destino do Adobe Target. |
| `com_adobe_audience_manager.enabled` | Define se os dados do evento são enviados para o serviço Audience Manager. |
| `com_adobe_launch_ssf` | Define se os dados do evento são enviados para o encaminhamento pelo lado do servidor. |

