---
title: Criar uma conexão básica do Microsoft SQL Server usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a um Microsoft SQL Server usando a API do Serviço de fluxo.
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 5%

---

# Criar uma conexão base do SQL Server [!DNL Microsoft] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Leia este tutorial para saber como criar uma conexão base para [!DNL Microsoft SQL Server] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Microsoft SQL Server] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias {#gather-required-credentials}

Para se conectar a [!DNL Microsoft SQL Server], você deve fornecer a seguinte propriedade de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `connectionString` | A cadeia de conexão associada à sua conta [!DNL Microsoft SQL Server]. O padrão da cadeia de caracteres de conexão depende se você está usando o nome do servidor ou o nome da instância para a fonte de dados:<ul><li>Cadeia de conexão usando o nome do servidor: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Cadeia de conexão usando nome de instância:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Microsoft SQL Server] é `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |  |

Para obter mais informações sobre como obter uma cadeia de conexão, consulte este [[!DNL Microsoft SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Microsoft SQL Server] como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Microsoft SQL Server]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for sql-server",
      "description": "Base connection for sql-server",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword"
          }
      },
      "connectionSpec": {
          "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
          "version": "1.0"
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.connectionString` | A cadeia de conexão associada à sua conta [!DNL Microsoft SQL Server]. Leia a seção sobre [coleta de credenciais necessárias](#gather-required-credentials) para obter mais informações. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Microsoft SQL Server] é: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu banco de dados no próximo tutorial.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Microsoft SQL Server] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)