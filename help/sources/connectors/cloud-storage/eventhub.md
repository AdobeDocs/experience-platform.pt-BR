---
keywords: 'Experience Platform;home;popular tópicos;Hubs de Evento do Azure;hubs de evento do azure;Hubs de Evento;hubs de evento;hubs de ;hubs de  do Azure;hubs de ;hubs de ;hubs de ;hubs de '
solution: Experience Platform
title: Conector Hubs de Evento do Azure
topic: overview
description: A documentação abaixo fornece informações sobre como conectar os Hubs de Evento do Azure à plataforma usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# (Beta) Conector de Hubs de Evento do Azure

>[!NOTE]
>
>O conector do Hubs de Evento do Azure está em beta. Consulte a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamentos na nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. [!DNL Platform] permite inserir dados  [!DNL Azure Event Hubs] em tempo real.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Conectar [!DNL Azure Event Hubs] a [!DNL Platform]

A documentação abaixo fornece informações sobre como conectar [!DNL Azure Event Hubs] a [!DNL Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar um conector Hubs de Evento do Azure usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Coletar dados de fluxo usando a API de Serviço de Fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface

- [Criar um conector de origem de Hubs de Evento do Azure na interface do usuário](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configurar um fluxo de dados para um conector de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)