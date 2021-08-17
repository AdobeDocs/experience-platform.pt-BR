---
keywords: Amazon Kinesis;destino cinesis;cinesis
title: Conexão Amazon Kinesis
description: Crie uma conexão de saída em tempo real com o armazenamento do Amazon Kinesis para fazer o stream de dados do Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# (Beta) [!DNL Amazon Kinesis] conexão

## Visão geral {#overview}

>[!IMPORTANT]
>
>O destino [!DNL Amazon Kinesis] na Plataforma está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

O serviço [!DNL Kinesis Data Streams] de [!DNL Amazon Web Services] permite coletar e processar grandes fluxos de registros de dados em tempo real.

Você pode criar uma conexão de saída em tempo real com seu armazenamento [!DNL Amazon Kinesis] para transmitir dados do Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Amazon Kinesis], consulte a [documentação do Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Para se conectar a [!DNL Amazon Kinesis] programaticamente, consulte o [Tutorial da API de destinos de transmissão](../../api/streaming-destinations.md).
* Para se conectar a [!DNL Amazon Kinesis] usando a interface do usuário da Plataforma, consulte as seções abaixo.

![Amazon Kinesis na interface do usuário](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casos de uso {#use-cases}

Ao usar destinos de transmissão como [!DNL Amazon Kinesis], você pode facilmente alimentar eventos de segmentação de alto valor e atributos de perfil associados em seus sistemas de escolha.

Por exemplo, um prospecto baixou um white-paper que os qualifica em um segmento de &quot;alta propensão à conversão&quot;. Ao mapear o segmento no qual o prospecto se enquadra no destino [!DNL Amazon Kinesis], você receberia esse evento em [!DNL Amazon Kinesis]. Lá, você pode empregar uma abordagem faça você mesmo e descrever a lógica de negócios sobre o evento, pois acha que funcionaria melhor com os sistemas de TI de sua empresa.

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

## Permissões [!DNL Amazon Kinesis] necessárias {#required-kinesis-permission}

Para se conectar e exportar dados com êxito para seus fluxos [!DNL Amazon Kinesis], o Experience Platform precisa de permissões para as seguintes ações:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Essas permissões são organizadas por meio do console [!DNL Kinesis] e são verificadas pela Platform depois que você configura o destino do Kinesis na interface do usuário da plataforma.

O exemplo abaixo exibe os direitos mínimos de acesso necessários para exportar dados com êxito para um destino [!DNL Kinesis].

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `kinesis:ListStreams` | Uma ação que lista seus fluxos de dados do Amazon Kinesis. |
| `kinesis:PutRecord` | Uma ação que grava um único registro de dados em um fluxo de dados do Kinesis. |
| `kinesis:PutRecords` | Uma ação que grava vários registros de dados em um fluxo de dados do Kinesis em uma única chamada. |

Para obter mais informações sobre como controlar o acesso para [!DNL Kinesis] fluxos de dados, leia o seguinte [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!DNL Amazon Web Services]chave de acesso e chave** secreta: No  [!DNL Amazon Web Services], gere um  `access key - secret access key` par para conceder à Platform acesso à sua  [!DNL Amazon Kinesis] conta. Saiba mais na [documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **região**: Indique em qual  [!DNL Amazon Web Services] região os dados serão transmitidos.
* **Nome**: Forneça um nome para a conexão com o  [!DNL Amazon Kinesis]
* **Descrição**: Forneça uma descrição para a conexão com o  [!DNL Amazon Kinesis].
* **fluxo**: Forneça o nome de um fluxo de dados existente em sua  [!DNL Amazon Kinesis] conta. A Platform exportará dados para esse fluxo.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Ativar segmentos para este destino {#activate}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para destinos.

## Dados exportados {#exported-data}

Seus dados [!DNL Experience Platform] exportados chegam em [!DNL Amazon Kinesis] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de um público que se qualificou para um determinado segmento e saiu de outro. As identidades desse prospecto são ECID e email.

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
>* [Conecte-se ao Amazon Kinesis e ative dados usando a API do Serviço de Fluxo](../../api/streaming-destinations.md)
* [Destino de Hubs de Eventos do Azure](./azure-event-hubs.md)
* [Tipos e categorias de destino](../../destination-types.md)

