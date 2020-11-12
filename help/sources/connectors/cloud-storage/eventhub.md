---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Conector Hubs de Evento do Azure
topic: overview
description: A documentação abaixo fornece informações sobre como conectar os Hubs de Evento do Azure à plataforma usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: e0a0b7fc28b8cc85c5140d3840e06e5c7078c307
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# (Beta) Conector de Hubs de Evento do Azure

>[!NOTE]
>
>O conector do Hubs de Evento do Azure está em beta. Consulte a visão geral [das](../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform]e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamentos na nuvem podem inserir seus próprios dados [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. [!DNL Platform] permite que você insira dados de [!DNL Azure Event Hubs] em tempo real.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes. Consulte a página lista de permissões [do endereço](../../ip-address-allow-list.md) IP para obter mais informações.

## Conectar-se [!DNL Azure Event Hubs] a [!DNL Platform]

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Event Hubs] a [!DNL Platform] APIs ou à interface do usuário:

### Uso de APIs

- [Criar um conector Hubs de Evento do Azure usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar um conector de origem de Hubs de Evento do Azure na interface do usuário](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configurar um fluxo de dados para um conector de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)