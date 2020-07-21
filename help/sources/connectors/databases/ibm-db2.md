---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector IBM DB2
topic: overview
translation-type: tm+mt
source-git-commit: 3b5e76afea5689dbd59f64f6192e6ef2a6acb7d3
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# (Beta) Conector IBM DB2

>[!NOTE]
>O conector IBM DB2 está em beta. Consulte a visão geral [das](../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

O Adobe Experience Platform fornece conectividade nativa para provedores de banco de dados como [!DNL Microsoft], MySQL e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

Diferentes tipos de bancos de dados de terceiros são suportados, incluindo relacional, NoSQL ou data warehouse. O suporte para provedores de banco de dados inclui o IBM DB2.

## lista de permissões de endereço IP

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

A documentação abaixo fornece informações sobre como conectar o IBM DB2 a [!DNL Platform] APIs ou a interface do usuário:

## Conectar o IBM DB2 a [!DNL Platform] APIs

- [Criar um conector IBM DB2 usando a API de Serviço de Fluxo](../../tutorials/api/create/databases/ibm-db2.md)
- [Explore um sistema de banco de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Coletar dados de um banco de dados usando a API de Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

## Conecte o IBM DB2 para [!DNL Platform] usar a interface do usuário

- [Criar um conector de origem IBM DB2 na interface do usuário](../../tutorials/ui/create/databases/ibm-db2.md)
- [Configurar um fluxo de dados para um conector de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)