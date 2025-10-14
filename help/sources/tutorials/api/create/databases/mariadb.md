---
title: Conectar o MariaDB ao Experience Platform usando a API do serviço de fluxo
description: Saiba como conectar sua conta MariaDB ao Experience Platform usando APIs.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---

# Conectar o [!DNL MariaDB] ao Experience Platform usando a API [!DNL Flow Service]

Leia este guia para saber como conectar sua conta do [!DNL MariaDB] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL MariaDB] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Leia a [[!DNL MariaDB] visão geral](../../../../connectors/databases/mariadb.md#prerequisites) para obter informações sobre autenticação.

### Uso de APIs do Experience Platform

Leia o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md) para obter informações sobre como fazer chamadas com êxito para as APIs do Experience Platform.

## Conectar [!DNL MariaDB] ao Experience Platform

Leia as etapas abaixo para obter informações sobre como conectar sua conta do [!DNL MariaDB] à Experience Platform.

### Criar uma conexão base para [!DNL MariaDB]

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

**Formato da API**

```https
POST /connections
```

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` e forneça as credenciais de autenticação apropriadas para sua conta [!DNL MariaDB].

>[!BEGINTABS]

>[!TAB Autenticação baseada em cadeia de conexão]

**Solicitação**

A solicitação a seguir cria uma conexão base para uma origem [!DNL MariaDB] usando autenticação baseada em cadeia de conexão.

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
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão associada à sua autenticação [!DNL MariaDB]. O padrão da cadeia de conexão [!DNL MariaDB] é: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL MariaDB] é: `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Exibir exemplo de resposta

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB Autenticação básica]

**Solicitação**

A solicitação a seguir cria uma conexão base para uma origem [!DNL MariaDB] usando autenticação básica.

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
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.server` | O nome ou IP do banco de dados [!DNL MariaDB]. |
| `auth.params.database` | O nome do banco de dados. |
| `auth.params.username` | O nome de usuário que corresponde ao banco de dados. |
| `auth.params.password` | A senha que corresponde ao banco de dados. |
| `auth.params.sslMode` | O método pelo qual os dados são criptografados durante a transferência. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL MariaDB] é: `3000eb99-cd47-43f3-827c-43caf170f015`. |

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

>[!ENDTABS]


## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL MariaDB] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
