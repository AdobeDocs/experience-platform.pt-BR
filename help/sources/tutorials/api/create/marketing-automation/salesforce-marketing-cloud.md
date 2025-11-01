---
title: Conectar O Salesforce Marketing Cloud Ao Experience Platform Usando A API Do Serviço De Fluxo
description: Saiba como conectar sua conta do Salesforce Marketing Cloud ao Experience Platform usando APIs.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 2%

---

# Conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando a API [!DNL Flow Service]

>[!WARNING]
>
>A origem [!DNL Salesforce Marketing Cloud] será substituída em janeiro de 2026. Uma nova fonte será lançada ainda este ano como alternativa. Depois que a nova origem for lançada, você deverá planejar migrar para a nova origem criando novas conexões de conta e fluxos de dados antes do final de janeiro de 2026.

Leia este guia para saber como conectar sua conta do [!DNL Salesforce Marketing Cloud] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Azure Synapse Analytics] usando a API [!DNL Flow Service].


### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Salesforce Marketing Cloud] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Leia a [[!DNL Salesforce Marketing Cloud] visão geral da autenticação](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md) para obter informações sobre autenticação.

### Uso de APIs do Experience Platform

Leia o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md) para obter informações sobre como fazer chamadas com êxito para as APIs do Experience Platform.

## Conectar [!DNL Salesforce Marketing Cloud] ao Experience Platform em [!DNL Azure]

Leia o seguinte para saber como criar uma conexão básica e conectar sua conta do [!DNL Salesforce Marketing Cloud] ao Experience Platform em [!DNL Azure].

### Criar uma conexão básica {#azure-base}

>[!IMPORTANT]
>
>No momento, a assimilação de objetos personalizados não tem suporte da integração de origem [!DNL Salesforce Marketing Cloud].

Uma **conexão base** armazena informações importantes que vinculam seu sistema de origem à Adobe Experience Platform. Isso inclui:

* Credenciais de autenticação da sua origem
* O status atual da conexão
* Uma **ID de conexão básica** exclusiva

A **ID da conexão base** permite procurar e explorar arquivos da sua origem, ajudando você a identificar quais itens serão assimilados, juntamente com seus tipos de dados e formatos.

Para criar uma ID de conexão base, envie uma solicitação POST para o ponto de extremidade `/connections`, incluindo suas credenciais de autenticação [!DNL Salesforce Marketing Cloud] nos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Salesforce Marketing Cloud].

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
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.host` |  |
| `auth.params.clientId` | A ID do cliente associada ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | O segredo do cliente associado ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

+++

+++Exibir resposta de exemplo

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## Conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

Leia as etapas abaixo para obter informações sobre como conectar sua conta do [!DNL Salesforce Marketing Cloud] ao Experience Platform no AWS.

### Criar uma conexão básica {#aws-base}

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Salesforce Service Cloud] se conectar ao Experience Platform no AWS.

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
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`).

+++Exibir exemplo de resposta

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## Criar um fluxo de dados para dados de [!DNL Salesforce Marketing Cloud]

Agora que você conectou com êxito a conta [!DNL Salesforce Marketing Cloud], é possível [criar um fluxo de dados e assimilar dados do provedor de automação de marketing na Experience Platform](../../collect/marketing-automation.md).