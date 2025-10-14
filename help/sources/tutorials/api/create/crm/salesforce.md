---
title: Conectar O Salesforce Ao Experience Platform Usando A API Do Serviço De Fluxo
description: Saiba como conectar o Adobe Experience Platform a uma conta do Salesforce usando a API do serviço de fluxo.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 56307d8457ba6d0046ad80a7c97405220aa6161c
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 3%

---

# Conectar o [!DNL Salesforce] ao Experience Platform usando a API [!DNL Flow Service]

Leia este guia para saber como você pode conectar sua conta de origem do [!DNL Salesforce] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Conectar [!DNL Salesforce] ao Experience Platform em [!DNL Azure] {#azure}

Leia as etapas abaixo para obter informações sobre como conectar sua origem do [!DNL Salesforce] ao Experience Platform no [!DNL Azure].

### Coletar credenciais necessárias

>[!WARNING]
>
>A autenticação básica para a origem [!DNL Salesforce] será descontinuada em janeiro de 2026. Você deve mudar para a autenticação de Credencial do cliente OAuth 2 para continuar usando a origem e assimilando dados da conta do [!DNL Salesforce] para o Experience Platform.

A origem [!DNL Salesforce] dá suporte à autenticação básica e à Credencial do Cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para conectar sua conta do [!DNL Salesforce] ao [!DNL Flow Service] usando a autenticação básica, forneça valores para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| `environmentUrl` | A URL da instância de origem [!DNL Salesforce]. O formato de `environmentUrl` é `https://[domain].my.salesforce.com`. |
| `username` | O nome de usuário da conta de usuário [!DNL Salesforce]. |
| `password` | A senha da conta de usuário [!DNL Salesforce]. |
| `securityToken` | O token de segurança para a conta de usuário [!DNL Salesforce]. |
| `apiVersion` | Opcional) A versão da API REST da instância [!DNL Salesforce] que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, será necessário inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre a introdução, visite [este documento do Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credencial do cliente OAuth 2]

Para conectar sua conta do [!DNL Salesforce] ao [!DNL Flow Service] usando a Credencial do Cliente OAuth 2, forneça valores para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| `environmentUrl` | A URL da instância de origem [!DNL Salesforce]. O formato de `environmentUrl` é `https://[domain].my.salesforce.com` |
| `clientId` | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce]. |
| `clientSecret` | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce]. |
| `apiVersion` | A versão da API REST da instância [!DNL Salesforce] que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, será necessário inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. Esse valor é obrigatório para autenticação de Credencial do cliente OAuth2. |
| `includeDeletedObjects` | Um valor booleano usado para determinar se os registros excluídos por software devem ser incluídos. Se definido como verdadeiro, os registros excluídos por software podem ser incluídos na consulta do [!DNL Salesforce] e assimilados da sua conta na Experience Platform. Se você não especificar sua configuração, este valor será o padrão `false`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce], leia o [[!DNL Salesforce] guia sobre Fluxos de Autorização do OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

### Criar uma conexão base para [!DNL Salesforce] no Experience Platform em [!DNL Azure]

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma conexão base e conectar sua conta do [!DNL Salesforce] ao Experience Platform em [!DNL Azure], faça uma solicitação POST para o ponto de extremidade `/connections` e forneça suas credenciais de autenticação do [!DNL Salesforce] no corpo da solicitação.

**Formato da API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticação básica]

+++Solicitação

A solicitação a seguir cria uma conexão base para [!DNL Salesforce] usando autenticação básica:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.environmentUrl` | A URL da instância [!DNL Salesforce]. |
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Salesforce]. |
| `auth.params.password` | A senha associada à sua conta [!DNL Salesforce]. |
| `auth.params.securityToken` | O token de segurança associado à sua conta [!DNL Salesforce]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++

+++Resposta

Uma resposta bem-sucedida retorna a conexão básica recém-criada, juntamente com a ID exclusiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB Credencial do cliente OAuth 2]

+++Solicitação

A solicitação a seguir cria uma conexão base para [!DNL Salesforce] usando a Credencial do Cliente OAuth 2:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0",
            "includeDeletedObjects": true
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.environmentUrl` | A URL da instância [!DNL Salesforce]. |
| `auth.params.clientId` | A ID do cliente associada à sua conta do [!DNL Salesforce]. |
| `auth.params.clientSecret` | O segredo do cliente associado à sua conta do [!DNL Salesforce]. |
| `auth.params.apiVersion` | A versão da API REST da instância [!DNL Salesforce] que você está usando. |
| `auth.params.includeDeletedObjects` | Um valor booliano usado para determinar se os registros excluídos por software devem ou não ser incluídos. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++


+++Resposta

Uma resposta bem-sucedida retorna a conexão básica recém-criada, juntamente com a ID exclusiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## Conectar o [!DNL Salesforce] ao Experience Platform no Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

Leia as etapas abaixo para obter informações sobre como conectar sua origem do [!DNL Salesforce] ao Experience Platform no AWS.

### Pré-requisitos

Para obter informações sobre como configurar sua conta do [!DNL Salesforce] para poder se conectar ao Experience Platform no AWS, leia a [[!DNL Salesforce] visão geral](../../../../connectors/crm/salesforce.md#aws).

### Criar uma conexão base para [!DNL Salesforce] no Experience Platform no AWS

Para criar uma conexão base e conectar sua conta do [!DNL Salesforce] ao Experience Platform no AWS, faça uma solicitação POST ao ponto de extremidade `/connections` e forneça os valores apropriados para suas credenciais.

**Formato da API**

```http
POST /connections
```

**Solicitação**

+++Selecione para exibir a solicitação

A solicitação a seguir cria uma conexão base para a origem [!DNL Salesforce] no Experience Platform no AWS.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

Para obter informações sobre como recuperar o [!DNL Salesforce] `jwtToken`, leia o manual sobre [como configurar uma [!DNL Salesforce] origem para se conectar ao Experience Platform no AWS](../../../../connectors/crm/salesforce.md#aws).

+++

**Resposta**

+++Selecione para exibir a resposta

Uma resposta bem-sucedida retorna a conexão básica recém-criada, juntamente com a ID exclusiva.

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### Verificar o status da conexão

Para verificar o status da conexão, faça uma solicitação GET para o ponto de extremidade `/connections` e forneça a ID de conexão básica gerada na etapa de criação.

**Formato da API**

```http
GET /connections
```

**Solicitação**

+++Selecione para exibir a solicitação

A solicitação a seguir recupera informações para a ID de conexão base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

>[!BEGINTABS]

>[!TAB Inicializando]

+++Selecione para exibir o exemplo de resposta

A resposta a seguir exibe informações para a ID de conexão base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` enquanto está no estado `initializing`.

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB Ativado]

+++Selecione para exibir o exemplo de resposta

A resposta a seguir exibe informações para a ID de conexão base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` enquanto está no estado `enabled`.

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Salesforce] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do CRM para o Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/crm.md)
