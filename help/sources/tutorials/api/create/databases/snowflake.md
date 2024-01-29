---
title: Criar uma conexão base de Snowflake usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Snowflake usando a API do serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---

# Criar um [!DNL Snowflake] conexão básica usando o [!DNL Flow Service] API

>[!IMPORTANT]
>
>A variável [!DNL Snowflake] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Use o tutorial a seguir para saber como criar uma conexão base para [!DNL Snowflake] usando o [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Snowflake] usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

Você deve fornecer valores para as seguintes propriedades de credencial para autenticar seu [!DNL Snowflake] origem.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

| Credencial | Descrição |
| ---------- | ----------- |
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes [!DNL Snowflake] organizações internacionais. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Para obter mais informações sobre nomes de conta, leia a [!DNL Snowflake] documentação sobre [identificadores de conta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | A variável [!DNL Snowflake] O warehouse gerencia o processo de execução da consulta para o aplicativo. Each [!DNL Snowflake] O warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a Platform. |
| `database` | A variável [!DNL Snowflake] contém os dados que você deseja trazer para a Platform. |
| `username` | O nome de usuário para o [!DNL Snowflake] conta. |
| `password` | A senha para o [!DNL Snowflake] conta de usuário. |
| `role` | A função de controle de acesso padrão a ser usada na [!DNL Snowflake] sessão. A função deve ser uma função existente que já foi atribuída ao usuário especificado. A função padrão é `PUBLIC`. |
| `connectionString` | A cadeia de conexão usada para se conectar ao [!DNL Snowflake] instância. O padrão da cadeia de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticação de par de chaves]

Para usar a autenticação de par de chaves, você deve gerar um par de chaves RSA de 2048 bits e fornecer os seguintes valores ao criar uma conta para o [!DNL Snowflake] origem.

| Credencial | Descrição |
| --- | --- |
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes [!DNL Snowflake] organizações internacionais. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Para obter mais informações sobre nomes de conta, leia a [!DNL Snowflake] documentação sobre [identificadores de conta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | O nome de usuário do seu [!DNL Snowflake] conta. |
| `privateKey` | A variável [!DNL Base64-]chave privada codificada de seu [!DNL Snowflake] conta. Você pode gerar chaves privadas criptografadas ou não. Se você estiver usando uma chave privada criptografada, também deverá fornecer uma senha de chave privada ao autenticar no Experience Platform. |
| `privateKeyPassphrase` | A senha da chave privada é uma camada adicional de segurança que deve ser usada ao autenticar com uma chave privada criptografada. Não é necessário fornecer a senha se você estiver usando uma chave privada não criptografada. |
| `database` | A variável [!DNL Snowflake] banco de dados que contém os dados que você deseja assimilar no Experience Platform. |
| `warehouse` | A variável [!DNL Snowflake] O warehouse gerencia o processo de execução da consulta para o aplicativo. Each [!DNL Snowflake] o warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para o Experience Platform. |

Para obter mais informações sobre esses valores, consulte a [[!DNL Snowflake] guia de autenticação de par de chaves](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Você deve definir o `PREVENT_UNLOAD_TO_INLINE_URL` sinalizador para `FALSE` para permitir o descarregamento de dados do [!DNL Snowflake] banco de dados para Experience Platform.

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Snowflake] credenciais de autenticação como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB ConnectionString]

+++Solicitação

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

+++

+++Resposta

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB Autenticação de par de chaves com chave privada criptografada]

+++Solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
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
| `auth.params.account` | O nome do seu [!DNL Snowflake] conta. |
| `auth.params.username` | O nome de usuário associado à [!DNL Snowflake] conta. |
| `auth.params.database` | A variável [!DNL Snowflake] banco de dados de onde os dados serão obtidos. |
| `auth.params.privateKey` | A variável [!DNL Base64-]chave privada criptografada codificada de sua [!DNL Snowflake] conta. |
| `auth.params.privateKeyPassphrase` | A senha que corresponde à sua chave privada. |
| `auth.params.warehouse` | A variável [!DNL Snowflake] depósito que você está usando. |
| `connectionSpec.id` | A variável [!DNL Snowflake] ID da especificação de conexão: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Resposta

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB Autenticação de par de chaves com chave privada não criptografada]

+++Solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
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
| `auth.params.account` | O nome do seu [!DNL Snowflake] conta. |
| `auth.params.username` | O nome de usuário associado à [!DNL Snowflake] conta. |
| `auth.params.database` | A variável [!DNL Snowflake] banco de dados de onde os dados serão obtidos. |
| `auth.params.privateKey` | A variável [!DNL Base64-]chave privada não criptografada codificada de seu [!DNL Snowflake] conta. |
| `auth.params.warehouse` | A variável [!DNL Snowflake] depósito que você está usando. |
| `connectionSpec.id` | A variável [!DNL Snowflake] ID da especificação de conexão: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Resposta

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

Ao seguir este tutorial, você criou um [!DNL Snowflake] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Platform usando o [!DNL Flow Service] API](../../collect/database-nosql.md)
