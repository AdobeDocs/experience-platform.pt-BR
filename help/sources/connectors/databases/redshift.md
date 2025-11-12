---
title: Visão geral do Amazon Redshift Source Connector
description: Saiba como conectar o Amazon Redshift ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 7%

---

# [!DNL Amazon Redshift] origem

>[!IMPORTANT]
>
>- A origem [!DNL Amazon Redshift] está disponível no catálogo de origens para usuários que compraram o Real-Time CDP Ultimate.
>
>- Agora você pode usar a origem [!DNL Amazon Redshift] ao executar o Adobe Experience Platform no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).


A Adobe Experience Platform permite a assimilação de dados de fontes externas, além de permitir estruturar, rotular e aprimorar os dados recebidos por meio dos serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilação de dados de um banco de dados de terceiros. O Experience Platform pode se conectar a diferentes tipos de bancos de dados, como bancos de dados relacionais, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Amazon Redshift].

## Configure sua origem [!DNL Amazon Redshift] para o Experience Platform no Azure {#azure}

Siga as etapas abaixo para saber como configurar sua conta do [!DNL Amazon Redshift] para o Experience Platform no Azure.

### INCLUO NA LISTA DE PERMISSÕES de endereços IP

Você deve adicionar endereços IP específicos da região ao seu incluo na lista de permissões antes de conectar suas fontes à Experience Platform no Azure. Para obter mais informações, leia o manual sobre [sobre como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform no Azure](../../ip-address-allow-list.md) para obter mais informações.

## Configure sua origem do [!DNL Amazon Redshift] para o Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).

### INCLUO NA LISTA DE PERMISSÕES de endereços IP para conexão no AWS

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform no AWS. Para obter mais informações, leia o manual sobre [sobre como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform no AWS](../../ip-address-allow-list.md) para obter mais informações.

## Conectar o [!DNL Amazon Redshift] ao Experience Platform usando APIs

- [Conectar o Amazon Redshift ao Experience Platform usando a API do Serviço de fluxo](../../tutorials/api/create/databases/redshift.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar o [!DNL Amazon Redshift] ao Experience Platform usando a interface

- [Criar uma conexão de origem do Amazon Redshift na interface do usuário](../../tutorials/ui/create/databases/redshift.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
