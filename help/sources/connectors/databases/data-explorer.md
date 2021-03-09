---
keywords: Experience Platform, home, tópicos populares, Azure Data Explorer, azure data explorer
solution: Experience Platform
title: Visão Geral do Conector de Origem do Azure Data Explorer
topic: visão geral
description: Saiba como conectar o Azure Data Explorer à Adobe Experience Platform usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Conector (Beta) [!DNL Azure Data Explorer]

>[!NOTE]
>
>O conector [!DNL Azure Data Explorer] está em beta. Consulte a [Visão geral das Fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

A Adobe Experience Platform fornece conectividade nativa para provedores de banco de dados como [!DNL Microsoft], MySQL e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

Há suporte para diferentes tipos de bancos de dados de terceiros, incluindo depósitos relacionais, NoSQL ou de dados. O suporte para provedores de banco de dados inclui [!DNL Azure Data Explorer].

## Lista de permissões de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [Lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>No momento, o conector de origem [!DNL Azure Data Explorer] não oferece suporte à conectividade de mesma região com a Plataforma. Isso significa que se a instância do Azure estiver usando a mesma região de rede que a Plataforma, uma conexão com as fontes da Plataforma não poderá ser estabelecida. Atualmente, somente a conectividade entre regiões é compatível. Entre em contato com o gerente de conta da Adobe para obter mais informações.

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Data Explorer] a [!DNL Platform] usando APIs ou a interface do usuário:

## Conecte [!DNL Azure Data Explorer] a [!DNL Platform] usando APIs

- [Criar uma conexão de origem do Azure Data Explorer usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/data-explorer.md)
- [Explorar um sistema de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Coletar dados de um banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

## Conecte [!DNL Azure Data Explorer] a [!DNL Platform] usando a interface do usuário

- [Criar uma conexão de origem do Azure Data Explorer na interface do usuário](../../tutorials/ui/create/databases/data-explorer.md)
- [Configurar um fluxo de dados para uma conexão de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)