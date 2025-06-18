---
title: Visão geral do Azure Synapse Analytics Source Connector
description: Saiba como conectar o Azure Synapse Analytics ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 4%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>A origem [!DNL Azure Synapse Analytics] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

[!DNL Azure Synapse Analytics] é um serviço de análise baseado em nuvem que unifica big data e data warehouse. Você pode assimilar, explorar, preparar e analisar dados usando SQL, [!DNL Spark] ou ferramentas em tempo real — tudo sem mover os dados.

Você pode usar a fonte [!DNL Azure Synapse Analytics] para conectar sua conta e trazer seus dados para a Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para concluir a configuração de pré-requisito antes de conectar sua conta do [!DNL Azure Synapse Analytics] à Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

### Configurar permissões

Para conectar sua conta de origem ao Experience Platform, sua conta deve ter as duas permissões a seguir ativadas:

* **Exibir fontes**
* **Gerenciar fontes**

Se você não tiver essas permissões, entre em contato com o administrador do produto para solicitar acesso. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/ui/overview.md).

### Autenticar no Experience Platform

Você pode usar a autenticação de chave de conta ou a autenticação de chave de entidade de serviço para conectar o [!DNL Azure Synapse Analytics] ao Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Forneça valores para as credenciais a seguir para conectar o banco de dados do [!DNL Azure Synapse Analytics] à Experience Platform usando a autenticação de chave de conta.

| Credencial | Descrição |
| --- | --- |
| String de conexão | Esta é a **cadeia de conexão** usada para autenticação com [!DNL Azure Synapse Analytics]. O formato padrão é: `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. Você deve substituir os espaços reservados pelos detalhes reais da conexão. |
| ID de especificação da conexão | A **especificação de conexão** fornece as propriedades do conector de uma fonte de dados. Isso inclui detalhes como especificações de autenticação e requisitos para criar conexões de **base** e **origem**. Para [!DNL Azure Synapse Analytics], a ID de especificação da conexão é: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Observação:** esta credencial só é necessária durante a conexão via APIs. |

>[!TAB Autenticação da chave da entidade de serviço]

Para recuperar suas credenciais para autenticação da chave da entidade de serviço, navegue até [[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home) e recupere valores para o seguinte:

* ID do aplicativo
* Nome de exibição
* Segredo
* ID do locatário

Em seguida, navegue até a [[!DNL Azure Synapse Analytics] instância](https://azure.microsoft.com/en-ca/products/synapse-analytics) e selecione a opção para criar um usuário a partir de um provedor externo. Aqui, forneça as permissões apropriadas para a entidade de serviço no esquema. **OBSERVAÇÃO:**: você deve incluir &quot;SELECT&quot;, pois ele é necessário para a visualização do esquema, semelhante a &quot;COPY&quot;. Por exemplo, um comando de exemplo pode ser:

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

Forneça valores para as credenciais a seguir para conectar o banco de dados do [!DNL Azure Synapse Analytics] à Experience Platform usando a autenticação de chave de entidade de serviço.

| Credencial | Descrição |
| --- | --- |
| Servidor | O nome de domínio totalmente qualificado do seu ponto de extremidade SQL [!DNL Azure Synapse Analytics]. |
| Banco de dados | O nome do banco de dados específico no espaço de trabalho [!DNL Azure Synapse Analytics]. |
| Locatário | A ID de locatário do [!DNL Azure Active Directory] associada à sua assinatura do [!DNL Azure]. |
| ID principal de serviço | A ID do cliente de um aplicativo [!DNL Azure Active Directory]. |
| Chave principal de serviço | O segredo do cliente ou a senha associada à entidade de serviço. |
| ID de especificação da conexão | A **especificação de conexão** fornece as propriedades do conector de uma fonte de dados. Isso inclui detalhes como especificações de autenticação e requisitos para criar conexões de **base** e **origem**. Para [!DNL Azure Synapse Analytics], a ID de especificação da conexão é: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Observação:** esta credencial só é necessária durante a conexão via APIs. |

Para obter mais informações, leia a [[!DNL Azure] documentação sobre gerenciamento de identidades para [!DNL Azure Synapse Analytics]](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity).

>[!ENDTABS]

## Conectar o [!DNL Azure Synapse Analytics] ao Experience Platform usando APIs

* [Conectar  [!DNL Azure Synapse Analytics]  ao Experience Platform usando a API de Serviço de Fluxo](../../tutorials/api/create/databases/synapse-analytics.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar o [!DNL Azure Synapse Analytics] ao Experience Platform usando a interface

* [Conectar [!DNL Azure Synapse Analytics] ao Experience Platform na interface](../../tutorials/ui/create/databases/synapse-analytics.md)
* [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)

