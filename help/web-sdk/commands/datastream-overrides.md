---
title: Substituições de configuração da sequência de dados
description: Saiba como configurar substituições de sequência de dados por meio do SDK da Web.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

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
   * Por meio dos comandos do SDK da Web `sendEvent` ou `configure`.
   * Por meio do comando `sendEvent` do SDK móvel.

Se você definir substituições na configuração do SDK da Web e em um comando específico (como [`sendEvent`](sendevent/overview.md)), as substituições no comando específico terão prioridade.

## Propriedades do objeto

As seguintes propriedades estão disponíveis nesse objeto:

* **Substituição de sequência de dados**: envia chamadas para uma sequência de dados diferente. Se você definir esse valor, outras substituições que exigem configuração de sequência de dados devem ser configuradas na sequência de dados definida aqui.
* **Contêiner de sincronização de ID de terceiros**: a ID do contêiner de sincronização de ID de terceiros de destino no Adobe Audience Manager. É necessário configurar uma substituição de container de ID de terceiros nas configurações do fluxo de dados antes de usar esse campo.
* **Token de propriedade de destino**: o token da propriedade de destino no Adobe Target. Antes de usar esse campo, é necessário configurar uma substituição do token de propriedade do Target nas configurações da sequência de dados.
* **Conjuntos de relatórios**: as IDs de conjunto de relatórios a serem substituídas no Adobe Analytics. É necessário configurar substituições do conjunto de relatórios nas configurações do fluxo de dados antes de usar esse campo.

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

O exemplo abaixo mostra como seria uma substituição de configuração em um comando `sendEvent`.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| Parâmetro | Descrição |
|---|---|
| `edgeConfigOverrides.datastreamId` | Use esse parâmetro para permitir que uma única solicitação seja enviada para uma sequência de dados diferente da definida pelo comando `configure`. |
| `com_adobe_analytics.reportSuites[]` | Uma matriz de strings que determina para quais conjuntos de relatórios deseja enviar dados do Analytics. |
| `com_adobe_identity.idSyncContainerId` | O contêiner de sincronização de ID de terceiros que você deseja usar no Audience Manager. |
| `com_adobe_target.propertyToken` | O token da propriedade de destino do Adobe Target. |

### Enviar substituições de configuração por meio do comando `configure` do SDK da Web {#send-configure}

O exemplo abaixo mostra como seria uma substituição de configuração em um comando `configure`.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

| Parâmetro | Descrição |
|---|---|
| `edgeConfigOverrides.datastreamId` | Use esse parâmetro para permitir que uma única solicitação seja enviada para uma sequência de dados diferente da definida pelo comando `configure`. |
| `com_adobe_analytics.reportSuites[]` | Uma matriz de strings que determina para quais conjuntos de relatórios deseja enviar dados do Analytics. |
| `com_adobe_identity.idSyncContainerId` | O contêiner de sincronização de ID de terceiros que você deseja usar no Audience Manager. |
| `com_adobe_target.propertyToken` | O token da propriedade de destino do Adobe Target. |
