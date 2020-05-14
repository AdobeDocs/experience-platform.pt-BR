---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector SQL Server usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Criar um conector do Microsoft SQL Server usando a API do Serviço de Fluxo

>[!NOTE]
>O conector do Microsoft SQL Server está em beta. Os recursos e a documentação estão sujeitos a alterações.

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para orientá-lo pelas etapas para conectar a Experience Platform a um Microsoft SQL Server (a seguir denominado &quot;SQL Server&quot;).

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): A Plataforma de experiência permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao SQL Server usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

Para se conectar ao SQL Server, é necessário fornecer a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão associada à sua conta do SQL Server. |

Consulte [este documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server) para obter mais informações sobre como iniciar o SQL Server.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos na plataforma Experience, incluindo os pertencentes ao Serviço de Fluxo, são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Pesquisar especificações de conexão

Para criar uma conexão com o SQL Server, um conjunto de especificações de conexão do SQL Server deve existir no Serviço de Fluxo. A primeira etapa na conexão da Plataforma ao SQL Server é recuperar essas especificações.

**Formato da API**

Cada fonte disponível tem seu próprio conjunto exclusivo de especificações de conexão para descrever propriedades do conector, como requisitos de autenticação. O envio de uma solicitação GET para o ponto de extremidade `/connectionSpecs` retornará as especificações de conexão para todas as fontes disponíveis. Você também pode incluir o query `property=name=="sql-server"` para obter informações especificamente para o SQL Server.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="sql-server"
```

**Solicitação**

A solicitação a seguir recupera as especificações de conexão do SQL Server.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="sql-server"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna as especificações de conexão do SQL Server, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão básica.

```json
{
    "items": [
        {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "name": "sql-server",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Connection String Based Authentication",
                    "type": "connectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to SQL Server database",
                        "properties": {
                            "connectionString": {
                                "type": "string",
                                "description": "connection string to connect to any SQL Server database.",
                                "format": "password",
                                "pattern": "^(Data Source=)(.*)(;Initial Catalog=)(.*)(;Integrated Security=)(.*)(;User ID=)(.*)(;Password=)(.*)(;)",
                                "examples": [
                                    "Data Source=<servername>\\<instance name if using named instance>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;"
                                ]
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Criar uma conexão básica

Uma conexão básica especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão básica é necessária por conta do SQL Server, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

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
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "version": "1.0"
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão associada à autenticação do SQL Server. |
| `connectionSpec.id` | A especificação de conexão (`id`) coletada na etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão básica recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão básica do SQL Server usando a API do Serviço de Fluxo e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão básica no próximo tutorial à medida que aprende a [explorar bancos de dados ou sistemas NoSQL usando a API](../../explore/database-nosql.md)do Serviço de Fluxo.
