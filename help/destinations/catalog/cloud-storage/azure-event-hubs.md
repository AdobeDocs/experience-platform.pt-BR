---
keywords: Destino do hub de eventos do Azure; hub de eventos do azure; azure eventhub
title: (Beta) Conexão de Hubs de Eventos do Azure
description: Crie uma conexão de saída em tempo real com o armazenamento dos Hubs de Eventos do Azure para fazer o stream de dados do Experience Platform.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 2%

---


# (Beta) [!DNL Azure Event Hubs] conexão

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

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

## Conectar destino {#connect-destination}

Consulte [Fluxo de trabalho de destinos de armazenamento na nuvem ](./workflow.md)para obter instruções sobre como se conectar aos destinos de armazenamento na nuvem, incluindo [!DNL Azure Event Hubs].

Para destinos [!DNL Azure Event Hubs], insira as seguintes informações no workflow criar destino:

## Etapa de autenticação {#authentication-step}

* **[!UICONTROL SAS Key Name]** e  **[!UICONTROL SAS Key]**: Preencha o nome e a chave da chave SAS. Saiba mais sobre como autenticar para [!DNL Azure Event Hubs] com chaves SAS na [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Preencha seu  [!DNL Azure Event Hubs] namespace. Saiba mais sobre [!DNL Azure Event Hubs] namespaces na [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Entrada necessária na etapa de autenticação](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

## Etapa de configuração {#setup-step}

* **[!UICONTROL Name]**: Preencha um nome para a conexão com o  [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Forneça uma descrição da conexão.  Exemplos: &quot;Clientes Premium&quot;, &quot;Masculino interessado em cozinha&quot;.
* **[!UICONTROL eventHubName]**: Forneça um nome para o fluxo para o  [!DNL Azure Event Hubs] destino.
* **[!UICONTROL Marketing actions]**: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Governança de dados no Adobe Experience Platform](../../../data-governance/policies/overview.md) . Para obter informações sobre as ações de marketing individuais definidas pelo Adobe, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Dados necessários na etapa de configuração](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

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
>* [AWS Kinesis destination](./amazon-kinesis.md)
>* [Tipos e categorias de destino](../../destination-types.md)