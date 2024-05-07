---
title: Configurar substituições de sequência de dados
description: Saiba como configurar substituições de sequência de dados na interface do usuário de sequências de dados e ativá-las por meio do SDK da Web ou do SDK móvel.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 17ed5f3c14d4787352f72d3d7721cbb6416d533e
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 57%

---

# Configurar substituições de sequência de dados

As substituições de sequência de dados permitem definir configurações adicionais para as sequências de dados, que são transmitidas para o Edge Network por meio do SDK da Web ou do SDK móvel.

Isso ajuda a acionar comportamentos de sequência de dados diferentes dos padrão, sem criar uma sequência de dados ou modificar as configurações existentes.

A substituição da configuração da sequência de dados é um processo de duas etapas:

1. Primeiro, você deve definir a substituição da configuração do fluxo de dados na [página de configuração do fluxo de dados](configure.md).
2. Em seguida, você deve enviar as sobreposições para o Edge Network de uma das seguintes maneiras:
   * Por meio da `sendEvent` ou `configure` [SDK da Web](#send-overrides) comandos.
   * Por meio do SDK da Web [extensão de tag](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Por meio do SDK móvel [sendEvent](#send-overrides) API ou usando [Regras](#send-overrides).

Este artigo explica o processo completo para criar cada tipo de substituição de configuração de sequência de dados compatível.

>[!IMPORTANT]
>
>As substituições de fluxo de dados são compatíveis somente com [SDK da Web](../web-sdk/home.md) e [SDK móvel](https://developer.adobe.com/client-sdks/home/) integrações. [API do servidor](../server-api/overview.md) atualmente, as integrações não aceitam substituições de fluxo de dados.
><br>
>As substituições de sequência de dados devem ser usadas quando você precisa que dados diferentes sejam enviados para sequências de dados diferentes. Não use substituições de fluxo de dados para casos de uso de personalização ou dados de consentimento.

## Casos de uso {#use-cases}

Para melhorar o entendimento sobre como e quando usar substituições de sequência de dados, veja alguns casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse recurso.

**Coleta de dados de várias regiões**

Uma empresa tem sites ou subdomínios diferentes para países diferentes nos quais opera. Ela [configurou](configure.md) sequências de dados separadas com conjuntos de relatórios específicos do Analytics, tokens de propriedade do Adobe Target específicos de um país, esquemas específicos de um país, conjuntos de dados, configurações do Journey Optimizer e assim por diante. A empresa também tem um conjunto global de configurações onde agrega todos os dados específicos de um país.

Ao usar substituições de sequência de dados, a empresa pode alternar dinamicamente o fluxo dos dados para sequências de dados diferentes, em vez do comportamento padrão de enviar dados para uma sequência de dados.

Um caso de uso comum pode ser o envio de dados para um fluxo de dados específico de país e também para um fluxo de dados global em que os clientes executam uma ação importante, como fazer um pedido ou atualizar o perfil do usuário.

**Diferenciação de perfis e identidades para diferentes unidades de negócios**

Uma empresa com várias unidades de negócios deseja usar várias sandboxes Experience Platform para armazenar dados específicos de cada unidade de negócios.

Em vez de enviar dados para uma sequência de dados padrão, a empresa pode usar substituições de sequência de dados para garantir que cada unidade de negócios tenha sua própria sequência de dados para receber dados.

## Configurar substituições na interface das sequências de dados {#configure-overrides}

As substituições de configuração de sequência de dados permitem modificar as seguintes configurações de sequência de dados:

* Conjuntos de dados de eventos da Experience Platform
* Tokens de propriedade do Adobe Target
* Containers de sincronização de ID do Audience Manager
* Conjuntos de relatórios do Adobe Analytics

### Substituições de sequência de dados para o Adobe Target {#target-overrides}

Para configurar substituições para uma sequência de dados do Adobe Target, primeiro você deve criar uma sequência de dados do Adobe Target. Siga as instruções para [configurar uma sequência de dados](configure.md) com o serviço do [Adobe Target](configure.md#target).

Depois de criar o fluxo de dados, edite o [Adobe Target](configure.md#target) serviço que você adicionou e usar o **[!UICONTROL Substituições do token de propriedade]** para adicionar as substituições de fluxo de dados desejadas, conforme mostrado na imagem abaixo. Adicione um token de propriedade por linha.

![Captura de tela da interface das sequências de dados mostrando as configurações do serviço do Adobe Target, com as substituições de token de propriedade realçadas.](assets/overrides/override-target.png)

Depois de adicionar as substituições desejadas, salve as configurações da sequência de dados.

Agora as substituições de sequência de dados do Adobe Target devem estar configuradas. Agora é possível [enviar as substituições para o Edge Network pelo SDK da Web ou SDK móvel](#send-overrides).

### Substituições de sequência de dados para o Adobe Analytics {#analytics-overrides}

Para configurar substituições para uma sequência de dados do Adobe Analytics, primeiro você deve criar uma sequência de dados do [Adobe Analytics](configure.md#analytics). Siga as instruções para [configurar uma sequência de dados](configure.md) com o serviço do [Adobe Analytics](configure.md#analytics).

Depois de criar o fluxo de dados, edite o [Adobe Analytics](configure.md#target) serviço que você adicionou e usar o **[!UICONTROL Substituições do conjunto de relatórios]** para adicionar as substituições de fluxo de dados desejadas, conforme mostrado na imagem abaixo.

Selecione **[!UICONTROL Mostrar modo de lote]** para habilitar a edição em lote de substituições de conjunto de relatórios. É possível copiar e colar uma lista de substituições de conjunto de relatórios, inserindo um conjunto de relatórios por linha.

![Captura de tela da interface das sequência de dados mostrando as configurações do serviço do Adobe Analytics, com as substituições de conjunto de relatórios realçadas.](assets/overrides/override-analytics.png)

Depois de adicionar as substituições desejadas, salve as configurações da sequência de dados.

Agora as substituições de sequência de dados do Adobe Analytics devem estar configuradas. Agora é possível [enviar as substituições para o Edge Network pelo SDK da Web ou SDK móvel](#send-overrides).

### Substituições de sequência de dados para conjuntos de dados de eventos da Experience Platform {#event-dataset-overrides}

Para configurar substituições de sequência de dados para conjuntos de dados de evento da Experience Platform, primeiro você deve criar uma sequência de dados da [Adobe Experience Platform](configure.md#aep). Siga as instruções para [configurar uma sequência de dados](configure.md) com o serviço da [Adobe Experience Platform](configure.md#aep).

Depois de criar o fluxo de dados, edite o [Adobe Experience Platform](configure.md#aep) serviço que você adicionou e selecione o **[!UICONTROL Adicionar conjunto de dados do evento]** opção para adicionar um ou mais conjuntos de dados do evento de substituição, conforme mostrado na imagem abaixo.

![Captura de tela da interface das sequências de dados mostrando as configurações do serviço da Adobe Experience Platform, com as substituições de conjunto de dados de evento realçadas.](assets/overrides/override-aep.png)

Depois de adicionar as substituições desejadas, salve as configurações da sequência de dados.

Agora as substituições de sequência de dados da Adobe Experience Platform devem estar configuradas. Agora é possível [enviar as substituições para o Edge Network pelo SDK da Web ou SDK móvel](#send-overrides).

### Substituições de sequência de dados para containers de sincronização de ID de terceiros {#container-overrides}

Para configurar substituições de sequência de dados para containers de sincronização de ID de terceiros, primeiro você deve criar uma sequência de dados. Siga as instruções para [configurar uma sequência de dados](configure.md).

Depois de criar a sequência de dados, acesse **[!UICONTROL Opções avançadas]** e habilite a opção **[!UICONTROL Sincronização de ID de terceiros]**.

Em seguida, use a seção **[!UICONTROL Substituições de ID de container]** para adicionar as IDs de container que você deseja usar para substituir a configuração padrão, conforme mostrado na imagem abaixo.

>[!IMPORTANT]
>
>As IDs de container devem ser valores numéricos, como `1234567`, e não strings, como `"1234567"`. Um erro será exibido se você enviar uma string por meio do SDK da Web como uma substituição de ID de container.

![Captura de tela da interface das sequências de dados mostrando as configurações da sequência de dados, com as substituições do container de sincronização de ID de terceiros realçadas.](assets/overrides/override-container.png)

Depois de adicionar as substituições desejadas, salve as configurações da sequência de dados.

Agora as substituições do container de sincronização de ID devem estar configuradas. Agora é possível [enviar as substituições para o Edge Network pelo SDK da Web ou SDK móvel](#send-overrides).

## Enviar as sobreposições para o Edge Network {#send-overrides}

Depois de configurar as substituições de fluxo de dados na interface da Coleção de dados, você pode enviar as substituições para o Edge Network por meio do SDK da Web ou do SDK móvel.

* **SDK da Web**: Consulte [substituições de configuração da sequência de dados](../web-sdk/commands/datastream-overrides.md#library) para obter instruções sobre a extensão da tag e exemplos de código da biblioteca JavaScript.
* **SDK móvel**: é possível enviar substituições da ID do fluxo de dados usando o [API sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) ou usando [Regras](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

## Exemplo de conteúdo {#payload-example}

Os exemplos acima geram uma [!DNL Edge Network] carga semelhante à abaixo.

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
