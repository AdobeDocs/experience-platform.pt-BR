---
title: Visão geral do Google BigQuery Source Connector
description: Saiba como conectar o Google BigQuery ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# [!DNL Google BigQuery] origem

>[!IMPORTANT]
>
>A origem [!DNL Google BigQuery] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Leia este documento para obter as etapas de pré-requisito que você precisa concluir para conectar com êxito sua conta do [!DNL Google BigQuery] ao Adobe Experience Platform no Azure ou no Amazon Web Services (AWS).

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para obter a configuração de pré-requisitos que você deve concluir para poder conectar sua conta do [!DNL Google BigQuery] à Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform no Azure ou no Amazon Web Services (AWS). Para obter mais informações, leia o manual sobre [sobre como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform no Azure e no AWS](../../ip-address-allow-list.md) para obter mais informações.

### Autenticar para o Experience Platform no Azure {#azure}

Você deve fornecer as credenciais a seguir para conectar sua conta do [!DNL Google BigQuery] à Experience Platform no Azure.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para autenticar usando uma combinação do OAuth 2.0 e a autenticação básica, forneça os valores apropriados para as credenciais a seguir.

| Credencial | Descrição |
| --- | --- |
| `project` | O projeto é a entidade organizacional básica dos recursos do [!DNL Google Cloud], incluindo o [!DNL Google BigQuery]. |
| `clientID` | A ID do cliente é metade das suas credenciais do OAuth 2.0 [!DNL Google BigQuery]. |
| `clientSecret` | O segredo do cliente é a outra metade das credenciais do OAuth 2.0 do [!DNL Google BigQuery]. |
| `refreshToken` | O token de atualização permite obter novos tokens de acesso para a API. Os tokens de acesso têm duração limitada e podem expirar durante o curso do projeto. Você pode usar o token de atualização para autenticar e solicitar tokens de acesso subsequentes para seu projeto quando necessário. |
| `largeResultsDataSetId` | (Opcional) A ID do conjunto de dados [!DNL Google BigQuery] pré-criada que é necessária para habilitar o suporte para grandes conjuntos de resultados. |

Para obter instruções detalhadas sobre como gerar credenciais OAuth 2.0 para APIs [!DNL Google], consulte o [[!DNL Google] guia de autenticação do OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) a seguir.

>[!TAB Autenticação de serviço]

Para autenticar usando a autenticação de serviço, forneça os valores apropriados para as credenciais a seguir.

**Observação**: sua conta de serviço deve ter permissões suficientes, como **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** e **[!DNL BigQuery Data Owner]**, para ser autenticada com êxito com a autenticação de serviço.

| Credencial | Descrição |
| --- | --- |
| `projectId` | A ID do [!DNL Google BigQuery] que você deseja consultar. |
| `keyFileContent` | O arquivo de chave usado para autenticar a conta de serviço. Você pode recuperar este valor do [[!DNL Google Cloud service accounts] painel](https://console.cloud.google.com). O conteúdo principal do arquivo está no formato JSON. Você deve codificar isso em [!DNL Base64] ao autenticar no Experience Platform. |
| `largeResultsDataSetId` | (Opcional) A ID do conjunto de dados [!DNL Google BigQuery] pré-criada que é necessária para habilitar o suporte para grandes conjuntos de resultados. |

Para obter mais informações sobre o uso de contas de serviço no [!DNL Google BigQuery], leia o manual sobre [uso de contas de serviço no [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

### Autenticar para o Experience Platform no AWS {#aws}

Você deve fornecer as credenciais a seguir para conectar sua conta do [!DNL Google BigQuery] ao Experience Platform no AWS.

| Credencial | Descrição |
| --- | --- |
| `projectId` | A ID do [!DNL Google BigQuery] que você deseja consultar. |
| `keyFileContent` | O arquivo de chave usado para autenticar a conta de serviço. Você pode recuperar este valor do [[!DNL Google Cloud service accounts] painel](https://console.cloud.google.com). O conteúdo principal do arquivo está no formato JSON. Você deve codificar isso em [!DNL Base64] ao autenticar no Experience Platform. |
| `datasetId` | A ID do conjunto de dados [!DNL Google BigQuery]. Essa ID representa onde as tabelas de dados estão localizadas. |

## Conectar [!DNL Google BigQuery] ao Experience Platform

A documentação abaixo fornece informações sobre como conectar o [!DNL Google BigQuery] ao Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Crie uma conexão básica do Google BigQuery usando a API de serviço de fluxo](../../tutorials/api/create/databases/bigquery.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

### Uso da interface

- [Criar uma conexão de origem do Google BigQuery na interface](../../tutorials/ui/create/databases/bigquery.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
