---
keywords: Experience Platform; home; tópicos populares; BigQuery; bigquery; Google BigQuery; google bigquery
solution: Experience Platform
title: Visão geral do Google BigQuery Source Connector
topic-legacy: overview
description: Saiba como conectar o Google BigQuery à Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 9d68e54baa894ebeff4603c7df01a1fe42aa217f
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Conector (Beta) [!DNL Google BigQuery]

>[!NOTE]
>
>O [!DNL Google BigQuery] está em beta. Consulte a [Visão geral das Fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] O oferece suporte para assimilar dados de um banco de dados de terceiros. A plataforma pode se conectar a diferentes tipos de bancos de dados, como relacional, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Google BigQuery].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos

A seção a seguir fornece mais informações sobre a configuração de pré-requisito necessária antes que você possa criar uma conexão de origem [!DNL Google BigQuery].

### Gerar suas credenciais [!DNL Google BigQuery]

Para conectar [!DNL Google BigQuery] à Plataforma, você precisa gerar valores para as seguintes credenciais:

| Credencial | Descrição |
| ---------- | ----------- |
| `project` | O projeto é a entidade de organização de nível base para seus recursos [!DNL Google Cloud], incluindo [!DNL Google BigQuery]. |
| `clientID` | A ID do cliente é a metade de suas credenciais do OAuth 2.0.[!DNL Google BigQuery] |
| `clientSecret` | O segredo do cliente é a outra metade de suas credenciais do OAuth 2.0.[!DNL Google BigQuery] |
| `refreshToken` | O token de atualização permite obter novos tokens de acesso para sua API. Os tokens de acesso têm vida limitada e podem expirar durante o andamento do projeto. Você pode usar o token de atualização para autenticar e solicitar tokens de acesso subsequentes para o seu projeto, quando necessário. |

Para obter instruções detalhadas sobre como gerar credenciais do OAuth 2.0 para [!DNL Google] APIs, consulte o seguinte [[!DNL Google] Guia de autenticação do OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Conectar [!DNL Google BigQuery] à plataforma

A documentação abaixo fornece informações sobre como se conectar [!DNL Google BigQuery] à Plataforma usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem do Google BigQuery usando a API de Serviço de Fluxo](../../tutorials/api/create/databases/bigquery.md)
- [Explorar um sistema de banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/explore/database-nosql.md)
- [Coletar dados de um banco de dados usando a API do Serviço de Fluxo](../../tutorials/api/collect/database-nosql.md)

### Uso da interface do usuário

- [Criar uma conexão de origem do Google BigQuery na interface do usuário](../../tutorials/ui/create/databases/bigquery.md)
- [Configurar um fluxo de dados para uma conexão de banco de dados na interface do usuário](../../tutorials/ui/dataflow/databases.md)
