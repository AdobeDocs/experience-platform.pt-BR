---
title: Destino da Amazon Kinesis
seo-title: Destino da Amazon Kinesis
description: Crie uma conexão de saída em tempo real com seu armazenamento Amazon Kinesis para transmitir dados da plataforma Adobe Experience.
seo-description: Crie uma conexão de saída em tempo real com seu armazenamento Amazon Kinesis para transmitir dados da plataforma Adobe Experience.
translation-type: tm+mt
source-git-commit: 47e03d3f58bd31b1aec45cbf268e3285dd5921ea
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# (Beta) Destino da Amazon Kinesis


>[!IMPORTANT]
>
>O [!DNL Amazon Kinesis] destino no Adobe Real-time CDP está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

O [!DNL Kinesis Data Streams] serviço da Amazon Web Services permite coletar e processar grandes fluxos de registros de dados em tempo real.

Você pode criar uma conexão de saída em tempo real com seu [!DNL Amazon Kinesis] armazenamento para transmitir dados da Adobe Experience Platform.

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

### Na etapa Conta {#account-step}

* **Chave de acesso e chave** secreta dos Serviços Web da Amazon: Em [!DNL Amazon Web Services], gere uma chave de acesso - par de chaves de acesso secreto para conceder à Adobe o acesso CDP em tempo real à sua [!DNL Amazon Kinesis] conta. Saiba mais na documentação [dos Serviços da Web da](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon.
* **região**: Indica em qual [!DNL Amazon Web Services] região os dados serão transmitidos.

![Campos de entrada na etapa da conta](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### Na etapa Autenticação {#authentication-step}

* **Nome**: Forneça um nome para a sua conexão com [!DNL Amazon Kinesis]
* **Descrição**: Forneça uma descrição para a sua conexão com [!DNL Amazon Kinesis].
* **fluxo**: Forneça o nome do seu fluxo de dados existente na sua [!DNL Amazon Kinesis] conta. A CDP em tempo real da Adobe exportará dados para esse fluxo.

![Campos de entrada na etapa de autenticação](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Dados exportados {#exported-data}

Seus dados exportados da plataforma de experiência vêm no formato [!DNL Amazon Kinesis] JSON. Por exemplo, um evento que contém a identidade de email com hash de uma audiência que saiu de um determinado segmento pode ser semelhante a:

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* [Conecte-se ao Amazon Kinesis e ative dados usando chamadas de API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destino dos Hubs de Evento do Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Tipos de destino e categorias](/help/rtcdp/destinations/destination-types.md)

