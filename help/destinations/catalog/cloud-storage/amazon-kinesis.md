---
keywords: Amazon Kinesis;destino cinesis;cinesis
title: Destino da conexão Amazon Kinesis
description: Crie uma conexão de saída em tempo real com seu armazenamento Amazon Kinesis para transmitir dados da Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 2%

---


# (Beta) [!DNL Amazon Kinesis] conexão

>[!IMPORTANT]
>
>O destino [!DNL Amazon Kinesis] na Plataforma está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

O serviço [!DNL Kinesis Data Streams] de [!DNL Amazon Web Services] permite coletar e processar grandes fluxos de registros de dados em tempo real.

Você pode criar uma conexão de saída em tempo real com seu armazenamento [!DNL Amazon Kinesis] para transmitir dados do Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Amazon Kinesis], consulte a [documentação da Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Para se conectar a [!DNL Amazon Kinesis] usando chamadas de API, consulte o [tutorial da API de destino de transmissão](../../api/streaming-destinations.md).
* Para conectar-se a [!DNL Amazon Kinesis] usando a interface do usuário da plataforma, consulte as seções abaixo.

![Amazon Kinesis na interface do usuário](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casos de uso {#use-cases}

Ao usar destinos de streaming como [!DNL Amazon Kinesis], você pode facilmente alimentar eventos de segmentação de alto valor e atributos de perfil associados em seus sistemas de escolha.

Por exemplo, um prospecto baixou um white paper que os qualifica em um segmento de &quot;alta propensão para converter&quot;. Ao mapear o segmento no qual o prospecto cai para o destino [!DNL Amazon Kinesis], você receberá esse evento em [!DNL Amazon Kinesis]. Lá, você pode usar uma abordagem faça-você-mesmo e descrever a lógica comercial sobre o evento, pois você acha que funcionaria melhor com seus sistemas de TI corporativos.

## Tipo de exportação {#export-type}

**Baseado**  em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [ da ativação de ](../../ui/activate-destinations.md#select-attributes)destino.

## Destino do Connect {#connect-destination}

Consulte [Fluxo de trabalho de destinos de armazenamentos na nuvem ](./workflow.md)para obter instruções sobre como se conectar aos destinos de armazenamentos na nuvem, incluindo aqueles suportados por [!DNL Amazon].

Para destinos [!DNL Amazon Kinesis], insira as seguintes informações no fluxo de trabalho de criação de destino:

### Na etapa Autenticação {#authentication-step}

* **[!DNL Amazon Web Services]chave de acesso e chave** secreta: Em  [!DNL Amazon Web Services], gere um  `access key - secret access key` par para conceder acesso à Plataforma à sua  [!DNL Amazon Kinesis] conta. Saiba mais na [documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **região**: Indica para qual  [!DNL Amazon Web Services] região transmitir dados.

![Campos de entrada na etapa da conta](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

### Na etapa de configuração {#setup-step}

* **Nome**: Forneça um nome para a sua conexão com  [!DNL Amazon Kinesis]
* **Descrição**: Forneça uma descrição para a sua conexão com  [!DNL Amazon Kinesis].
* **fluxo**: Forneça o nome de um fluxo de dados existente em sua  [!DNL Amazon Kinesis] conta. A plataforma exportará dados para esse fluxo.

![Campos de entrada na etapa de autenticação](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Dados exportados {#exported-data}

Seus dados exportados [!DNL Experience Platform] chegam em [!DNL Amazon Kinesis] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de uma audiência que se qualificou para um determinado segmento e saiu de outro. As identidades para este prospecto são ECID e email.

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
>* [Conecte-se ao Amazon Kinesis e ative dados usando chamadas de API](../../api/streaming-destinations.md)
>* [Destino dos Hubs de Evento do Azure](./azure-event-hubs.md)
>* [Tipos de destino e categorias](../../destination-types.md)

