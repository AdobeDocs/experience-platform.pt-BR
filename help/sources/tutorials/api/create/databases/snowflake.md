---
keywords: Experience Platform, home, tópicos populares, Snowflake, snowflake
solution: Experience Platform
title: Criar uma conexão base do Snowflake usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Snowflake usando a API de Serviço de Fluxo.
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 0928da0ad15ce23d3677fec7b9866d079f3db407
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 2%

---

# Crie um [!DNL Snowflake] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Snowflake] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Snowflake] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Snowflake], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `account` | O nome completo da conta associado ao [!DNL Snowflake] conta. Um [!DNL Snowflake] o nome da conta inclui o nome da conta, a região e a plataforma da nuvem. Por exemplo, `cj12345.east-us-2.azure`. Para obter mais informações sobre nomes de conta, consulte esta seção [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | O [!DNL Snowflake] warehouse gerencia o processo de execução de consulta do aplicativo. Cada [!DNL Snowflake] O warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a Platform. |
| `database` | O [!DNL Snowflake] O banco de dados contém os dados que você deseja trazer para a Plataforma. |
| `username` | O nome de usuário para a [!DNL Snowflake] conta. |
| `password` | A senha do [!DNL Snowflake] conta do usuário. |
| `connectionString` | A cadeia de conexão usada para se conectar ao seu [!DNL Snowflake] instância. O padrão da string de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Snowflake] é `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Para obter mais informações sobre a introdução, consulte esta seção [[!DNL Snowflake] documento](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Snowflake] credenciais de autenticação como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Snowflake]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Snowflake base connection",
        "description": "Snowflake base connection",
        "auth": {
            "specName": "Basic Authentication for Snowflake,
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão usada para se conectar ao seu [!DNL Snowflake] instância. O padrão da string de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | O [!DNL Snowflake] ID de especificação de conexão: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Ao seguir este tutorial, você criou um [!DNL Snowflake] conexão usando o [!DNL Flow Service] e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
