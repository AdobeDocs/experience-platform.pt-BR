---
title: Criar uma conexão base de Snowflake usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Snowflake usando a API do serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 669b47753a9c9400f22aa81d08a4d25bb5e414c5
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 5%

---

# Criar um [!DNL Snowflake] conexão básica usando o [!DNL Flow Service] API

>[!IMPORTANT]
>
>A variável [!DNL Snowflake] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Snowflake] usando o [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Snowflake] usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com [!DNL Snowflake], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `account` | O nome completo da conta associado à [!DNL Snowflake] conta. Um [!DNL Snowflake] o nome da conta inclui o nome da conta, a região e a plataforma de nuvem. Por exemplo, `cj12345.east-us-2.azure`. Para obter mais informações sobre nomes de conta, consulte esta [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | A variável [!DNL Snowflake] O warehouse gerencia o processo de execução da consulta para o aplicativo. Each [!DNL Snowflake] O warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a Platform. |
| `database` | A variável [!DNL Snowflake] contém os dados que você deseja trazer para a Platform. |
| `username` | O nome de usuário para o [!DNL Snowflake] conta. |
| `password` | A senha para o [!DNL Snowflake] conta de usuário. |
| `role` | A função de controle de acesso padrão a ser usada na [!DNL Snowflake] sessão. A função deve ser uma função existente que já foi atribuída ao usuário especificado. A função padrão é `PUBLIC`. |
| `connectionString` | A cadeia de conexão usada para se conectar ao [!DNL Snowflake] instância. O padrão da cadeia de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Snowflake] é `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Para obter mais informações sobre a introdução, consulte esta [[!DNL Snowflake] documento](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!NOTE]
>
>Você deve definir o `PREVENT_UNLOAD_TO_INLINE_URL` sinalizador para `FALSE` para permitir o descarregamento de dados do [!DNL Snowflake] banco de dados para Experience Platform.

## Crie uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Snowflake] credenciais de autenticação como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Snowflake]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
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
| `auth.params.connectionString` | A cadeia de conexão usada para se conectar ao [!DNL Snowflake] instância. O padrão da cadeia de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | A variável [!DNL Snowflake] ID da especificação de conexão: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Ao seguir este tutorial, você criou um [!DNL Snowflake] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Platform usando o [!DNL Flow Service] API](../../collect/database-nosql.md)
