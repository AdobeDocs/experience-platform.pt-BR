---
keywords: Amazon Kinesis;destino cinesis;cinesis
title: Conexão Amazon Kinesis
description: Crie uma conexão de saída em tempo real com o armazenamento do Amazon Kinesis para fazer o stream de dados do Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: f7f3bc229ddad046dca5ea8d2889942fc9cb2cab
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---

# (Beta) [!DNL Amazon Kinesis] conexão

## Visão geral {#overview}

>[!IMPORTANT]
>
>O [!DNL Amazon Kinesis] no Platform está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

O [!DNL Kinesis Data Streams] serviço por [!DNL Amazon Web Services] O permite coletar e processar grandes fluxos de registros de dados em tempo real.

Você pode criar uma conexão de saída em tempo real com o [!DNL Amazon Kinesis] armazenamento para fazer o stream de dados do Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Amazon Kinesis], consulte o [Documentação do Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Para conectar-se a [!DNL Amazon Kinesis] programaticamente, consulte o [Tutorial da API de destinos de transmissão](../../api/streaming-destinations.md).
* Para conectar-se a [!DNL Amazon Kinesis] usando a interface do usuário da Platform, consulte as seções abaixo.

![Amazon Kinesis na interface do usuário](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casos de uso {#use-cases}

Ao usar destinos de transmissão, como [!DNL Amazon Kinesis], você pode alimentar facilmente eventos de segmentação de alto valor e atributos de perfil associados nos sistemas de sua escolha.

Por exemplo, um prospecto baixou um white-paper que os qualifica em um segmento de &quot;alta propensão à conversão&quot;. Mapeando o segmento em que o prospecto entra na [!DNL Amazon Kinesis] , você receberia esse evento em [!DNL Amazon Kinesis]. Lá, você pode empregar uma abordagem faça você mesmo e descrever a lógica de negócios sobre o evento, pois acha que funcionaria melhor com os sistemas de TI de sua empresa.

## Tipo de exportação {#export-type}

**Baseado em perfil** - estiver exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do [fluxo de trabalho de ativação do público](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Obrigatório [!DNL Amazon Kinesis] permissões {#required-kinesis-permission}

Para se conectar e exportar dados com êxito para seu [!DNL Amazon Kinesis] fluxos, o Experience Platform precisa de permissões para as seguintes ações:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Essas permissões são organizadas por meio do [!DNL Kinesis] e são marcados pela Platform depois de configurar o destino do Kinesis na interface do usuário da plataforma.

O exemplo abaixo exibe os direitos mínimos de acesso necessários para exportar dados com êxito para um [!DNL Kinesis] destino.

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

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!DNL Amazon Web Services]chave de acesso e chave secreta**: Em [!DNL Amazon Web Services]gerar um `access key - secret access key` par para conceder acesso à plataforma [!DNL Amazon Kinesis] conta. Saiba mais na [Documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **região**: Indicar qual [!DNL Amazon Web Services] região para a qual transmitir dados.
* **Nome**: Forneça um nome para a conexão com o [!DNL Amazon Kinesis]
* **Descrição**: Forneça uma descrição para a conexão com o [!DNL Amazon Kinesis].
* **fluxo**: Forneça o nome de um fluxo de dados existente em seu [!DNL Amazon Kinesis] conta. A Platform exportará dados para esse fluxo.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Ativar segmentos para este destino {#activate}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Comportamento de exportação de perfil {#profile-export-behavior}

O Experience Platform otimiza o comportamento de exportação do perfil para o destino do Amazon Kinesis, a fim de exportar apenas dados para o seu destino quando ocorrerem atualizações relevantes para um perfil após a qualificação de segmento ou outros eventos significativos. Os perfis são exportados para o seu destino nas seguintes situações:

* A atualização de perfil foi acionada por uma alteração na associação de segmento para pelo menos um dos segmentos mapeados para o destino. Por exemplo, o perfil se qualificou para um dos segmentos mapeados para o destino ou saiu de um dos segmentos mapeados para o destino.
* A atualização do perfil foi acionada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos segmentos mapeados para o destino foi adicionado a uma nova identidade no atributo do mapa de identidade.
* A atualização do perfil foi acionada por uma alteração em atributos para pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis onde as atualizações relevantes ocorreram são exportados para o seu destino. Por exemplo, se um segmento mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o seu destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde as alterações se encontrem. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

## Dados exportados {#exported-data}

Seu exportado [!DNL Experience Platform] os dados chegam em [!DNL Amazon Kinesis] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de um público que se qualificou para um determinado segmento e saiu de outro. As identidades desse prospecto são ECID e email.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
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
>* [Destino de Hubs de Eventos do Azure](./azure-event-hubs.md)
>* [Tipos e categorias de destino](../../destination-types.md)

