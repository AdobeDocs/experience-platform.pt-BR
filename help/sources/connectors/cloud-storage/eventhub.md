---
keywords: Experience Platform, home, tópicos populares, Hubs de eventos do Azure, Hubs de eventos do azure, Hubs de eventos, Hubs de eventos
solution: Experience Platform
title: Visão Geral do Conector de Origem dos Hubs de Eventos do Azure
topic-legacy: overview
description: Saiba como conectar Hubs de Eventos do Azure ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: cda9ca9c560b1af2147c00ea4e89dff09b7428ba
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] conector

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como o AWS, [!DNL Google Cloud Platform]e [!DNL Azure]. Você pode trazer seus dados desses sistemas para a Plataforma.

As fontes de armazenamento em nuvem podem trazer seus próprios dados para a plataforma sem precisar baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes . A Platform permite trazer dados do [!DNL Event Hubs] em tempo real.

## Usar uma rede virtual à qual se conectar [!DNL Event Hubs] para a plataforma

Você pode configurar uma rede virtual para se conectar [!DNL Event Hubs] para a Platform enquanto as medidas de firewall estão ativadas. Para configurar uma rede virtual, vá para [[!DNL Event Hubs] documento de conjunto de regras de rede](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) e depois selecione **Experimente** no painel REST API. Em seguida, autentique seu [!DNL Azure] conta usando suas credenciais e selecione a [!DNL Event Hubs] namespace, grupo de recursos e assinatura que você deseja trazer para a plataforma.

Após a configuração, atualize o **corpo da solicitação** com o JSON que corresponde à sua região de rede, na lista abaixo:

>[!TIP]
>
>Você deve fazer um backup das regras de filtragem IP do firewall existentes, pois elas serão excluídas após esta chamada.

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
          "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
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
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Veja o seguinte [[!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) para obter mais informações sobre conjuntos de regras de rede.

## Connect [!DNL Event Hubs] para a plataforma

A documentação abaixo fornece informações sobre como se conectar [!DNL Event Hubs] para Plataforma usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem de Hubs de Eventos usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Coletar dados de fluxo usando a API do Serviço de fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface do usuário

- [Criar uma conexão de origem de Hubs de eventos na interface do usuário](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
