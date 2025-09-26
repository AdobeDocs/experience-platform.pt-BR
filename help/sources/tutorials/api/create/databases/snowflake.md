---
title: Conectar o Snowflake ao Experience Platform usando a API do Serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Snowflake usando a API do Serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 4%

---

# Conectar o [!DNL Snowflake] ao Experience Platform usando a API [!DNL Flow Service]

>[!IMPORTANT]
>
>A origem [!DNL Snowflake] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Leia este guia para saber como você pode conectar sua conta de origem do [!DNL Snowflake] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Snowflake] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Leia a [[!DNL Snowflake] visão geral](../../../../connectors/databases/snowflake.md#prerequisites) para obter informações sobre autenticação.

## Conectar [!DNL Snowflake] ao Experience Platform no Azure {#azure}

>[!WARNING]
>
>A autenticação básica (ou autenticação de chave de conta) para a origem [!DNL Snowflake] será substituída em novembro de 2025. Você deve migrar para a autenticação baseada em par de chaves para continuar usando a origem e assimilando dados do banco de dados para o Experience Platform. Para obter mais informações sobre a descontinuação, leia o [[!DNL Snowflake] manual de práticas recomendadas sobre como mitigar os riscos de comprometimento de credenciais](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

Leia as etapas abaixo para obter informações sobre como conectar sua origem do [!DNL Snowflake] à Experience Platform no Azure.

>[!NOTE]
>
>Você deve definir o sinalizador `PREVENT_UNLOAD_TO_INLINE_URL` como `FALSE` para permitir o descarregamento de dados do banco de dados [!DNL Snowflake] para o Experience Platform.

### Criar uma conexão base para [!DNL Snowflake] no Experience Platform no Azure {#azure-base}

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação do [!DNL Snowflake] como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB CadeiadaConexão]

+++Solicitação

A solicitação a seguir cria uma conexão base para [!DNL Snowflake]:

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
| `auth.params.connectionString` | A cadeia de conexão usada para se conectar à sua instância do [!DNL Snowflake]. O padrão da cadeia de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

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
| `auth.params.account` | O nome da sua conta [!DNL Snowflake]. |
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Snowflake]. |
| `auth.params.database` | O banco de dados [!DNL Snowflake] de onde os dados serão extraídos. |
| `auth.params.privateKey` | A chave privada criptografada codificada [!DNL Base64-] da sua conta [!DNL Snowflake]. |
| `auth.params.privateKeyPassphrase` | A senha que corresponde à sua chave privada. |
| `auth.params.warehouse` | O warehouse [!DNL Snowflake] que você está usando. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

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
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
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
| `auth.params.account` | O nome da sua conta [!DNL Snowflake]. |
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Snowflake]. |
| `auth.params.database` | O banco de dados [!DNL Snowflake] de onde os dados serão extraídos. |
| `auth.params.privateKey` | A chave privada não criptografada codificada [!DNL Base64-] da sua conta [!DNL Snowflake]. |
| `auth.params.warehouse` | O warehouse [!DNL Snowflake] que você está usando. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## Conectar o [!DNL Snowflake] ao Experience Platform no Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

Leia as etapas abaixo para obter informações sobre como conectar sua origem do [!DNL Snowflake] ao Experience Platform no AWS.

### Criar uma conexão base para [!DNL Snowflake] no Experience Platform no AWS {#aws-base}

**Formato da API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticação básica]

A solicitação a seguir cria uma conexão base para [!DNL Snowflake] para assimilar dados para o Experience Platform no AWS:

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
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.host` | A URL de host à qual sua conta do [!DNL Snowflake] se conecta. |
| `auth.params.port` | O número da porta usada por [!DNL Snowflake] ao se conectar a um servidor pela Internet. |
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Snowflake]. |
| `auth.params.database` | O banco de dados [!DNL Snowflake] de onde os dados serão extraídos. |
| `auth.params.password` | A senha associada à sua conta [!DNL Snowflake]. |
| `auth.params.warehouse` | O warehouse [!DNL Snowflake] que você está usando. |
| `auth.params.schema` | O nome do esquema associado ao banco de dados [!DNL Snowflake]. Você deve garantir que o usuário ao qual deseja conceder acesso ao banco de dados também tenha acesso a esse esquema. |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
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
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
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
| `auth.params.account` | O nome da sua conta [!DNL Snowflake]. |
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Snowflake]. |
| `auth.params.database` | O banco de dados [!DNL Snowflake] de onde os dados serão extraídos. |
| `auth.params.privateKey` | A chave privada não criptografada codificada [!DNL Base64-] da sua conta [!DNL Snowflake]. |
| `auth.params.warehouse` | O warehouse [!DNL Snowflake] que você está usando. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++


+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!ENDTABS]

Seguindo este tutorial, você criou uma conexão de base [!DNL Snowflake] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] ](../../collect/database-nosql.md)
