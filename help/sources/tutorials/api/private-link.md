---
title: Suporte a link privado em origens
description: Saiba como criar e usar links privados para Fontes do Adobe Experience Platform
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 4c91ffc60a2537fcc76ce935bf3b163984fdc5e4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 6%

---

# Suporte a link privado em origens

>[!AVAILABILITY]
>
>Este recurso está em Disponibilidade Limitada e, no momento, só tem suporte nas seguintes fontes:
>
>* [[!DNL Azure Blob]](../../connectors/cloud-storage/blob.md)
>* [[!DNL Azure Data Lake Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

Leia este guia para saber como estabelecer uma conexão de ponto de extremidade privado com fontes baseadas no Azure por meio de um link privado e permitir um mecanismo de transferência mais seguro para seus dados.

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Platform].
* [Sandboxes](../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../landing/api-guide.md).

## Criar um ponto de extremidade privado {#create-private-endpoint}

Para criar um ponto de extremidade privado, faça uma solicitação POST para `/privateEndpoints`.

**Formato da API**

```http
POST /privateEndpoints
```

**Solicitação**

A solicitação a seguir cria um ponto de extremidade privado:

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [],
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do seu ponto de extremidade privado. |
| `subscriptionId` | A ID associada à sua assinatura do [!DNL Azure]. Para obter mais informações, leia o guia [!DNL Azure] em [recuperando sua assinatura e IDs de locatário de [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | O nome do seu grupo de recursos em [!DNL Azure]. Um grupo de recursos contém recursos relacionados para uma solução [!DNL Azure]. Para obter mais informações, leia o guia [!DNL Azure] em [gerenciando grupos de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | O nome do recurso. Em [!DNL Azure], um recurso se refere a instâncias como máquinas virtuais, aplicativos Web e bancos de dados. Para obter mais informações, leia o guia [!DNL Azure] em [noções básicas sobre o [!DNL Azure] gerenciador de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | Os nomes de domínio totalmente qualificados para sua origem. Esta propriedade é necessária somente ao usar a origem [!DNL Snowflake]. |
| `connectionSpec.id` | A ID de especificação da conexão da origem que você está usando. |
| `connectionSpec.version` | A versão da ID de especificação de conexão que você está usando. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o seguinte:

+++Selecione para exibir o exemplo de resposta

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "fqdns": [],
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID do terminal privado recém-criado. |
| `name` | O nome do seu ponto de extremidade privado. |
| `subscriptionId` | A ID associada à sua assinatura do [!DNL Azure]. Para obter mais informações, leia o guia [!DNL Azure] em [recuperando sua assinatura e IDs de locatário de [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | O nome do seu grupo de recursos em [!DNL Azure]. Um grupo de recursos contém recursos relacionados para uma solução [!DNL Azure]. Para obter mais informações, leia o guia [!DNL Azure] em [gerenciando grupos de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | O nome do recurso. Em [!DNL Azure], um recurso se refere a instâncias como máquinas virtuais, aplicativos Web e bancos de dados. Para obter mais informações, leia o guia [!DNL Azure] em [noções básicas sobre o [!DNL Azure] gerenciador de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | Os nomes de domínio totalmente qualificados para sua origem. Esta propriedade é necessária somente ao usar a origem [!DNL Snowflake]. |
| `connectionSpec.id` | A ID de especificação da conexão da origem que você está usando. |
| `connectionSpec.version` | A versão da ID de especificação de conexão que você está usando. |
| `state` | O estado atual do seu ponto de extremidade privado. Os estados válidos incluem: <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## Recuperar uma lista de pontos de extremidade privados {#retrieve-private-endpoints}

Para recuperar uma lista de pontos de extremidade privados de uma determinada sandbox em sua organização, faça uma solicitação GET para `/privateEndpoints`.

**Formato da API**

```http
GET /privateEndpoints
```

**Solicitação**

A solicitação a seguir recupera uma lista de todos os endpoints privados existentes em sua organização.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna uma lista de pontos de extremidade privados na organização.

+++Selecione para exibir o exemplo de resposta

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Recuperar uma lista de pontos de extremidade privados para uma determinada fonte {#retrieve-private-endpoints-by-source}

Para recuperar uma lista de pontos de extremidade privados que correspondam a uma origem específica, faça uma solicitação GET para o ponto de extremidade `/privateEndpoints` e forneça o `connectionSpec.id` da origem.

**Formato da API**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | A ID de especificação de conexão da origem para a qual você deseja pesquisar pontos de extremidade privados. |

**Solicitação**

A solicitação a seguir recupera uma lista de todos os pontos de extremidade privados que correspondem à origem com ID de especificação de conexão: `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna uma lista de todos os pontos de extremidade privados que correspondem à origem com a ID de especificação de conexão: `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Selecione para exibir o exemplo de resposta

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Recuperar um ponto de extremidade privado {#retrieve-specific-private-endpoint}

Para recuperar um ponto de extremidade privado específico, faça uma solicitação GET para `/privateEndpoints` e forneça a ID do ponto de extremidade privado que você deseja recuperar.

**Formato da API**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | A ID do ponto de extremidade privado que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera o ponto de extremidade privado com a ID:`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o ponto de extremidade privado com ID: `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`

+++Selecione para exibir o exemplo de resposta

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## Resolver um ponto de extremidade privado {#resolve-private-endpoint}

**Formato da API**

```http
GET /privateEndpoints?op=autoResolve
```

**Solicitação**

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**Resposta**

+++Selecione para exibir o exemplo de resposta

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## Ativar criação interativa {#enable-interactive-authoring}

A criação interativa é usada para funcionalidades como explorar uma conexão ou conta e visualizar dados. Para habilitar a criação interativa, faça uma solicitação POST para `/privateEndpoints/interactiveAuthoring` e especifique `enable` como operador em seus parâmetros de consulta.

**Formato da API**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `op` | A operação que você deseja executar. Para habilitar a criação interativa, defina o valor `op` como `enable`. |

**Solicitação**

A solicitação a seguir ativa a criação interativa para o endpoint privado e define o TTL como 60 minutos.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `autoTerminationMinutes` | O TTL (tempo de vida útil) de criação interativo em minutos. A criação interativa é usada para funcionalidades como explorar uma conexão ou conta e visualizar dados. Você pode definir um TTL máximo de 120 minutos. O TTL padrão é de 60 minutos. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Accepted).

## Recuperar status de criação interativa {#retrieve-interactive-authoring-status}

Para exibir o status atual da criação interativa para seu ponto de extremidade privado, faça uma solicitação GET para `/privateEndpoints/interactiveAuthoring`.

**Formato da API**

```http
GET /privateEndpoints/interactiveAuthoring
```

**Solicitação**

A solicitação a seguir recupera o status da criação interativa:

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

+++Selecione para exibir o exemplo de resposta

```json
{
    "status": "Disabled"
}
```

| Propriedade | Descrição |
| --- | --- |
| `status` | O status da criação interativa. Os valores válidos incluem: `disabled`, `enabling`, `enabled`. |

+++

## Excluir ponto de acesso privado {#delete-private-endpoint}

Para excluir seu ponto de extremidade privado, faça uma solicitação DELETE para `/privateEndpoints` e forneça a ID do ponto de extremidade que deseja excluir.

**Formato da API**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | A ID da empresa privada que você deseja excluir. |

**Solicitação**

A solicitação a seguir exclui o ponto de extremidade privado com ID: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (Sucesso). Você pode verificar a exclusão fazendo uma solicitação GET e para `/privateEndpoints` e fornecendo a ID excluída como um parâmetro de consulta.

## Serviço de fluxo {#flow-service}

Leia as seções a seguir para obter informações sobre como usar pontos de extremidade privados em conjunto com a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

### Criar uma conexão com um ponto de extremidade privado {#create-base-connection}

Para criar uma conexão com um ponto de extremidade privado no Experience Platform, faça uma solicitação POST para o ponto de extremidade `/connections` da API [!DNL Flow Service].

**Formato da API**

```http
POST /connections/
```

**Solicitação**

A solicitação a seguir cria uma conexão de base autenticada para [!DNL Snowflake], ao mesmo tempo em que usa um ponto de extremidade privado.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "A base connection for a Snowflake source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
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
| `name` | O nome da sua conexão básica. |
| `description` | (Opcional) Uma descrição que fornece informações adicionais sobre sua conexão. |
| `auth.specName` | A autenticação que está sendo usada para conectar sua origem ao Experience Platform. |
| `auth.params.connectionString` | A cadeia de conexão [!DNL Snowflake]. Para obter mais informações, leia o [[!DNL Snowflake] guia de autenticação de API](../api/create/databases/snowflake.md). |
| `auth.params.usePrivateLink` | Um valor booleano que determina se você está usando ou não um ponto de extremidade privado. Defina esse valor como `true` se estiver usando um ponto de extremidade privado. |
| `connectionSpec.id` | A ID de especificação de conexão de [!DNL Snowflake]. |
| `connectionSpec.version` | A versão da ID de especificação da conexão do [!DNL Snowflake]. |

+++

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão básica recém-gerada e a tag.

+++Selecione para exibir o exemplo de resposta

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### Recuperar conexões vinculadas a um determinado ponto de extremidade privado {#retrieve-connections-by-endpoint}

Para recuperar conexões vinculadas a um ponto de extremidade privado específico, faça uma solicitação GET para o ponto de extremidade `/connections` e forneça a ID do ponto de extremidade privado como um parâmetro de consulta.

**Formato da API**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | A ID do ponto de extremidade privado vinculado às conexões que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera conexões existentes vinculadas ao ponto de extremidade privado com ID: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna uma lista de conexões vinculadas ao ponto de extremidade privado consultado.

+++Selecione para exibir o exemplo de resposta

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### Recuperar conexões associadas a qualquer ponto de extremidade privado {#retrieve-connections}

Para recuperar conexões associadas a qualquer ponto de extremidade privado, faça uma solicitação GET para o ponto de extremidade `/connections` e forneça `property=auth.params.usePrivateLink==true` como um parâmetro de consulta.

**Formato da API**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**Solicitação**

A solicitação a seguir recupera todas as conexões em sua organização que estão usando pontos de extremidade privados.

+++Selecione para exibir o exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna todas as conexões vinculadas a pontos de extremidade privados.

+++Selecione para exibir o exemplo de resposta

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++