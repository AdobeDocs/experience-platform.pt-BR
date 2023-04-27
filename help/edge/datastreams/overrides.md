---
title: Configurar substituições do datastream
description: Saiba como configurar substituições de conjunto de dados na interface do usuário do Datastreams e ativá-las por meio do SDK da Web.
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# Configurar substituições do datastream

As substituições de conjunto de dados permitem definir configurações adicionais para seus conjuntos de dados, que são passados para a Rede de borda por meio do SDK da Web.

Isso ajuda você a acionar diferentes comportamentos do conjunto de dados do que os padrão, sem criar um novo conjunto de dados ou modificar as configurações existentes.

A substituição da configuração do conjunto de dados é um processo de duas etapas:

1. Primeiro, você deve definir as substituições de configuração do conjunto de dados na variável [página de configuração do datastream](configure.md).
2. Em seguida, você deve enviar as substituições para a Edge Network por meio de um comando do SDK da Web ou usando o SDK da Web [extensão de tag](../extension/web-sdk-extension-configuration.md).

Este artigo explica o processo completo de substituição da configuração do conjunto de dados para cada tipo de substituição suportada.

## Configurar substituições do datastream na interface do usuário do Datastreams {#configure-overrides}

As substituições de configuração do conjunto de dados permitem modificar as seguintes configurações do conjunto de dados:

* Conjuntos de dados de evento Experience Platform
* Tokens de propriedade do Adobe Target
* Contêineres de sincronização de ID do Audience Manager
* Conjuntos de relatórios do Adobe Analytics

### Substituições de fluxo de dados para o Adobe Target {#target-overrides}

Para configurar substituições do datastream para um datastreamento Adobe Target, primeiro você deve ter um datastreamento Adobe Target criado. Siga as instruções para [configurar um conjunto de dados](configure.md) com o [Adobe Target](configure.md#target) serviço.

Depois de criar o armazenamento de dados, edite o [Adobe Target](configure.md#target) que você adicionou e usa o **[!UICONTROL Substituições de token de propriedade]** para adicionar as substituições do conjunto de dados desejadas, conforme mostrado na imagem abaixo. Adicione um token de propriedade por linha.

![Captura de tela da interface do usuário do Datastreams mostrando as configurações do serviço Adobe Target, com as substituições do token de propriedade realçadas.](../assets/datastreams/overrides/override-target.png)

Depois de ter adicionado as substituições desejadas, salve as configurações do armazenamento de dados.

Agora, você deve ter as substituições do armazenamento de dados do Adobe Target configuradas. Agora você pode [enviar as substituições para a Edge Network por meio do SDK da Web](#send-overrides).

### Substituições de fluxo de dados para o Adobe Analytics {#analytics-overrides}

Para configurar substituições do datastream para um datastreamento Adobe Analytics, primeiro você deve ter um [Adobe Analytics](configure.md#analytics) datastream criado. Siga as instruções para [configurar um conjunto de dados](configure.md) com o [Adobe Analytics](configure.md#analytics) serviço.

Depois de criar o armazenamento de dados, edite o [Adobe Analytics](configure.md#target) que você adicionou e usa o **[!UICONTROL Substituições do conjunto de relatórios]** para adicionar as substituições do conjunto de dados desejadas, conforme mostrado na imagem abaixo.

Selecionar **[!UICONTROL Mostrar Modo de Lote]** para ativar a edição em lote das substituições do conjunto de relatórios. Você pode copiar e colar uma lista de substituições do conjunto de relatórios, inserindo um conjunto de relatórios por linha.

![Captura de tela da interface do usuário do Datastreams mostrando as configurações do serviço Adobe Analytics, com as substituições do conjunto de relatórios realçadas.](../assets/datastreams/overrides/override-analytics.png)

Depois de ter adicionado as substituições desejadas, salve as configurações do armazenamento de dados.

Agora, você deve ter as substituições do armazenamento de dados do Adobe Analytics configuradas. Agora você pode [enviar as substituições para a Edge Network por meio do SDK da Web](#send-overrides).

### Substituições de fluxo de dados para conjuntos de dados de evento do Experience Platform {#event-dataset-overrides}

Para configurar substituições do datastream para conjuntos de dados de evento do Experience Platform, primeiro você deve ter um [Adobe Experience Platform](configure.md#aep) datastream criado. Siga as instruções para [configurar um conjunto de dados](configure.md) com o [Adobe Experience Platform](configure.md#aep) serviço.

Depois de criar o armazenamento de dados, edite o [Adobe Experience Platform](configure.md#aep) que você adicionou e selecione o **[!UICONTROL Adicionar conjunto de dados de evento]** opção para adicionar um ou mais conjuntos de dados de evento de substituição, conforme mostrado na imagem abaixo.

![Captura de tela da interface do usuário do Datastreams mostrando as configurações do serviço Adobe Experience Platform, com as substituições do conjunto de dados do evento realçadas.](../assets/datastreams/overrides/override-aep.png)

Depois de ter adicionado as substituições desejadas, salve as configurações do armazenamento de dados.

Agora, você deve ter as substituições do armazenamento de dados do Adobe Experience Platform configuradas. Agora você pode [enviar as substituições para a Edge Network por meio do SDK da Web](#send-overrides).

### Substituições de fluxo de dados para contêineres de sincronização de ID de terceiros {#container-overrides}

Para configurar substituições de armazenamento de dados para contêineres de sincronização de ID de terceiros, primeiro é necessário criar um conjunto de dados. Siga as instruções para [configurar um conjunto de dados](configure.md) para criar um.

Depois de criar o armazenamento de dados, acesse **[!UICONTROL Opções avançadas]** e ativar **[!UICONTROL Sincronização de ID de terceiros]** opção.

Em seguida, use o **[!UICONTROL Substituições da ID do contêiner]** para adicionar as IDs do contêiner que você deseja substituir a configuração padrão, conforme mostrado na imagem abaixo.

>[!IMPORTANT]
>
>As IDs de contêiner devem ser valores numéricos, como `1234567`e não cadeias de caracteres, como `"1234567"`. Se você enviar um valor de string por meio do SDK da Web como uma substituição de ID de container, você receberá um erro.

![Captura de tela da interface do usuário do Datastreams mostrando as configurações do datastream, com as substituições do contêiner de sincronização de ID de terceiros destacadas.](../assets/datastreams/overrides/override-container.png)

Depois de ter adicionado as substituições desejadas, salve as configurações do armazenamento de dados.

Agora, você deve ter as substituições do contêiner de sincronização de ID configuradas. Agora você pode [enviar as substituições para a Edge Network por meio do SDK da Web](#send-overrides).

## Enviar as substituições para a Edge Network por meio do SDK da Web {#send-overrides}

>[!NOTE]
>
>Como alternativa ao envio das substituições de configuração por meio de comandos do SDK da Web, é possível adicionar as substituições de configuração ao SDK da Web [extensão de tag](../extension/web-sdk-extension-configuration.md).

Depois [configuração das substituições do datastream](#configure-overrides) na interface do usuário da Coleta de dados, agora é possível enviar as substituições para a Edge Network, por meio do SDK da Web.

Enviar as substituições para a Edge Network por meio do SDK da Web é a segunda e última etapa da ativação das substituições de configuração do conjunto de dados.

As substituições de configuração do armazenamento de dados são enviadas para a Rede de borda por meio do `edgeConfigOverrides` comando SDK da Web. Esse comando cria substituições do datastream que são passadas para o [!DNL Edge Network] no comando seguinte ou, no caso de `configure` , para cada solicitação.

O `edgeConfigOverrides` cria substituições do datastream que são passadas para o [!DNL Edge Network] no comando seguinte ou, no caso de `configure`, para cada solicitação.

Quando uma substituição de configuração é enviada com a variável `configure` , ele é incluído nos seguintes comandos compatíveis.

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [configure](../fundamentals/configuring-the-sdk.md)

As opções especificadas globalmente podem ser substituídas pela opção de configuração em comandos individuais.

### Enviar substituições de configuração por meio do `sendEvent` comando {#send-event}

O exemplo abaixo mostra como uma substituição de configuração pode ser em um `sendEvent` comando.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
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

### Enviar substituições de configuração por meio do `configure` comando {#send-configure}

O exemplo abaixo mostra como uma substituição de configuração pode ser em um `configure` comando.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  edgeConfigId: "etc",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": { 
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
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

### Exemplo de carga útil {#payload-example}

Os exemplos acima geram um [!DNL Edge Network] carga com esta aparência:

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
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
    "state": {  }
  },
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```

