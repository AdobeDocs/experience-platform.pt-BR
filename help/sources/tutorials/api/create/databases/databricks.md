---
title: Conectar Databricks Ao Experience Platform Usando A API Do Serviço De Fluxo
description: Saiba como conectar Databricks ao Experience Platform usando APIs.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 96e395e3b3d977d7eb04c400f6fd290977bf1101
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---

# Conectar o [!DNL Databricks] ao Experience Platform usando a API [!DNL Flow Service]

>[!AVAILABILITY]
>
>* A origem [!DNL Databricks] está disponível no catálogo de origens para usuários que compraram o Real-Time CDP Ultimate.
>
>* A origem [!DNL Databricks] está na versão beta. Leia os [termos e condições](../../../../home.md#terms-and-conditions) na visão geral das fontes para obter mais informações sobre como usar fontes com rótulo beta.

Leia este guia para saber como conectar sua conta do [!DNL Databricks] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Leia o manual sobre [como começar a usar as APIs do Experience Platform](../../../../../landing/api-guide.md) para obter informações sobre como fazer chamadas com êxito para as APIs do Experience Platform.

### Configurar pré-requisitos

Leia a [[!DNL Databricks] visão geral](../../../../connectors/databases/databricks.md) para saber mais sobre as configurações de pré-requisito que devem ser concluídas antes de você poder conectar sua conta à Experience Platform.

### Coletar credenciais necessárias

Forneça valores para as credenciais a seguir para conectar [!DNL Databricks] ao Experience Platform.

| Credencial | Descrição |
| --- | --- |
| `domain` | A URL do espaço de trabalho [!DNL Databricks]. Por exemplo, `https://adb-1234567890123456.7.azuredatabricks.net`. |
| `clusterId` | A ID do cluster em [!DNL Databricks]. Este cluster já deve ser um cluster existente e deve ser um cluster interativo. |
| `accessToken` | O token de acesso que autentica a conta do [!DNL Databricks]. Você pode gerar seu token de acesso usando o espaço de trabalho [!DNL Databricks]. |
| `database` | O nome do banco de dados no lago delta. |
| `connectionSpec.Id` | A ID de especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação da conexão para [!DNL Databricks] é `e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`. |

Para obter mais informações, leia a visão geral[&#128279;](../../../../connectors/databases/databricks.md) do [!DNL Databricks] .

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` e forneça as credenciais de autenticação apropriadas para sua conta [!DNL Databricks].

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para uma origem [!DNL Databricks] usando autenticação de token de acesso.

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
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.domain` | A URL do espaço de trabalho [!DNL Databricks]. |
| `auth.params.clusterId` | A ID do cluster em [!DNL Databricks]. Este cluster já deve ser um cluster existente e deve ser um cluster interativo |
| `auth.params.accessToken` | O token de acesso que autentica a conta do [!DNL Databricks]. |
| `auth.params.database` | O nome do banco de dados no lago delta. |
| `connectionSpec.id` | A ID de especificação de conexão [!DNL Databricks]. |

+++

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo a ID de conexão básica.

+++Exibir exemplo de resposta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma conexão entre sua conta do [!DNL Databricks] e a Experience Platform. Você pode usar sua ID de conexão base recém-gerada nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
