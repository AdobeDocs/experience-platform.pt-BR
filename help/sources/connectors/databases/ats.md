---
keywords: Experience Platform, home, tópicos populares, Armazenamento de tabela do Azure, armazenamento de tabela do azure, ATS, ats
solution: Experience Platform
title: Visão Geral do Conector de Origem de Armazenamento de Tabela do Azure
topic-legacy: overview
description: Saiba como conectar o Armazenamento de Tabela do Azure à Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# [!DNL Azure Table Storage] conector

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de um banco de dados de terceiros. A plataforma pode se conectar a diferentes tipos de bancos de dados, como relacional, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Azure Table Storage].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>No momento, o conector de origem [!DNL Azure Table Storage] não oferece suporte à conectividade de mesma região com a Plataforma. Isso significa que se a instância do Azure estiver usando a mesma região de rede que a Plataforma, uma conexão com as fontes da Plataforma não poderá ser estabelecida. Atualmente, somente a conectividade entre regiões é compatível. Entre em contato com o gerente de conta do Adobe para obter mais informações.

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Table Storage] à Plataforma usando APIs ou a interface do usuário:

## Conecte [!DNL Azure Table Storage] à plataforma usando APIs

- [Criar uma conexão base de Armazenamento de Tabela do Azure usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/ats.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

## Conecte [!DNL Azure Table Storage] à plataforma usando a interface do usuário

- [Criar uma conexão de origem do Armazenamento de Tabela do Azure na interface do usuário](../../tutorials/ui/create/databases/ats.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)
