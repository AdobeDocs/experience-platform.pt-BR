---
title: Visão geral do Conector do Source dos Hubs de Eventos do Azure
description: Saiba como conectar os Hubs de Eventos do Azure ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 02c777b5db9734cf45b35f131d83c35c5ce670fb
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] origem

>[!IMPORTANT]
>
>* A origem [!DNL Azure Event Hubs] está disponível no catálogo de origens para usuários que compraram o Real-Time CDP Ultimate.
>
>* Agora você pode usar a origem [!DNL Azure Event Hubs] ao executar o Adobe Experience Platform no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. Você pode trazer seus dados desses sistemas para a Experience Platform.

As fontes de armazenamento na nuvem podem trazer seus próprios dados para a Experience Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens. O Experience Platform permite trazer dados de [!DNL Event Hubs] em tempo real.

## Dimensionamento com [!DNL Event Hubs]

O fator de escala da instância do [!DNL Event Hubs] deve ser aumentado se você precisar assimilar dados de alto volume, aumentar o paralelismo ou aumentar a velocidade da assimilação no Experience Platform.

### Dados de maior volume de entrada

Atualmente, o volume máximo de dados que você pode trazer da sua conta do [!DNL Event Hubs] para a Experience Platform é de 2000 registros por segundo. Para aumentar e assimilar dados de volume maior, entre em contato com o representante da Adobe.

### Aumentar paralelismo no [!DNL Event Hubs] e no Experience Platform

Paralelismo refere-se à execução simultânea das mesmas tarefas em várias unidades de processamento para aumentar a velocidade e o desempenho. Você pode aumentar o paralelismo no lado do [!DNL Event Hubs] aumentando a partição ou adquirindo mais unidades de processamento para sua conta [!DNL Event Hubs]. Consulte este [[!DNL Event Hubs] documento no dimensionamento](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) para obter mais informações.

Para aumentar a taxa de velocidade da assimilação no Experience Platform, o Experience Platform deve aumentar o número de tarefas no conector de origem para ler das partições do [!DNL Event Hubs]. Depois de aumentar o paralelismo no lado do [!DNL Event Hubs], entre em contato com o representante da Adobe para dimensionar as tarefas do Experience Platform com base na nova partição. Atualmente, esse processo não é automatizado.

## Usar uma rede virtual para se conectar ao [!DNL Event Hubs] ao Experience Platform

O Experience Platform dá suporte à conexão com [!DNL Event Hubs] via rede virtual. Isso permite transferir dados por uma conexão privada segura em vez da Internet pública. Incluir na lista de permissões Você pode modificar o Experience Platform VNet para rotear com segurança o tráfego [!DNL Event Hubs] através do backbone privado [!DNL Azure], mantendo as proteções de firewall existentes.

Para configurar uma rede virtual, vá para este [[!DNL Event Hubs] documento do conjunto de regras de rede](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) e siga as etapas listadas abaixo:

* Selecione **Experimentar** no painel REST API;
* Autentique sua conta do [!DNL Azure] usando suas credenciais no mesmo navegador;
* Selecione o namespace [!DNL Event Hubs], o grupo de recursos e a assinatura que você deseja trazer para a Experience Platform e selecione **EXECUTAR**;
* No corpo JSON exibido, adicione a seguinte sub-rede Experience Platform em `virtualNetworkRules` dentro de `properties`:


>[!IMPORTANT]
>
>Você deve fazer um backup do corpo JSON recebido antes de atualizar `virtualNetworkRules` com a sub-rede do Experience Platform, pois ela contém suas regras de filtragem de IP existentes. Caso contrário, as regras serão excluídas após a chamada.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Consulte a lista abaixo para ver as diferentes regiões das sub-redes do Experience Platform:

### VA7: América do Norte

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2: Europa

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5: Austrália

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5-vnet/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Consulte o seguinte [[!DNL Event Hubs] documento](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) para obter mais informações sobre conjuntos de regras de rede.

## Conectar [!DNL Event Hubs] ao Experience Platform

>[!NOTE]
>
>Depois de criar ou atualizar um fluxo de dados de transmissão, é necessária uma breve pausa de 5 minutos na assimilação de dados para evitar possíveis instâncias de perda ou perda de dados.

A documentação abaixo fornece informações sobre como conectar o [!DNL Event Hubs] ao Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

* [Criar uma conexão de origem de Hubs de Eventos usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Coletar dados de transmissão usando a API de Serviço de Fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface

* [Criar uma conexão de origem de Hubs de Eventos na interface](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
