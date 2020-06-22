---
title: Destino da Amazon Kinesis
seo-title: Destino da Amazon Kinesis
description: Crie uma conexão de saída em tempo real com seu armazenamento Amazon Kinesis para transmitir dados do Adobe Experience Platform.
seo-description: Crie uma conexão de saída em tempo real com seu armazenamento Amazon Kinesis para transmitir dados do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: e93bfc028d5e23c3add55677c4003ca549a902c6
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 2%

---


# (Beta) Destino da Amazon Kinesis


>[!IMPORTANT]
>
>O [!DNL Amazon Kinesis] destino no Adobe Real-time CDP está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

O [!DNL Kinesis Data Streams] serviço da Amazon Web Services permite coletar e processar grandes fluxos de registros de dados em tempo real.

Você pode criar uma conexão de saída em tempo real com seu [!DNL Amazon Kinesis] armazenamento para transmitir dados do Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Amazon Kinesis], consulte a documentação [da](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)Amazon.
* Para conectar-se a [!DNL Amazon Kinesis] chamadas de API, consulte o tutorial [da API de destinos de](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)transmissão contínua.
* Para conectar-se [!DNL Amazon Kinesis] usando a interface do usuário CDP em tempo real da Adobe, consulte as seções abaixo.

![Amazon Kinesis na interface do usuário](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Casos de uso {#use-cases}

Ao usar destinos de streaming como o Amazon Kinesis, você pode facilmente alimentar eventos de segmentação de alto valor e atributos associados ao perfil em seus sistemas de escolha.

Por exemplo, um prospecto baixou um white paper que os qualifica em um segmento de &quot;alta propensão para converter&quot;. Ao mapear o segmento em que o prospecto cai para o destino da Amazônia Kinesis, você receberia esse evento na Amazon Kinesis. Lá, você pode usar uma abordagem faça-você-mesmo e descrever a lógica comercial sobre o evento, pois você acha que funcionaria melhor com seus sistemas de TI corporativos.

## Destino do Connect {#connect-destination}

Consulte Fluxo de trabalho de destinos do armazenamento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obter instruções sobre como se conectar aos destinos do armazenamento na nuvem, incluindo aqueles suportados por [!DNL Amazon].

Para [!DNL Amazon Kinesis] destinos, insira as seguintes informações no fluxo de trabalho de criação de destino:

### Na etapa Autenticação {#authentication-step}

* **Chave de acesso e chave** secreta dos Serviços Web da Amazon: Em [!DNL Amazon Web Services], gere uma chave de acesso - par de chaves de acesso secreto para conceder à Adobe o acesso CDP em tempo real à sua [!DNL Amazon Kinesis] conta. Saiba mais na documentação [dos Serviços da Web da](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon.
* **região**: Indica em qual [!DNL Amazon Web Services] região os dados serão transmitidos.

![Campos de entrada na etapa da conta](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### Na etapa de configuração {#setup-step}

* **Nome**: Forneça um nome para a sua conexão com [!DNL Amazon Kinesis]
* **Descrição**: Forneça uma descrição para a sua conexão com [!DNL Amazon Kinesis].
* **fluxo**: Forneça o nome de um fluxo de dados existente em sua [!DNL Amazon Kinesis] conta. A CDP em tempo real da Adobe exportará dados para esse fluxo.

![Campos de entrada na etapa de autenticação](/help/rtcdp/destinations/assets/aws-kinesis-setup-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Dados exportados {#exported-data}

Seus dados de Experience Platform exportados chegam [!DNL Amazon Kinesis] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de uma audiência que se qualificou para um determinado segmento e saiu de outro. As identidades para este prospecto são ECID e email.

```
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
>* [Conecte-se ao Amazon Kinesis e ative dados usando chamadas de API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destino dos Hubs de Evento do Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Tipos de destino e categorias](/help/rtcdp/destinations/destination-types.md)

