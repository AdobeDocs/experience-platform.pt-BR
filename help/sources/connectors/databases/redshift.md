---
title: Visão geral do Amazon Redshift Source Connector
description: Saiba como conectar o Amazon Redshift ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: 84d09038ded1f35269ebf67c6bc1a5dacaafe4ac
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# [!DNL Amazon Redshift] origem

>[!IMPORTANT]
>
>- A origem [!DNL Amazon Redshift] está disponível no catálogo de origens para usuários que compraram o Real-Time CDP Ultimate.
>
>- Agora você pode usar a origem [!DNL Amazon Redshift] ao executar o Adobe Experience Platform no Amazon Web Services (AWS). O Experience Platform em execução no AWS está atualmente disponível para um número limitado de clientes. Para saber mais sobre a infraestrutura de Experience Platform compatível, consulte a [visão geral de várias nuvens do Experience Platform](../../../landing/multi-cloud.md).


O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um banco de dados de terceiros. A Platform pode se conectar a diferentes tipos de bancos de dados, como bancos de dados relacionais, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Amazon Redshift].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Configurar a origem do [!DNL Amazon Redshift] para o Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform executadas no Amazon Web Services (AWS). O Experience Platform em execução no AWS está atualmente disponível para um número limitado de clientes. Para saber mais sobre a infraestrutura de Experience Platform compatível, consulte a [visão geral de várias nuvens do Experience Platform](../../../landing/multi-cloud.md).

Adicione os seguintes endereços IP ao seu Experience Platform no Amazon Web Services (AWS) para conectar sua conta do [!DNL Amazon Redshift] ao incluir na lista de permissões:

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

## Conectar [!DNL Amazon Redshift] à plataforma usando APIs

- [Criar uma conexão básica do Amazon Redshift usando a API do serviço de fluxo](../../tutorials/api/create/databases/redshift.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Amazon Redshift] à Plataforma usando a interface

- [Criar uma conexão de origem do Amazon Redshift na interface do usuário](../../tutorials/ui/create/databases/redshift.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
