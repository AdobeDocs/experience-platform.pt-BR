---
keywords: Azure event hub destination;azure event hub;azure eventhub
title: (Beta) Destino dos Hubs de Eventos do Azure
seo-title: (Beta) Destino dos Hubs de Eventos do Azure
description: Crie uma conexão de saída em tempo real com seu armazenamento de Hubs de Evento do Azure para transmitir dados do Experience Platform.
seo-description: Crie uma conexão de saída em tempo real com seu armazenamento de Hubs de Evento do Azure para transmitir dados do Experience Platform.
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---


# (Beta) [!DNL Azure Event Hubs] destino

>[!IMPORTANT]
>
>O [!DNL Azure Event Hubs] destino no CDP em tempo real do Adobe está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

[!DNL Azure Event Hubs] é uma grande plataforma de transmissão de dados e um serviço de ingestão de eventos. Pode receber e processar milhões de eventos por segundo. Os dados enviados para um hub de evento podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de agrupamento/armazenamento.

Você pode criar uma conexão de saída em tempo real com seu [!DNL Azure Event Hubs] armazenamento para transmitir dados da Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Azure Event Hubs], consulte a documentação [da](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)Microsoft.
* Para conectar-se a [!DNL Azure Event Hubs] chamadas de API, consulte o tutorial [da API de destinos de](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)transmissão contínua.
* Para se conectar ao [!DNL Azure Event Hubs] uso da interface de usuário CDP em tempo real do Adobe, consulte as seções abaixo.

![Kinesis AWS na interface do usuário](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Casos de uso {#use-cases}

Ao usar destinos de streaming como [!DNL Azure Event Hubs], você pode facilmente alimentar eventos de segmentação de alto valor e atributos de perfil associados em seus sistemas preferidos.

Por exemplo, um prospecto baixou um white paper que os qualifica em um segmento de &quot;alta propensão para converter&quot;. Ao mapear o segmento no qual o prospecto cai para o [!DNL Azure Event Hubs] destino, você receberá esse evento [!DNL Azure Event Hubs]. Lá, você pode usar uma abordagem faça-você-mesmo e descrever a lógica comercial sobre o evento, pois você acha que funcionaria melhor com seus sistemas de TI corporativos.

## Destino do Connect {#connect-destination}

Consulte Fluxo de trabalho de destinos do armazenamento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obter instruções sobre como se conectar aos destinos do armazenamento na nuvem, incluindo [!DNL Azure Event Hubs].

Para [!DNL Azure Event Hubs] destinos, insira as seguintes informações no fluxo de trabalho de criação de destino:

### Na etapa Autenticação {#authentication-step}

* **[!UICONTROL Nome]** da chave SAS e chave **** SAS: Preencha o nome e a chave da sua chave SAS. Saiba mais sobre como autenticar [!DNL Azure Event Hubs] com chaves SAS na documentação [da](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Namespace]**: Preencha a sua [!DNL Azure Event Hubs] namespace. Saiba mais sobre [!DNL Azure Event Hubs] as namespaces na documentação [da](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Entrada necessária na etapa de autenticação](/help/rtcdp/destinations/assets/event-hubs-authentication.png)

### Na etapa de configuração {#setup-step}

* **[!UICONTROL Nome]**: Preencha um nome para a conexão com [!DNL Azure Event Hubs].
* **[!UICONTROL Descrição]**: Forneça uma descrição da conexão.  Exemplos: &quot;Clientes premium&quot;, &quot;Masculino interessado em cozinha&quot;.
* **[!UICONTROL eventHubName]**: Forneça um nome para o fluxo para o seu [!DNL Azure Event Hubs] destino.

![Dados necessários na etapa de configuração](/help/rtcdp/destinations/assets/event-hubs-setup-step.png)

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.


## Dados exportados {#exported-data}

Seus [!DNL Experience Platform] dados exportados chegam [!DNL Azure Event Hubs] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de uma audiência que se qualificou para um determinado segmento e saiu de outro. As identidades para este prospecto são ECID e email.

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
>* [Conecte-se aos Hubs de Evento do Azure e ative dados usando chamadas de API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destino AWS Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Tipos de destino e categorias](/help/rtcdp/destinations/destination-types.md)