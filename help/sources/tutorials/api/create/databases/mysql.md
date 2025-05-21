---
title: Conectar o MySQL ao Experience Platform usando a API do Serviço de fluxo
description: Saiba como conectar seu banco de dados MySQL ao Experience Platform usando APIs.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 5%

---

# Conectar o [!DNL MySQL] ao Experience Platform usando a API [!DNL Flow Service]

Leia este guia para saber como conectar sua conta do [!DNL MySQL] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL MySQL] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Leia a [[!DNL MySQL] visão geral](../../../../connectors/databases/mysql.md#prerequisites) para obter informações sobre autenticação.

### Uso de APIs do Experience Platform

Leia o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md) para obter informações sobre como fazer chamadas com êxito para as APIs do Experience Platform.

## Conectar [!DNL MySQL] ao Experience Platform no Azure {#azure}

Leia as etapas abaixo para obter informações sobre como conectar sua conta do [!DNL MySQL] à Experience Platform no Azure.

### Criar uma conexão base para [!DNL MySQL] no Experience Platform no Azure {#azure-base}

Uma conexão básica vincula sua origem ao Experience Platform, armazenando detalhes de autenticação, status da conexão e uma ID exclusiva. Use essa ID para procurar arquivos de origem e identificar itens específicos a serem assimilados, incluindo seus tipos de dados e formatos.

**Formato da API**

```https
POST /connections
```

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` e forneça suas credenciais de autenticação [!DNL MySQL] como parte dos parâmetros de solicitação.

>[!BEGINTABS]

>[!TAB Autenticação baseada em cadeia de conexão]

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL MySQL] usando autenticação baseada em cadeia de conexão.

+++Exibir exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.connectionString` | A cadeia de conexão [!DNL MySQL] associada à sua conta. O padrão da cadeia de conexão [!DNL MySQL] é: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL MySQL]: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Exibir exemplo de resposta

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB Autenticação básica]

**Solicitação**

A solicitação a seguir cria uma conexão base para uma origem [!DNL MySQL] usando autenticação básica.

+++Exibir exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "DISABLED"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.server` | O nome ou IP do banco de dados [!DNL MySQL]. |
| `auth.params.database` | O nome do banco de dados. |
| `auth.params.username` | O nome de usuário que corresponde ao banco de dados. |
| `auth.params.password` | A senha que corresponde ao banco de dados. |
| `auth.params.sslMode` | O método pelo qual os dados são criptografados durante a transferência. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL MySQL] é: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Exibir exemplo de resposta

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## Conectar o [!DNL MySQL] ao Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

Leia as etapas abaixo para obter informações sobre como conectar sua conta do [!DNL MySQL] ao Experience Platform no AWS.

### Criar uma conexão base para [!DNL MySQL] no Experience Platform no AWS {#aws-base}

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL MySQL] se conectar ao Experience Platform no AWS.

+++Exibir exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.server` | O nome ou IP do banco de dados [!DNL MySQL]. |
| `auth.params.database` | O nome do banco de dados. |
| `auth.params.username` | O nome de usuário que corresponde ao banco de dados. |
| `auth.params.password` | A senha que corresponde ao banco de dados. |
| `auth.params.sslMode` | Um valor booleano que controla se o SSL é imposto ou não, dependendo do suporte do servidor. O padrão dessa configuração é `false`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL MySQL] é: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Exibir exemplo de resposta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Criar um fluxo de dados para dados de [!DNL MySQL]

Agora que você conectou com êxito o banco de dados [!DNL MySQL], agora é possível [criar um fluxo de dados e assimilar dados do banco de dados na Experience Platform](../../collect/database-nosql.md).