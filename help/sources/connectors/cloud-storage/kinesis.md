---
keywords: Experience Platform;lar;tópicos populares;Amazon Kinesis;amazon cinesis;Kinesis;cinesis
solution: Experience Platform
title: Visão geral do Amazon Kinesis Source Connector
topic: overview
description: Saiba como conectar o Amazon Kinesis ao Adobe Experience Platform usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: a489ab248793a063295578943ad600d8eacab6a2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Conector (Beta) [!DNL Amazon Kinesis]

>[!NOTE]
>
>O conector [!DNL Amazon Kinesis] está em beta. Consulte a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamentos na nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. [!DNL Platform] permite inserir dados  [!DNL Amazon Kinesis] em tempo real.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Conectar [!DNL Amazon Kinesis] a [!DNL Platform]

A documentação abaixo fornece informações sobre como conectar [!DNL Amazon Kinesis] a [!DNL Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem Amazon Kinesis usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Coletar dados de fluxo usando a API de Serviço de Fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface

- [Criar uma conexão de origem Amazon Kinesis na interface do usuário](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)