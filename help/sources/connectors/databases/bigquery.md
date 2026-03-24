---
title: Visão geral do Google BigQuery Source Connector
description: Saiba como conectar o Google BigQuery ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 2136ace3e3c1157ac7bbfe56071af3dc9bc66fd6
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# [!DNL Google BigQuery] origem

>[!IMPORTANT]
>
>A origem [!DNL Google BigQuery] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Leia este documento para obter as etapas de pré-requisito que você precisa concluir para conectar com êxito sua conta do [!DNL Google BigQuery] ao Adobe Experience Platform no Azure ou no Amazon Web Services (AWS).

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para obter a configuração de pré-requisitos que você deve concluir para poder conectar sua conta do [!DNL Google BigQuery] à Experience Platform.

### INCLUO NA LISTA DE PERMISSÕES de endereços IP

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform no Azure ou no Amazon Web Services (AWS). Para obter mais informações, leia o guia sobre [Experience Platform de endereços IP para se conectar ao incluir na lista de permissões no Azure e no AWS](../../ip-address-allow-list.md) para obter mais informações.

### Autenticar para o Experience Platform no Azure {#azure}

Você deve fornecer as credenciais a seguir para conectar sua conta do [!DNL Google BigQuery] ao Experience Platform no Azure.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para autenticar usando uma combinação do OAuth 2.0 e a autenticação básica, forneça os valores apropriados para as credenciais a seguir.

| Credencial | Descrição |
| --- | --- |
| `project` | O projeto é a entidade organizacional básica dos recursos do [!DNL Google Cloud], incluindo o [!DNL Google BigQuery]. |
| `clientID` | A ID do cliente é metade das suas credenciais do OAuth 2.0 [!DNL Google BigQuery]. |
| `clientSecret` | O segredo do cliente é a outra metade das credenciais do OAuth 2.0 do [!DNL Google BigQuery]. |
| `refreshToken` | O token de atualização permite obter novos tokens de acesso para a API. Os tokens de acesso têm duração limitada e podem expirar durante o curso do projeto. Você pode usar o token de atualização para autenticar e solicitar tokens de acesso subsequentes para seu projeto quando necessário. Certifique-se de que o token de atualização inclua os seguintes [!DNL Google] escopos OAuth: <ul><li>`https://www.googleapis.com/auth/bigquery`</li><li>`https://www.googleapis.com/auth/cloud-platform`</li></ul> Esses escopos permitem que o Experience Platform envie trabalhos do BigQuery e leia dados do seu projeto configurado. |
| `largeResultsDataSetId` | (Opcional) A ID do conjunto de dados [!DNL Google BigQuery] pré-criada que é necessária para habilitar o suporte para grandes conjuntos de resultados.<ul><li>O `largeResultsDataSetId` deve se referir a um conjunto de dados [!DNL BigQuery] pré-criado usado para armazenar tabelas temporárias para conjuntos de resultados grandes.</li><li>O valor deve conter somente a ID do conjunto de dados (por exemplo, `marketing_temp_results`), não o nome qualificado do projeto (não use `my-project.marketing_temp_results`).</li><li>A localização (região) do conjunto de dados especificado em `largeResultsDataSetId` deve corresponder à localização das tabelas que estão sendo consultadas.</li><li>A conta usada pelo conector deve ter permissões para ler e gravar resultados temporários neste conjunto de dados. No mínimo, atribua a função [!DNL BigQuery Data Editor] no conjunto de dados especificado em `largeResultsDataSetId`.</li></ul> |

#### Funções IAM necessárias para a identidade [!DNL Google]

A identidade [!DNL Google] usada para gerar as credenciais OAuth (ID do cliente, segredo do cliente e refreshToken) deve ter as seguintes funções IAM no projeto de destino [!DNL Google Cloud]:

- [!DNL BigQuery Job User]
- [!DNL BigQuery Data Viewer]
- [!DNL BigQuery Read Session User]

Essas funções garantem que o Experience Platform possa criar e executar [!DNL BigQuery] trabalhos, ler dados das tabelas configuradas e usar sessões de leitura conforme exigido pelo conector. Verifique se essas funções são concedidas no mesmo projeto que contém os conjuntos de dados [!DNL BigQuery] que você planeja usar com a origem.

Para obter instruções detalhadas sobre como gerar credenciais OAuth 2.0 para APIs [!DNL Google], consulte o [[!DNL Google] guia de autenticação do OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) a seguir.

>[!TAB Autenticação de serviço]

Para autenticar usando a autenticação de serviço, forneça os valores apropriados para as credenciais a seguir.

**Observação**: sua conta de serviço deve ter permissões suficientes, como **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** e **[!DNL BigQuery Data Owner]**, para ser autenticada com êxito com a autenticação de serviço.

| Credencial | Descrição |
| --- | --- |
| `projectId` | A ID do [!DNL Google BigQuery] que você deseja consultar. |
| `keyFileContent` | O arquivo de chave usado para autenticar a conta de serviço. Você pode recuperar este valor do [[!DNL Google Cloud service accounts] painel](https://console.cloud.google.com). O conteúdo principal do arquivo está no formato JSON. Você deve codificar isso em [!DNL Base64] ao autenticar no Experience Platform. |
| `largeResultsDataSetId` | (Opcional) A ID do conjunto de dados [!DNL Google BigQuery] pré-criada que é necessária para habilitar o suporte para grandes conjuntos de resultados.<ul><li>O `largeResultsDataSetId` deve se referir a um conjunto de dados [!DNL BigQuery] pré-criado usado para armazenar tabelas temporárias para conjuntos de resultados grandes.</li><li>O valor deve conter somente a ID do conjunto de dados (por exemplo, `marketing_temp_results`), não o nome qualificado do projeto (não use `my-project.marketing_temp_results`).</li><li>A localização (região) do conjunto de dados especificado em `largeResultsDataSetId` deve corresponder à localização das tabelas que estão sendo consultadas.</li><li>A conta usada pelo conector deve ter permissões para ler e gravar resultados temporários neste conjunto de dados. No mínimo, atribua a função [!DNL BigQuery Data Editor] no conjunto de dados especificado em `largeResultsDataSetId`.</li></ul> |

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
