---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector IBM DB2 usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: c4162d88a688ce2028de08b63e7b7eab954a0e29

---


# Criar um conector IBM DB2 usando a API de Serviço de Fluxo

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar o IBM DB2 (a seguir denominado &quot;DB2&quot;) à plataforma Experience.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): A Plataforma de experiência permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao DB2 usando a API de Serviço de Fluxo.

| Credencial | Descrição |
| ---------- | ----------- |
| `server` | O nome do servidor DB2. Você pode especificar o número da porta após o nome do servidor delimitado por dois pontos. Por exemplo: server:port. |
| `database` | O nome do banco de dados DB2. |
| `username` | O nome de usuário usado para conexão com o banco de dados DB2. |
| `password` | A senha da conta de usuário especificada para o nome de usuário. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para DB2 é `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

Para obter mais informações sobre a introdução, consulte [este documento](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)DB2.

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

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente um conector é necessário por conta DB2, pois pode ser usado para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão DB2, sua ID exclusiva de especificação de conexão deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para DB2 é `09182899-b429-40c9-a15a-bf3ddbc8ced7`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "DB2 connection",
        "description": "DB2 test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão associada à sua conta DB2. |
| `connectionSpec.id` | A ID da especificação de conexão DB2: `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão IBM DB2 usando a API de Serviço de Fluxo e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API](../../explore/database-nosql.md)do Serviço de Fluxo.
