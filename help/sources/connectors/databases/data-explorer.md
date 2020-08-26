---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de Data Explorer do Azure
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Conector (Beta) [!DNL Azure Data Explorer]

>[!NOTE]
>
>O [!DNL Azure Data Explorer] conector está em beta. Consulte a visão geral [das](../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

A Adobe Experience Platform fornece conectividade nativa para provedores de banco de dados como [!DNL Microsoft], MySQL e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

Diferentes tipos de bancos de dados de terceiros são suportados, incluindo depósitos relacionais, NoSQL ou de dados. O suporte para provedores de banco de dados inclui [!DNL Azure Data Explorer].

## LISTA DE PERMISSÕES de endereço IP

Os seguintes endereços IP devem ser adicionados a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes.

### Região Leste dos EUA

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Região da Europa Ocidental

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Austrália Oriental

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Data Explorer] a [!DNL Platform] APIs ou à interface do usuário:

## Conectar-se [!DNL Azure Data Explorer] a [!DNL Platform] APIs

- [Criar um conector de Data Explorer do Azure usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/data-explorer.md)
- [Explore um sistema de banco de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Coletar dados de um banco de dados usando a API de Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar-se [!DNL Azure Data Explorer] à [!DNL Platform] interface do usuário

- [Criar um conector de origem de Data Explorer do Azure na interface do usuário](../../tutorials/ui/create/databases/data-explorer.md)
- [Configurar um fluxo de dados para um conector de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)