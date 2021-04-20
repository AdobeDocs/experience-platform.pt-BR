---
keywords: Experience Platform, home, tópicos populares, Google PubSub, google pubsub
solution: Experience Platform
title: Visão geral do Google PubSub Source Connector
topic: overview
description: Saiba como conectar o Google PubSub à Adobe Experience Platform usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Conector (Beta) [!DNL Google PubSub]

>[!NOTE]
>
>O conector [!DNL Google PubSub] está em beta. Consulte a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como [!DNL AWS], [!DNL Google Cloud Platform] e [!DNL Azure], permitindo que você traga dados desses sistemas para a Platform para uso em serviços e destinos de downstream.

As fontes de armazenamento em nuvem podem trazer seus dados para a plataforma sem a necessidade de baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de fontes. A Platform permite trazer dados de [!DNL Azure Event Hubs] em tempo real.

## Lista de permissões de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [Lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Conectar [!DNL Google PubSub] à plataforma

A documentação abaixo fornece informações sobre como se conectar [!DNL Google PubSub] à Plataforma usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem Google PubSub usando a API do Serviço de Fluxo](../../tutorials/api/create/cloud-storage/google-pubsub.md)
- [Coletar dados de fluxo usando a API do Serviço de fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface do usuário

- [Criar uma conexão de fonte do Google PubSub na interface do usuário](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)