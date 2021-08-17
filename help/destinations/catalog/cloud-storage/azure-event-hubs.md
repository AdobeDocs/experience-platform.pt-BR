---
keywords: Destino do hub de eventos do Azure; hub de eventos do azure; azure eventhub
title: (Beta) !Hubs de Eventos do Azure]
description: Crie uma conexão de saída em tempo real com o armazenamento do !DNL Azure Event Hubs] para fazer o stream de dados do Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# (Beta) [!DNL Azure Event Hubs] conexão

## Visão geral {#overview}

>[!IMPORTANT]
>
>O destino [!DNL Azure Event Hubs] na Plataforma está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

[!DNL Azure Event Hubs] O é uma grande plataforma de transmissão de dados e um serviço de assimilação de eventos. Ele pode receber e processar milhões de eventos por segundo. Os dados enviados para um hub de eventos podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/agrupamento.

Você pode criar uma conexão de saída em tempo real com seu armazenamento [!DNL Azure Event Hubs] para transmitir dados do Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Azure Event Hubs], consulte a [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para se conectar a [!DNL Azure Event Hubs] programaticamente, consulte o [Tutorial da API de destinos de transmissão](../../api/streaming-destinations.md).
* Para se conectar a [!DNL Azure Event Hubs] usando a interface do usuário da Plataforma, consulte as seções abaixo.

![AWS Kinesis na interface do usuário](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casos de uso {#use-cases}

Ao usar destinos de transmissão como [!DNL Azure Event Hubs], você pode facilmente alimentar eventos de segmentação de alto valor e atributos de perfil associados em seus sistemas de escolha.

Por exemplo, um prospecto baixou um white-paper que os qualifica em um segmento de &quot;alta propensão à conversão&quot;. Ao mapear o segmento no qual o prospecto se enquadra no destino [!DNL Azure Event Hubs], você receberia esse evento em [!DNL Azure Event Hubs]. Lá, você pode empregar uma abordagem faça você mesmo e descrever a lógica de negócios sobre o evento, pois acha que funcionaria melhor com os sistemas de TI de sua empresa.

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação do  [público-alvo](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Chave SAS]** e Chave  **[!UICONTROL SAS]**: Preencha o nome e a chave da chave SAS. Saiba mais sobre como autenticar para [!DNL Azure Event Hubs] com chaves SAS na [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Preencha seu  [!DNL Azure Event Hubs] namespace. Saiba mais sobre [!DNL Azure Event Hubs] namespaces na [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nome]**: Preencha um nome para a conexão com o  [!DNL Azure Event Hubs].
* **[!UICONTROL Descrição]**: Forneça uma descrição da conexão.  Exemplos: &quot;Clientes Premium&quot;, &quot;Masculino interessado em cozinha&quot;.
* **[!UICONTROL eventHubName]**: Forneça um nome para o fluxo para o  [!DNL Azure Event Hubs] destino.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar dados do público-alvo para exportar perfis de fluxo contínuo](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

## Dados exportados {#exported-data}

Seus dados [!DNL Experience Platform] exportados chegam em [!DNL Azure Event Hubs] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de um público que se qualificou para um determinado segmento e saiu de outro. As identidades desse prospecto são ECID e email.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```


>[!MORELIKETHIS]
>
>* [Conecte-se aos Hubs de Eventos do Azure e ative dados usando a API do Serviço de Fluxo](../../api/streaming-destinations.md)
* [AWS Kinesis destination](./amazon-kinesis.md)
* [Tipos e categorias de destino](../../destination-types.md)

