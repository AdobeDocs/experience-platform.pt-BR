---
title: Visão geral do conector de origem do Google BigQuery
description: Saiba como conectar o Google BigQuery ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# [!DNL Google BigQuery] origem

>[!IMPORTANT]
>
>A variável [!DNL Google BigQuery] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] O fornece suporte para assimilação de dados de um banco de dados de terceiros. A Platform pode se conectar a diferentes tipos de bancos de dados, como bancos de dados relacionais, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Google BigQuery].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos

A seção a seguir fornece mais informações sobre a configuração de pré-requisitos necessária antes que você possa criar um [!DNL Google BigQuery] conexão de origem.

### Gerar o [!DNL Google BigQuery] credenciais

Para conectar [!DNL Google BigQuery] Para o Platform, é necessário gerar valores para as seguintes credenciais:

| Credencial | Descrição |
| ---------- | ----------- |
| `project` | O projeto é a entidade organizacional de nível básico do [!DNL Google Cloud] recursos, incluindo [!DNL Google BigQuery]. |
| `clientID` | A ID do cliente é metade de sua [!DNL Google BigQuery] Credenciais do OAuth 2.0. |
| `clientSecret` | O segredo do cliente é a outra metade do seu [!DNL Google BigQuery] Credenciais do OAuth 2.0. |
| `refreshToken` | O token de atualização permite obter novos tokens de acesso para a API. Os tokens de acesso têm duração limitada e podem expirar durante o curso do projeto. Você pode usar o token de atualização para autenticar e solicitar tokens de acesso subsequentes para o seu projeto quando necessário. |
| `largeResultsDataSetId` | O pré-criado  [!DNL Google BigQuery] a ID do conjunto de dados que é necessária para habilitar o suporte para grandes conjuntos de resultados. |

Para obter instruções detalhadas sobre como gerar credenciais do OAuth 2.0 para [!DNL Google] APIs, consulte o seguinte [[!DNL Google] Guia de autenticação do OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Conectar [!DNL Google BigQuery] para a Platform

A documentação abaixo fornece informações sobre como se conectar [!DNL Google BigQuery] para a Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Crie uma conexão básica do Google BigQuery usando a API de serviço de fluxo](../../tutorials/api/create/databases/bigquery.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

### Uso da interface

- [Criar uma conexão de origem do Google BigQuery na interface](../../tutorials/ui/create/databases/bigquery.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
