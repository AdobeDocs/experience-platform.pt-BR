---
keywords: Experience Platform;home;popular topics;Microsoft SQL;microsoft sql;sql server;SQL server
solution: Experience Platform
title: Criar um conector SQL Server usando a API de Serviço de Fluxo
topic: overview
description: Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar o Experience Platform a um Microsoft SQL Server (a seguir denominado "SQL Server").
translation-type: tm+mt
source-git-commit: 5959d4344ec1c16542de045899ce74beb39a7bc4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---


# Criar um conector [!DNL Microsoft] SQL Server usando a [!DNL Flow Service] API

>[!NOTE]
>
>O conector [!DNL Microsoft] SQL Server está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [!DNL Flow Service] API para guiá-lo pelas etapas para se conectar [!DNL Experience Platform] [!DNL Microsoft] a um SQL Server (a seguir denominado &quot;SQL Server&quot;).

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao SQL Server usando a [!DNL Flow Service] API.

### Reunir credenciais obrigatórias

Para se conectar ao SQL Server, é necessário fornecer a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão associada à sua conta do SQL Server. O padrão da cadeia de conexão do SQL Server é: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |
| `connectionSpec.id` | A ID usada para gerar uma conexão. A ID de especificação de conexão fixa para o SQL Server é `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

Para obter mais informações sobre como obter uma cadeia de conexão, consulte [este documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server)do SQL Server.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta do SQL Server, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão com o SQL Server, sua ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação de POST. A ID de especificação de conexão do SQL Server é `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for sql-server",
        "description": "Base connection for sql-server",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};"
            }
        },
        "connectionSpec": {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "version": "1.0"
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão associada à sua conta do SQL Server. O padrão da cadeia de conexão do SQL Server é: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |
| `connectionSpec.id` | A ID de especificação de conexão para o SQL Server é: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu banco de dados no próximo tutorial.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão do SQL Server usando a [!DNL Flow Service] API e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar bancos de dados ou sistemas NoSQL usando a API](../../explore/database-nosql.md)do Serviço de Fluxo.
