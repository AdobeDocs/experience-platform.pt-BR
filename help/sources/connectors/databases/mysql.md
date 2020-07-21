---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector MySQL
topic: overview
translation-type: tm+mt
source-git-commit: 3b5e76afea5689dbd59f64f6192e6ef2a6acb7d3
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# (Beta) Conector MySQL

>[!NOTE]
>O conector MySQL está em beta. Consulte a visão geral [das](../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas, ao mesmo tempo em que lhe fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] fornece suporte para assimilar dados de um banco de dados de terceiros. [!DNL Platform] pode se conectar a diferentes tipos de bancos de dados, como relacional, NoSQL ou datas warehouses. O suporte para provedores de banco de dados inclui MySQL.

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

A documentação abaixo fornece informações sobre como conectar o MySQL a [!DNL Platform] APIs ou à interface do usuário:

## Conectar o MySQL a [!DNL Platform] APIs

- [Criar um conector MySQL usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/mysql.md)
- [Explore um sistema de banco de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Coletar dados de um banco de dados usando a API de Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar MySQL para [!DNL Platform] usar a interface do usuário

- [Criar um conector de origem MySQL na interface do usuário](../../tutorials/ui/create/databases/mysql.md)
- [Configurar um fluxo de dados para um conector de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)