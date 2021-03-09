---
keywords: Experience Platform; home; tópicos populares; Microsoft SQL; microsoft sql; SQL; sql
solution: Experience Platform
title: Visão Geral do Conector de Origem do SQL Server
topic: visão geral
description: Saiba como conectar o Microsoft SQL Server à Adobe Experience Platform usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# (Beta) [!DNL Microsoft] Conector do SQL Server

A Adobe Experience Platform permite que os dados sejam assimilados de fontes externas, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando serviços [!DNL Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] O oferece suporte para assimilar dados de um banco de dados de terceiros. [!DNL Platform] pode se conectar a diferentes tipos de bancos de dados, como relacional, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Microsoft] SQL Server.

## Lista de permissões de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [Lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>O [!DNL Microsoft] conector de origem do SQL Server atualmente não oferece suporte à conectividade de mesma região com o Platform. Isso significa que se a instância do Azure estiver usando a mesma região de rede que a Plataforma, uma conexão com as fontes da Plataforma não poderá ser estabelecida. Atualmente, somente a conectividade entre regiões é compatível. Entre em contato com o gerente de conta da Adobe para obter mais informações.

A documentação abaixo fornece informações sobre como conectar o [!DNL Microsoft] SQL Server a [!DNL Platform] usando APIs ou a interface do usuário:

## Conecte o [!DNL Microsoft] SQL Server a [!DNL Platform] usando APIs

- [Criar uma conexão de origem do Microsoft SQL Server usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/sql-server.md)
- [Explorar um sistema de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Coletar dados de um banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

## Conecte o [!DNL Microsoft] SQL Server a [!DNL Platform] usando a interface do usuário

- [Criar uma conexão de origem do Microsoft SQL Server na interface do usuário](../../tutorials/ui/create/databases/sql-server.md)
- [Configurar um fluxo de dados para uma conexão de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)