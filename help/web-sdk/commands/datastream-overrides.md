---
title: Substituições de configuração da sequência de dados
description: Saiba como configurar substituições de sequência de dados por meio do SDK da Web.
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

---


# Configurar substituições de sequência de dados

A variável `edgeConfigOverrides` permite substituir as definições de configuração para comandos executados na página atual. Esse objeto de substituição não é um comando, mas um objeto que você pode incluir na maioria dos comandos do SDK da Web.

Esse objeto é útil quando você tem sites ou subdomínios diferentes para países diferentes ou se tem várias sandboxes Experience Platform para armazenar dados específicos de diferentes unidades de negócios.

>[!IMPORTANT]
>
>Para obter instruções detalhadas de configuração completa para substituições de fluxo de dados, consulte o [substituições de configuração da sequência de dados](../../datastreams/overrides.md#configure-overrides) documentação.

A substituição da configuração da sequência de dados é um processo de duas etapas:

1. Primeiro, você deve definir a substituição da configuração do fluxo de dados na [página de configuração do fluxo de dados](../../datastreams/configure.md), na interface dos fluxos de dados. Consulte a [substituições de configuração da sequência de dados](../../datastreams/overrides.md#configure-overrides) documentação para obter instruções sobre como configurar sobreposições.
2. Depois de configurar a substituição do fluxo de dados na interface do usuário, você deve enviar as substituições para a Rede de borda de uma das seguintes maneiras:
   * Por meio do SDK da Web [extensão de tag](#tag-extension).
   * Por meio da `sendEvent` ou `configure` Comandos do SDK da Web.
   * Por meio do SDK móvel `sendEvent` comando.

Se você definir substituições na configuração do SDK da Web e em um comando específico (como [`sendEvent`](sendevent/overview.md)), as sobreposições no comando específico têm prioridade.

## Propriedades do objeto

As seguintes propriedades estão disponíveis nesse objeto:

* **Substituição de sequência de dados**: envia chamadas para um fluxo de dados diferente. Se você definir esse valor, outras substituições que exigem configuração de sequência de dados devem ser configuradas na sequência de dados definida aqui.
* **Contêiner de sincronização de ID de terceiros**: a ID do contêiner de destino da sincronização de ID de terceiros no Adobe Audience Manager. É necessário configurar uma substituição de container de ID de terceiros nas configurações do fluxo de dados antes de usar esse campo.
* **Token de propriedade de destino**: o token da propriedade de destino no Adobe Target. Antes de usar esse campo, é necessário configurar uma substituição do token de propriedade do Target nas configurações da sequência de dados.
* **Conjuntos de relatórios**: as IDs do conjunto de relatórios que serão substituídas no Adobe Analytics. É necessário configurar substituições do conjunto de relatórios nas configurações do fluxo de dados antes de usar esse campo.

## Enviar substituições de sequência de dados para a Rede de borda por meio da extensão de tag do SDK da Web {#tag-extension}

Consulte a documentação em [configuração de substituições de fluxo de dados](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) da extensão de tag do SDK da Web para obter instruções detalhadas de configuração.

Se quiser configurar substituições de sequência de dados na extensão de tag do SDK da Web, defina cada campo desejado em **[!UICONTROL Substituições de configuração da sequência de dados]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até **[!UICONTROL Substituições de configuração da sequência de dados]** seção. Defina cada valor de substituição desejado.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

Se quiser definir substituições apenas para um comando específico, defina cada campo desejado nas ações de uma regra de tag.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Enviar evento]**.
1. Role para baixo até a seção rotulada **[!UICONTROL Substituições de configuração da sequência de dados]**.
1. Defina cada campo desta seção com o valor de substituição desejado.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

São fornecidos campos separados para [!UICONTROL Desenvolvimento], [!UICONTROL Estágios], e [!UICONTROL Produção] ambientes. Preencha cada campo desejado para cada ambiente.

## Envie as substituições para a Rede de borda por meio da biblioteca JavaScript do SDK da Web {#library}

Depois [configurar as substituições do fluxo de dados](../../datastreams/overrides.md) Na interface da Coleção de dados, agora é possível enviar as substituições para a Rede de borda, por meio da biblioteca JavaScript do SDK da Web.

Se estiver usando o SDK da Web, enviar as substituições para a Rede de borda por meio do `edgeConfigOverrides` é a segunda e última etapa da ativação de substituições de configuração de fluxo de dados.

As substituições de configuração de sequência de dados são enviadas para a rede de borda por meio do comando `edgeConfigOverrides` do SDK da Web. Esse comando cria substituições de sequência de dados que são passadas para o [!DNL Edge Network] no próximo comando. Se você estiver usando a variável `configure` , as substituições são passadas para cada solicitação.

A variável `edgeConfigOverrides` cria substituições de fluxo de dados que são passadas para o [!DNL Edge Network] no próximo comando.

Quando uma substituição de configuração é enviada com o comando `configure`, ela é incluída nos seguintes comandos do SDK da Web.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

As opções definidas globalmente podem ser substituídas pela opção de configuração em comandos individuais.

### Enviar substituições de configuração por meio do SDK da Web `sendEvent` comando {#send-event}

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

### Enviar substituições de configuração por meio do SDK da Web `configure` comando {#send-configure}

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