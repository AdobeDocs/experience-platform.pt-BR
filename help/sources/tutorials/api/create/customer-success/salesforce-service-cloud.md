---
title: Criar uma conexão do Salesforce Service Cloud Source usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform à Salesforce Service Cloud usando a API do Serviço de fluxo.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 3%

---

# Criar uma conexão de origem [!DNL Salesforce Service Cloud] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Leia este tutorial para saber como criar uma conexão base para [!DNL Salesforce Service Cloud] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Salesforce Service Cloud] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

>[!WARNING]
>
>A autenticação básica para a origem [!DNL Salesforce Service Cloud] será descontinuada em janeiro de 2026. Você deve mudar para a autenticação de Credencial do cliente OAuth 2 para continuar usando a origem e assimilando dados da conta do [!DNL Salesforce Service Cloud] para o Experience Platform.

A origem [!DNL Salesforce Service Cloud] dá suporte à autenticação básica e à Credencial do Cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para conectar sua conta do [!DNL Salesforce Service Cloud] ao [!DNL Flow Service] usando a autenticação básica, forneça valores para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| `environmentUrl` | A URL da instância de origem [!DNL Salesforce Service Cloud]. |
| `username` | O nome de usuário da conta de usuário [!DNL Salesforce Service Cloud]. |
| `password` | A senha da conta de usuário [!DNL Salesforce Service Cloud]. |
| `securityToken` | O token de segurança para a conta de usuário [!DNL Salesforce Service Cloud]. |
| `apiVersion` | (Opcional) A versão da API REST da instância [!DNL Salesforce Service Cloud] que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, será necessário inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce Service Cloud] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre a introdução, visite [este documento do Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credencial do cliente OAuth 2]

Para conectar sua conta do [!DNL Salesforce Service Cloud] ao [!DNL Flow Service] usando a Credencial do Cliente OAuth 2, forneça valores para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| `environmentUrl` | A URL da instância de origem [!DNL Salesforce Service Cloud]. |
| `clientId` | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce Service Cloud]. |
| `clientSecret` | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce Service Cloud]. |
| `apiVersion` | A versão da API REST da instância [!DNL Salesforce Service Cloud] que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, será necessário inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. Esse valor é obrigatório para autenticação de Credencial do cliente OAuth2. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce Service Cloud] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce Service Cloud], leia o [[!DNL Salesforce Service Cloud] guia sobre Fluxos de Autorização do OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Salesforce Service Cloud] como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

>[!BEGINTABS]

>[!TAB Autenticação básica]

A solicitação a seguir cria uma conexão base para [!DNL Salesforce Service Cloud] usando autenticação básica:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Parâmetro | Descrição |
| ---| --- |
| `auth.params.environmentUrl` | A URL da instância [!DNL Salesforce Service Cloud]. |
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Salesforce Service Cloud]. |
| `auth.params.password` | A senha associada à sua conta [!DNL Salesforce Service Cloud]. |
| `auth.params.securityToken` | O token de segurança associado à sua conta [!DNL Salesforce Service Cloud]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Salesforce Service Cloud]: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB Credencial do Cliente OAuth2]

A solicitação a seguir cria uma conexão base para [!DNL Salesforce Service Cloud] usando a Credencial do Cliente OAuth 2:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `auth.params.environmentUrl` | A URL da instância [!DNL Salesforce Service Cloud]. |
| `auth.params.clientId` | A ID do cliente associada à sua conta do [!DNL Salesforce Service Cloud]. |
| `auth.params.clientSecret` | O segredo do cliente associado à sua conta do [!DNL Salesforce Service Cloud]. |
| `auth.params.apiVersion` | A versão da API REST da instância [!DNL Salesforce Service Cloud] que você está usando. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Salesforce Service Cloud]: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**Resposta**

Uma resposta bem-sucedida retorna a conexão básica recém-criada, juntamente com a ID exclusiva.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Salesforce Service Cloud] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de sucesso do cliente para o Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/customer-success.md)
