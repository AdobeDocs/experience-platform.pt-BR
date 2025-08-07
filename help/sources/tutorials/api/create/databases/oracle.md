---
title: Conectar o Oracle DB ao Experience Platform usando a API do Serviço de fluxo
description: Saiba como conectar o Oracle DB ao Experience Platform usando APIs.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# Conectar o [!DNL Oracle DB] ao Experience Platform usando a API [!DNL Flow Service]

Leia este guia para saber como conectar sua conta do [!DNL Oracle DB] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Oracle] usando a API [!DNL Flow Service].

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

### Coletar credenciais necessárias

Leia a [[!DNL Oracle DB] visão geral](../../../../connectors/databases/oracle.md#prerequisites) para obter informações sobre autenticação.

## Conectar [!DNL Oracle DB] ao Experience Platform no Azure {#azure}

Leia as etapas abaixo para obter informações sobre como conectar sua conta do [!DNL Oracle DB] à Experience Platform no Azure.

### Criar uma conexão base para [!DNL Oracle DB] no Experience Platform no Azure {#azure-base}

Uma conexão básica vincula sua origem ao Experience Platform, armazenando detalhes de autenticação, status da conexão e uma ID exclusiva. Use essa ID para procurar arquivos de origem e identificar itens específicos a serem assimilados, incluindo seus tipos de dados e formatos.

**Formato da API**

```https
POST /connections
```

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` e forneça suas credenciais de autenticação [!DNL Oracle DB] como parte dos parâmetros de solicitação.

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Oracle DB] usando autenticação de cadeia de conexão.

+++Exibir solicitação


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão usada para se conectar a [!DNL Oracle DB]. O padrão da cadeia de conexão [!DNL Oracle DB] é: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Oracle]: `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Exibir resposta

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## Conectar o [!DNL Oracle DB] ao Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

Leia as etapas abaixo para obter informações sobre como conectar sua conta do [!DNL Oracle DB] ao Experience Platform no AWS.

### Criar uma conexão base para [!DNL Oracle DB] no Experience Platform no AWS {#aws-base}

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Oracle DB] se conectar ao Experience Platform no AWS.

+++Exibir solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
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
| `auth.params.server` | O endereço IP ou o nome de host do servidor [!DNL Oracle DB]. |
| `auth.params.port` | O número da porta do servidor [!DNL Oracle DB]. |
| `auth.params.database` | O nome da instância [!DNL Oracle DB] à qual você está se conectando. |
| `auth.params.username` | A conta de usuário associada à sua instância [!DNL Oracle DB]. |
| `auth.prams.password` | A senha que corresponde à sua conta de usuário do [!DNL Oracle DB]. |
| `auth.params.schema` | O esquema que contém seus objetos de banco de dados. |
| `auth.params.sslMode` | Um valor booleano que indica se as medidas SSL são ou não impostas. |
| `connectionSpec.id` | A ID de especificação da conexão que corresponde à origem [!DNL Oracle DB]. Este valor de ID é corrigido como: `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`) e correspondente. Você pode usar a ID para [criar conexão de origem](../../collect/database-nosql.md#create-a-source-connection) e o `etag` para [atualizar sua conta](../../update.md).

+++Exibir resposta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Criar um fluxo de dados para dados de [!DNL Oracle DB]

Agora que a conta do [!DNL Oracle DB] foi conectada com êxito, você pode [criar um fluxo de dados e assimilar dados do banco de dados na Experience Platform](../../collect/database-nosql.md).