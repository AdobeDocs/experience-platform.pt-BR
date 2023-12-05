---
title: Visão geral do conector de origem dos Hubs de eventos do Azure
description: Saiba como conectar os Hubs de Eventos do Azure ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 12ddf87d594b7e25a0356cd419e990b262c1734e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] origem

>[!IMPORTANT]
>
>A variável [!DNL Azure Event Hubs] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, [!DNL Google Cloud Platform], e [!DNL Azure]. Você pode trazer seus dados desses sistemas para a Platform.

As fontes de armazenamento na nuvem podem trazer seus próprios dados para a Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens. A Platform permite trazer dados de [!DNL Event Hubs] em tempo real.

## Dimensionamento com [!DNL Event Hubs]

O fator de escala do seu [!DNL Event Hubs] A instância do deve ser aumentada se for necessário assimilar dados de alto volume, aumentar o paralelismo ou aumentar a velocidade da plataforma de assimilação.

### Dados de maior volume de entrada

Atualmente, o volume máximo de dados que você pode trazer de sua [!DNL Event Hubs] para a Platform é de 2000 registros por segundo. Para aumentar e assimilar dados de volume maior, entre em contato com o representante da Adobe.

### Aumentar paralelismo em [!DNL Event Hubs] e Platform

Paralelismo refere-se à execução simultânea das mesmas tarefas em várias unidades de processamento para aumentar a velocidade e o desempenho. É possível aumentar o paralelismo no [!DNL Event Hubs] lado aumentando a partição ou adquirindo mais unidades de processamento para o seu [!DNL Event Hubs] conta. Veja isto [[!DNL Event Hubs] documento no dimensionamento](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) para obter mais informações.

Para aumentar a taxa de velocidade de assimilação no lado da Platform, a Platform deve aumentar o número de tarefas no conector de origem para ler do [!DNL Event Hubs] partições. Depois de aumentar o paralelismo no [!DNL Event Hubs] Por favor, entre em contato com seu representante da Adobe para escalar as tarefas da Platform com base em sua nova partição. Atualmente, esse processo não é automatizado.

## Usar uma rede virtual para se conectar a [!DNL Event Hubs] para a Platform

Você pode configurar uma rede virtual para se conectar [!DNL Event Hubs] para a Platform enquanto as medidas de firewall estão ativadas. Para configurar uma rede virtual, vá para [[!DNL Event Hubs] documento de conjunto de regras de rede](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) e siga as etapas listadas abaixo:

* Selecionar **Experimente** no painel REST API;
* Autentique seu [!DNL Azure] conta usando suas credenciais no mesmo navegador;
* Selecione o [!DNL Event Hubs] namespace, grupo de recursos e assinatura que você deseja trazer para a Platform e, em seguida, selecionar **EXECUÇÃO**;
* No corpo JSON exibido, adicione a seguinte sub-rede da plataforma em `virtualNetworkRules` dentro `properties`:


>[!IMPORTANT]
>
>Você deve fazer um backup do corpo JSON recebido antes da atualização `virtualNetworkRules` com a sub-rede da Platform, pois ela contém suas regras de filtragem de IP existentes. Caso contrário, as regras serão excluídas após a chamada.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Consulte a lista abaixo para ver as diferentes regiões das sub-redes da Platform:

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

## Conectar [!DNL Event Hubs] para a Platform

A documentação abaixo fornece informações sobre como se conectar [!DNL Event Hubs] para a Platform usando APIs ou a interface do usuário:

### Uso de APIs

* [Criar uma conexão de origem de Hubs de Eventos usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Coletar dados de transmissão usando a API de Serviço de Fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface

* [Criar uma conexão de origem de Hubs de Eventos na interface](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
