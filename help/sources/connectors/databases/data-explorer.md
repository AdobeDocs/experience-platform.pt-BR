---
keywords: Experience Platform, home, tópicos populares, Data Explorer do Azure, explorador de dados do azure
solution: Experience Platform
title: Visão Geral do Conector de Origem do Azure Data Explorer
topic-legacy: overview
description: Saiba como conectar o Azure Data Explorer ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 869bd8bb-51e6-4e0c-a3ec-ff083dda5789
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Conector (Beta) [!DNL Azure Data Explorer]

>[!NOTE]
>
>O conector [!DNL Azure Data Explorer] está em beta. Consulte a [Visão geral das Fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

O Adobe Experience Platform fornece conectividade nativa para provedores de banco de dados como [!DNL Microsoft], MySQL e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

Há suporte para diferentes tipos de bancos de dados de terceiros, incluindo depósitos relacionais, NoSQL ou de dados. O suporte para provedores de banco de dados inclui [!DNL Azure Data Explorer].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>No momento, o conector de origem [!DNL Azure Data Explorer] não oferece suporte à conectividade de mesma região com a Plataforma. Isso significa que se a instância do Azure estiver usando a mesma região de rede que a Plataforma, uma conexão com as fontes da Plataforma não poderá ser estabelecida. Atualmente, somente a conectividade entre regiões é compatível. Entre em contato com o gerente de conta do Adobe para obter mais informações.

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Data Explorer] a [!DNL Platform] usando APIs ou a interface do usuário:

## Conecte [!DNL Azure Data Explorer] a [!DNL Platform] usando APIs

- [Criar uma conexão base de Data Explorer do Azure usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/data-explorer.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

## Conecte [!DNL Azure Data Explorer] a [!DNL Platform] usando a interface do usuário

- [Criar uma conexão de origem de Data Explorer do Azure na interface do usuário](../../tutorials/ui/create/databases/data-explorer.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)
