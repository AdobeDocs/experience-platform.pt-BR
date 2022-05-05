---
keywords: Experience Platform; home; tópicos populares; BigQuery; bigquery; Google BigQuery; google bigquery
solution: Experience Platform
title: Visão geral do Google BigQuery Source Connector
topic-legacy: overview
description: Saiba como conectar o Google BigQuery ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: fa861e9740e05b4fcc4e8039bb288301d42b8357
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# (Beta) [!DNL Google BigQuery] conector

>[!NOTE]
>
>O [!DNL Google BigQuery] está em beta. Consulte a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] O oferece suporte para assimilar dados de um banco de dados de terceiros. A plataforma pode se conectar a diferentes tipos de bancos de dados, como relacional, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Google BigQuery].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos

A seção a seguir fornece mais informações sobre a configuração de pré-requisito necessária antes que você possa criar um [!DNL Google BigQuery] conexão de origem.

### Gere seu [!DNL Google BigQuery] credenciais

Para ligar [!DNL Google BigQuery] para Platform, você precisa gerar valores para as seguintes credenciais:

| Credencial | Descrição |
| ---------- | ----------- |
| `project` | O projeto é a entidade de organização de nível base para seu [!DNL Google Cloud] recursos, incluindo [!DNL Google BigQuery]. |
| `clientID` | A ID do cliente é metade de seu [!DNL Google BigQuery] Credenciais do OAuth 2.0. |
| `clientSecret` | O segredo do cliente é a outra metade de seu [!DNL Google BigQuery] Credenciais do OAuth 2.0. |
| `refreshToken` | O token de atualização permite obter novos tokens de acesso para sua API. Os tokens de acesso têm vida limitada e podem expirar durante o andamento do projeto. Você pode usar o token de atualização para autenticar e solicitar tokens de acesso subsequentes para o seu projeto, quando necessário. |

Para obter instruções detalhadas sobre como gerar credenciais do OAuth 2.0 para [!DNL Google] APIs, consulte o seguinte [[!DNL Google] Guia de autenticação do OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Connect [!DNL Google BigQuery] para a plataforma

A documentação abaixo fornece informações sobre como se conectar [!DNL Google BigQuery] para Plataforma usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão básica do Google BigQuery usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/bigquery.md)
- [Explorar tabelas de dados usando a API do Serviço de fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

### Uso da interface do usuário

- [Criar uma conexão de origem Google BigQuery na interface do usuário](../../tutorials/ui/create/databases/bigquery.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)
