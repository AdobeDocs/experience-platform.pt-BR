---
keywords: Experience Platform, home, tópicos populares, Hubs de eventos do Azure, Hubs de eventos do azure, Hubs de eventos, Hubs de eventos
solution: Experience Platform
title: Visão Geral do Conector de Origem dos Hubs de Eventos do Azure
topic-legacy: overview
description: Saiba como conectar Hubs de Eventos do Azure ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# (Beta) Conector de Hubs de Eventos do Azure

>[!NOTE]
>
>O conector do Hubs de Eventos do Azure está em beta. Consulte a [Visão geral das Fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamento em nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes . [!DNL Platform] O permite trazer dados do  [!DNL Azure Event Hubs] em tempo real.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Conecte [!DNL Azure Event Hubs] a [!DNL Platform]

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Event Hubs] a [!DNL Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem de Hubs de Eventos do Azure usando a API do Serviço de Fluxo](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Coletar dados de fluxo usando a API do Serviço de fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface do usuário

- [Criar uma conexão de origem dos Hubs de Eventos do Azure na interface do usuário](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
