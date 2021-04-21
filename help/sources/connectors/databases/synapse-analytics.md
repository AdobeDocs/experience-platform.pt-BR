---
keywords: Experience Platform, home, tópicos populares, Azure synapse Analytics, azure synapse analytics, Synapse, sinapse
solution: Experience Platform
title: Visão geral do conector de origem do Azure synapse Analytics
topic-legacy: overview
description: Saiba como conectar o Azure synapse Analytics ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Conector (Beta) [!DNL Azure Synapse Analytics]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando serviços [!DNL Platform]. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] O oferece suporte para assimilar dados de um banco de dados de terceiros. [!DNL Platform] pode se conectar a diferentes tipos de bancos de dados, como relacional, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Azure Synapse Analytics].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>No momento, o conector de origem [!DNL Azure Synapse Analytics] não oferece suporte à conectividade de mesma região com a Plataforma. Isso significa que se a instância do Azure estiver usando a mesma região de rede que a Plataforma, uma conexão com as fontes da Plataforma não poderá ser estabelecida. Atualmente, somente a conectividade entre regiões é compatível. Entre em contato com o gerente de conta do Adobe para obter mais informações.

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Synapse Analytics] a [!DNL Platform] usando APIs ou a interface do usuário:

## Conecte [!DNL Azure Synapse Analytics] a [!DNL Platform] usando APIs

- [Criar uma conexão de origem do Azure synapse Analytics usando a API de Serviço de Fluxo](../../tutorials/api/create/databases/synapse-analytics.md)
- [Explorar um sistema de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Coletar dados de um banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

## Conecte [!DNL Azure Synapse Analytics] a [!DNL Platform] usando a interface do usuário

- [Criar uma conexão de origem do Azure synapse Analytics na interface do usuário](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Configurar um fluxo de dados para uma conexão de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)
