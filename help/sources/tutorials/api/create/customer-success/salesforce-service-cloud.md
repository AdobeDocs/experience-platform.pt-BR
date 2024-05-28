---
title: Criar uma conexão de origem do serviço Salesforce na nuvem usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform à Salesforce Service Cloud usando a API do Flow Service.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 3%

---

# Criar um [!DNL Salesforce Service Cloud] conexão de origem usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Leia este tutorial para saber como criar uma conexão básica para [!DNL Salesforce Service Cloud] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam um único [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Salesforce Service Cloud] usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A variável [!DNL Salesforce Service Cloud] A origem oferece suporte à autenticação básica e à Credencial do Cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para conectar seu [!DNL Salesforce Service Cloud] conta para [!DNL Flow Service] usando a autenticação básica, forneça valores para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| `environmentUrl` | O URL do [!DNL Salesforce Service Cloud] instância de origem. |
| `username` | O nome de usuário para o [!DNL Salesforce Service Cloud] conta de usuário. |
| `password` | A senha para o [!DNL Salesforce Service Cloud] conta de usuário. |
| `securityToken` | O token de segurança para o [!DNL Salesforce Service Cloud] conta de usuário. |
| `apiVersion` | (Opcional) A versão da API REST do [!DNL Salesforce Service Cloud] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce Service Cloud] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre a introdução, visite [este documento do Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credencial do cliente OAuth 2]

Para conectar seu [!DNL Salesforce Service Cloud] conta para [!DNL Flow Service] usando a Credencial do cliente OAuth 2, forneça valores para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| `environmentUrl` | O URL do [!DNL Salesforce Service Cloud] instância de origem. |
| `clientId` | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo para [!DNL Salesforce Service Cloud]. |
| `clientSecret` | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo para [!DNL Salesforce Service Cloud]. |
| `apiVersion` | A versão da API REST do [!DNL Salesforce Service Cloud] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. Esse valor é obrigatório para autenticação de Credencial do cliente OAuth2. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce Service Cloud] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce Service Cloud], leia o [[!DNL Salesforce Service Cloud] guia sobre fluxos de autorização OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Salesforce Service Cloud] credenciais de autenticação como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

>[!BEGINTABS]

>[!TAB Autenticação básica]

A solicitação a seguir cria uma conexão básica para [!DNL Salesforce Service Cloud] usando autenticação básica:

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
| `auth.params.environmentUrl` | O URL do seu [!DNL Salesforce Service Cloud] instância. |
| `auth.params.username` | O nome de usuário associado à [!DNL Salesforce Service Cloud] conta. |
| `auth.params.password` | A senha associada ao seu [!DNL Salesforce Service Cloud] conta. |
| `auth.params.securityToken` | O token de segurança associado à [!DNL Salesforce Service Cloud] conta. |
| `connectionSpec.id` | A variável [!DNL Salesforce Service Cloud] ID da especificação de conexão: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB Credencial do cliente OAuth2]

A solicitação a seguir cria uma conexão básica para [!DNL Salesforce Service Cloud] usando a credencial do cliente OAuth 2:

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
| `auth.params.environmentUrl` | O URL do seu [!DNL Salesforce Service Cloud] instância. |
| `auth.params.clientId` | A ID do cliente associada à [!DNL Salesforce Service Cloud] conta. |
| `auth.params.clientSecret` | O segredo do cliente associado à [!DNL Salesforce Service Cloud] conta. |
| `auth.params.apiVersion` | A versão da API REST do [!DNL Salesforce Service Cloud] instância que você está usando. |
| `connectionSpec.id` | A variável [!DNL Salesforce Service Cloud] ID da especificação de conexão: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

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

Ao seguir este tutorial, você criou um [!DNL Salesforce Service Cloud] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer os dados de sucesso do cliente para a Platform usando o [!DNL Flow Service] API](../../collect/customer-success.md)
