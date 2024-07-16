---
title: Visão geral do Snowflake Source Connector
description: Saiba como conectar o Snowflake ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Snowflake] origem

>[!IMPORTANT]
>
>* A origem [!DNL Snowflake] está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.
>* Por padrão, a origem [!DNL Snowflake] interpreta `null` como uma cadeia de caracteres vazia. Entre em contato com seu representante de Adobe para garantir que seus valores de `null` sejam gravados corretamente como `null` no Adobe Experience Platform.
>* Para Experience Platform assimilar dados, os fusos horários de todas as fontes de lote baseadas em tabela devem ser configurados como UTC. O único carimbo de data/hora com suporte para a origem [!DNL Snowflake] é TIMESTAMP_NTZ com a hora UTC.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um banco de dados de terceiros. A Platform pode se conectar a diferentes tipos de bancos de dados, como bancos de dados relacionais, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Snowflake].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

A documentação abaixo fornece informações sobre como conectar o [!DNL Snowflake] à Plataforma usando APIs ou a interface do usuário:

## Conectar [!DNL Snowflake] à plataforma usando APIs

* [Criar uma conexão básica de Snowflake usando a API do serviço de fluxo](../../tutorials/api/create/databases/snowflake.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Snowflake] à Plataforma usando a interface

* [Criar uma conexão de origem de Snowflake na interface](../../tutorials/ui/create/databases/snowflake.md)
* [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
