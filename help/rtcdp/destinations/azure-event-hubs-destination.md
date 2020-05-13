---
title: Destino dos Hubs de Evento do Azure
seo-title: Destino dos Hubs de Evento do Azure
description: Crie uma conexão de saída em tempo real com seu armazenamento de Hubs de Evento do Azure para transmitir dados da plataforma Experience.
seo-description: Crie uma conexão de saída em tempo real com seu armazenamento de Hubs de Evento do Azure para transmitir dados da plataforma Experience.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# Destino dos Hubs de Evento do Azure

## Visão geral {#overview}

[!DNL Azure Event Hubs] é uma grande plataforma de transmissão de dados e um serviço de ingestão de eventos. Pode receber e processar milhões de eventos por segundo. Os dados enviados para um hub de evento podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de agrupamento/armazenamento.

Você pode criar uma conexão de saída em tempo real com seu [!DNL Azure Event Hubs] armazenamento para transmitir dados da Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Azure Event Hubs], consulte a documentação [da](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)Microsoft.
* Para conectar-se a [!DNL Azure Event Hubs] chamadas de API, consulte o tutorial [da API de destinos de]transmissão contínua.
* Para conectar-se [!DNL Azure Event Hubs] usando a interface do usuário CDP em tempo real da Adobe, consulte as seções abaixo.

![AWS Kinesis na interface do usuário](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Casos de uso {#use-cases}

Ao usar destinos de streaming como os Hubs de Evento do Azure, você pode facilmente alimentar eventos de segmentação de alto valor e atributos de perfil associados em seus sistemas de escolha.

Por exemplo, um prospecto baixou um white paper que os qualifica em um segmento de &quot;alta propensão para converter&quot;. Ao mapear o segmento no qual o prospecto cai para o destino dos Hubs de Evento do Azure, você receberá esse evento nos Hubs de Evento do Azure. Lá, você pode usar uma abordagem faça-você-mesmo e descrever a lógica comercial sobre o evento, pois você acha que funcionaria melhor com seus sistemas de TI corporativos.

## Destino do Connect {#connect-destination}

Consulte Fluxo de trabalho de destinos do armazenamento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obter instruções sobre como se conectar aos destinos do armazenamento na nuvem, incluindo [!DNL Azure Event Hubs].

Para [!DNL Azure Event Hubs] destinos, insira as seguintes informações no fluxo de trabalho de criação de destino:

### Na etapa Conta {#account-step}

* **[!UICONTROL Nome]** da chave SAS e chave **** SAS: Preencha o nome e a chave da sua chave SAS. Saiba mais sobre como autenticar [!DNL Azure Event Hubs] com chaves SAS na documentação [da](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Namespace]**: Preencha a sua [!DNL Azure Event Hubs] namespace. Saiba mais sobre [!DNL Azure Event Hubs] as namespaces na documentação [da](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Entrada necessária na etapa de autenticação](/help/rtcdp/destinations/assets/event-hubs-account-step.png)

### Na etapa Autenticação {#authentication-step}

* **[!UICONTROL Nome]**: Preencha um nome para a conexão com [!DNL Azure Event Hubs].
* **[!UICONTROL Descrição]**: Forneça uma descrição da conexão.  Exemplos: &quot;Clientes premium&quot;, &quot;Masculino interessado em cozinha&quot;.
* **[!UICONTROL eventHubName]**: Forneça um nome para o fluxo para o seu [!DNL Azure Event Hubs] destino.

![Dados necessários na etapa de configuração](/help/rtcdp/destinations/assets/event-hubs-authentication-step.png)

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.


## Dados exportados {#exported-data}

Seus dados exportados da plataforma de experiência vêm no formato [!DNL Azure Event Hubs] JSON. Por exemplo, um fluxo de evento contendo a identidade de email com hash de uma audiência que saiu de um determinado segmento pode ser semelhante a:

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
>* Tutorial da API Link para Hubs de Eventos do Azure
>* [Destino AWS Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Tipos de destino e categorias](/help/rtcdp/destinations/destination-types.md)