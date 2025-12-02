---
title: Configurar substituições de sequência de dados
description: Saiba como configurar substituições de fluxo de dados na interface do usuário de fluxos de dados e ativá-las por meio do Web SDK ou do Mobile SDK.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 53%

---

# Configurar substituições de sequência de dados

As substituições de fluxos de dados permitem definir configurações adicionais para seus fluxos de dados, que são transmitidos para a Edge Network por meio da Web SDK ou da SDK móvel.

Isso ajuda a acionar comportamentos de sequência de dados diferentes dos padrão, sem criar uma sequência de dados ou modificar as configurações existentes.

A substituição da configuração da sequência de dados é um processo de duas etapas:

1. Primeiro, você deve definir a substituição da configuração da sequência de dados na [página de configuração da sequência de dados](configure.md).
2. Em seguida, você deve enviar as sobreposições para a Edge Network de uma das seguintes maneiras:
   * Por meio dos comandos `sendEvent` ou `configure` [Web SDK](#send-overrides).
   * Por meio da [extensão de tag](../tags/extensions/client/web-sdk/configure/configuration-overrides.md) do Web SDK.
   * Por meio da API [sendEvent](#send-overrides) do Mobile SDK ou usando [Regras](#send-overrides).

Este artigo explica o processo completo para criar cada tipo de substituição de configuração de sequência de dados compatível.

>[!IMPORTANT]
>
>Atualmente, as integrações da [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) não oferecem suporte a substituições de sequência de dados.
><br>
>As substituições de sequência de dados devem ser usadas quando você precisa que dados diferentes sejam enviados para sequências de dados diferentes. Não use substituições de fluxo de dados para casos de uso de personalização ou dados de consentimento.

## Casos de uso {#use-cases}

Para melhorar o entendimento sobre como e quando usar substituições de sequência de dados, veja alguns casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse recurso.

**Coleta de dados de várias regiões**

Uma empresa tem sites ou subdomínios diferentes para países diferentes nos quais opera. Ela [configurou](configure.md) sequências de dados separadas com conjuntos de relatórios específicos do Analytics, tokens de propriedade do Adobe Target específicos de um país, esquemas específicos de um país, conjuntos de dados, configurações do Journey Optimizer e assim por diante. A empresa também tem um conjunto global de configurações onde agrega todos os dados específicos de um país.

Ao usar substituições de sequência de dados, a empresa pode alternar dinamicamente o fluxo dos dados para sequências de dados diferentes, em vez do comportamento padrão de enviar dados para uma sequência de dados.

Um caso de uso comum pode ser o envio de dados para um fluxo de dados específico de país e também para um fluxo de dados global em que os clientes executam uma ação importante, como fazer um pedido ou atualizar o perfil do usuário.

**Diferenciação de perfis e identidades para diferentes unidades de negócios**

Uma empresa com várias unidades de negócios deseja usar várias sandboxes da Experience Platform para armazenar dados específicos de cada unidade de negócios.

Em vez de enviar dados para uma sequência de dados padrão, a empresa pode usar substituições de sequência de dados para garantir que cada unidade de negócios tenha sua própria sequência de dados para receber dados.

## Configurar substituições na interface das sequências de dados {#configure-overrides}

As substituições de configuração de sequência de dados permitem modificar as seguintes configurações de sequência de dados:

* Conjuntos de dados de eventos da Experience Platform
* Tokens de propriedade do Adobe Target
* Containers de sincronização de ID do Audience Manager
* Conjuntos de relatórios do Adobe Analytics

### Substituições de sequência de dados para o Adobe Target {#target-overrides}

Para configurar substituições para uma sequência de dados do Adobe Target, primeiro você deve criar uma sequência de dados do Adobe Target. Siga as instruções para [configurar uma sequência de dados](configure.md) com o serviço do [Adobe Target](configure.md#target).

Depois de criar a sequência de dados, edite o serviço [Adobe Target](configure.md#target) que você adicionou e use a seção **[!UICONTROL Property Token Overrides]** para adicionar as substituições da sequência de dados desejadas, conforme mostrado na imagem abaixo. Adicione um token de propriedade por linha.

![Captura de tela da interface das sequências de dados mostrando as configurações do serviço do Adobe Target, com as substituições de token de propriedade realçadas.](assets/overrides/override-target.png)

Depois de adicionar as substituições desejadas, salve as configurações da sequência de dados.

Agora as substituições de sequência de dados do Adobe Target devem estar configuradas. Agora você pode [enviar as substituições para a Edge Network por meio do Web SDK ou do Mobile SDK](#send-overrides).

### Substituições de sequência de dados para o Adobe Analytics {#analytics-overrides}

Para configurar substituições para uma sequência de dados do Adobe Analytics, primeiro você deve criar uma sequência de dados do [Adobe Analytics](configure.md#analytics). Siga as instruções para [configurar uma sequência de dados](configure.md) com o serviço do [Adobe Analytics](configure.md#analytics).

Depois de criar a sequência de dados, edite o serviço [Adobe Analytics](configure.md#target) que você adicionou e use a seção **[!UICONTROL Report Suite Overrides]** para adicionar as substituições da sequência de dados desejadas, conforme mostrado na imagem abaixo.

Selecione **[!UICONTROL Show Batch Mode]** para habilitar a edição em lote de substituições do conjunto de relatórios. É possível copiar e colar uma lista de substituições de conjunto de relatórios, inserindo um conjunto de relatórios por linha.

![Captura de tela da interface das sequência de dados mostrando as configurações do serviço do Adobe Analytics, com as substituições de conjunto de relatórios realçadas.](assets/overrides/override-analytics.png)

Depois de adicionar as substituições desejadas, salve as configurações da sequência de dados.

Agora as substituições de sequência de dados do Adobe Analytics devem estar configuradas. Agora você pode [enviar as substituições para a Edge Network por meio do Web SDK ou do Mobile SDK](#send-overrides).

### Substituições de sequência de dados para conjuntos de dados de eventos da Experience Platform {#event-dataset-overrides}

Para configurar substituições de sequência de dados para conjuntos de dados de evento da Experience Platform, primeiro você deve criar uma sequência de dados da [Adobe Experience Platform](configure.md#aep). Siga as instruções para [configurar uma sequência de dados](configure.md) com o serviço da [Adobe Experience Platform](configure.md#aep).

Depois de criar a sequência de dados, edite o serviço [Adobe Experience Platform](configure.md#aep) que você adicionou e selecione a opção **[!UICONTROL Add Event Dataset]** para adicionar um ou mais conjuntos de dados de evento de substituição, conforme mostrado na imagem abaixo.

![Captura de tela da interface das sequências de dados mostrando as configurações do serviço da Adobe Experience Platform, com as substituições de conjunto de dados de evento realçadas.](assets/overrides/override-aep.png)

Depois de adicionar as substituições desejadas, salve as configurações da sequência de dados.

Agora as substituições de sequência de dados da Adobe Experience Platform devem estar configuradas. Agora você pode [enviar as substituições para a Edge Network por meio do Web SDK ou do Mobile SDK](#send-overrides).

### Substituições de sequência de dados para containers de sincronização de ID de terceiros {#container-overrides}

Para configurar substituições de sequência de dados para containers de sincronização de ID de terceiros, primeiro você deve criar uma sequência de dados. Siga as instruções para [configurar uma sequência de dados](configure.md).

Depois de criar a sequência de dados, vá para **[!UICONTROL Advanced Options]** e habilite a opção **[!UICONTROL Third Party ID Sync]**.

Em seguida, use a seção **[!UICONTROL Container ID Overrides]** para adicionar as IDs de contêiner nas quais você deseja substituir a configuração padrão, como mostrado na imagem abaixo.

>[!IMPORTANT]
>
>As IDs de container devem ser valores numéricos, como `1234567`, e não strings, como `"1234567"`. Um erro será exibido se você enviar uma string por meio do SDK da Web como uma substituição de ID de container.

![Captura de tela da interface das sequências de dados mostrando as configurações da sequência de dados, com as substituições do container de sincronização de ID de terceiros realçadas.](assets/overrides/override-container.png)

Depois de adicionar as substituições desejadas, salve as configurações da sequência de dados.

Agora as substituições do container de sincronização de ID devem estar configuradas. Agora você pode [enviar as substituições para a Edge Network por meio do Web SDK ou do Mobile SDK](#send-overrides).

## Enviar as sobreposições para a Edge Network {#send-overrides}

Depois de configurar as substituições de fluxo de dados na interface da Coleção de dados, você pode enviar as substituições para a Edge Network por meio da Web SDK ou do Mobile SDK.

* **Web SDK**: consulte [substituições da configuração da sequência de dados](/help/collection/js/commands/configure/edgeconfigoverrides.md) para obter exemplos de código de biblioteca do JavaScript.
* **SDK Móvel**: você pode enviar substituições de ID de sequência de dados usando a [API sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) ou usando as [Regras](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

## Exemplo de conteúdo {#payload-example}

Os exemplos acima geram uma carga de [!DNL Edge Network] similar à abaixo.

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
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
  "events": [  ]
}
```
