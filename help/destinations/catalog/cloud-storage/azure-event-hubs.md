---
keywords: destino do hub do evento do Azure;hub do evento do azure;azure eventhub
title: (Beta) Conexão de Hubs de Evento do Azure
description: Crie uma conexão de saída em tempo real com seu armazenamento de Hubs de Evento do Azure para transmitir dados do Experience Platform.
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 2%

---


# (Beta) [!DNL Azure Event Hubs] conexão

>[!IMPORTANT]
>
>O destino [!DNL Azure Event Hubs] na Plataforma está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

[!DNL Azure Event Hubs] é uma grande plataforma de transmissão de dados e um serviço de ingestão de eventos. Pode receber e processar milhões de eventos por segundo. Os dados enviados para um hub de evento podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de agrupamento/armazenamento.

Você pode criar uma conexão de saída em tempo real com seu armazenamento [!DNL Azure Event Hubs] para transmitir dados do Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Azure Event Hubs], consulte a [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para se conectar a [!DNL Azure Event Hubs] usando chamadas de API, consulte o [tutorial da API de destino de transmissão](../../api/streaming-destinations.md).
* Para conectar-se a [!DNL Azure Event Hubs] usando a interface do usuário da plataforma, consulte as seções abaixo.

![Kinesis AWS na interface do usuário](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casos de uso {#use-cases}

Ao usar destinos de streaming como [!DNL Azure Event Hubs], você pode facilmente alimentar eventos de segmentação de alto valor e atributos de perfil associados em seus sistemas de escolha.

Por exemplo, um prospecto baixou um white paper que os qualifica em um segmento de &quot;alta propensão para converter&quot;. Ao mapear o segmento no qual o prospecto cai para o destino [!DNL Azure Event Hubs], você receberá esse evento em [!DNL Azure Event Hubs]. Lá, você pode usar uma abordagem faça-você-mesmo e descrever a lógica comercial sobre o evento, pois você acha que funcionaria melhor com seus sistemas de TI corporativos.

## Tipo de exportação {#export-type}

**Baseado**  em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [ da ativação de ](../../ui/activate-destinations.md#select-attributes)destino.

## Destino do Connect {#connect-destination}

Consulte [Fluxo de trabalho de destinos do armazenamento da nuvem ](./workflow.md)para obter instruções sobre como se conectar aos destinos do armazenamento da nuvem, incluindo [!DNL Azure Event Hubs].

Para destinos [!DNL Azure Event Hubs], insira as seguintes informações no fluxo de trabalho de criação de destino:

### Na etapa Autenticação {#authentication-step}

* **[!UICONTROL Nome da chave SAS]** e chave **** SAS: Preencha o nome e a chave da sua chave SAS. Saiba mais sobre como autenticar em [!DNL Azure Event Hubs] com chaves SAS na [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Preencha a sua  [!DNL Azure Event Hubs] namespace. Saiba mais sobre [!DNL Azure Event Hubs] namespaces na [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Entrada necessária na etapa de autenticação](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

### Na etapa de configuração {#setup-step}

* **[!UICONTROL Nome]**: Preencha um nome para a conexão com  [!DNL Azure Event Hubs].
* **[!UICONTROL Descrição]**: Forneça uma descrição da conexão.  Exemplos: &quot;Clientes premium&quot;, &quot;Masculino interessado em cozinha&quot;.
* **[!UICONTROL eventHubName]**: Forneça um nome para o fluxo para o seu  [!DNL Azure Event Hubs] destino.
* **[!UICONTROL Ações]** de marketing: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. É possível selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Data Governance no Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obter informações sobre as ações de marketing individuais definidas pelo Adobe, consulte [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Dados necessários na etapa de configuração](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Dados exportados {#exported-data}

Seus dados exportados [!DNL Experience Platform] chegam em [!DNL Azure Event Hubs] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de uma audiência que se qualificou para um determinado segmento e saiu de outro. As identidades para este prospecto são ECID e email.

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
>* [Conecte-se aos Hubs de Evento do Azure e ative dados usando chamadas de API](../../api/streaming-destinations.md)
>* [Destino AWS Kinesis](./amazon-kinesis.md)
>* [Tipos de destino e categorias](../../destination-types.md)