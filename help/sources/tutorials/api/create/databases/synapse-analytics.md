---
title: Conectar O Azure Synapse Analytics Ao Experience Platform Usando A API Do Serviço De Fluxo
description: Saiba como conectar sua conta do Azure Synapse Analytics ao Experience Platform usando APIs.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 3%

---

# Conectar o [!DNL Azure Synapse Analytics] ao Experience Platform usando a API [!DNL Flow Service]

>[!IMPORTANT]
>
>A origem [!DNL Azure Synapse Analytics] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Leia este guia para saber como conectar sua conta do [!DNL Azure Synapse Analytics] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Azure Synapse Analytics] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Leia a [[!DNL Azure Synapse Analytics] visão geral](../../../../connectors/databases/synapse-analytics.md#prerequisites) para obter informações sobre autenticação.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Conectar [!DNL Azure Synapse Analytics] ao Experience Platform

Leia o seguinte para saber como criar uma conexão básica e conectar sua conta do [!DNL Azure Synapse Analytics] à Experience Platform.

### Criar uma conexão básica

Uma **conexão base** armazena informações importantes que vinculam seu sistema de origem à Adobe Experience Platform. Isso inclui:

* Credenciais de autenticação da sua origem
* O status atual da conexão
* Uma **ID de conexão básica** exclusiva

A **ID da conexão base** permite procurar e explorar arquivos da sua origem, ajudando você a identificar quais itens serão assimilados, juntamente com seus tipos de dados e formatos.

Para criar uma ID de conexão base, envie uma solicitação POST para o ponto de extremidade `/connections`, incluindo suas credenciais de autenticação [!DNL Azure Synapse Analytics] nos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticação Baseada em Cadeia de Conexão]

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Azure Synapse Analytics] usando autenticação baseada em cadeia de conexão.

+++Exibir solicitação de exemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão usada para se conectar a [!DNL Azure Synapse Analytics]. O padrão da cadeia de conexão [!DNL Azure Synapse Analytics] é `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Azure Synapse Analytics] é: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Exibir resposta de exemplo

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB Autenticação Baseada na Chave da Entidade de Serviço]

A solicitação a seguir cria uma conexão base para [!DNL Azure Synapse Analytics] usando a autenticação baseada na chave da entidade de serviço.

**Solicitação**

+++Exibir solicitação de exemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| Credencial | Descrição |
| --- | --- |
| `auth.params.server` | O nome de domínio totalmente qualificado do seu ponto de extremidade SQL [!DNL Azure Synapse Analytics]. |
| `auth.params.database` | O nome do banco de dados específico no espaço de trabalho [!DNL Azure Synapse Analytics]. |
| `auth.params.tenant` | A ID de locatário do [!DNL Azure Active Directory] associada à sua assinatura do [!DNL Azure]. |
| `auth.params.servicePrincipalId` | A ID do cliente de um aplicativo [!DNL Azure Active Directory]. |
| `auth.params.servicePrincipalKey` | O segredo do cliente ou a senha associada à entidade de serviço. |
| `connectSpec.id` | A ID de especificação de conexão de [!DNL Azure Synapse Analytics]. |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Exibir resposta de exemplo

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Azure Synapse Analytics] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
