---
title: Criar uma conexão básica do Salesforce usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a uma conta do Salesforce usando a API do Serviço de fluxo.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 8d62cf4ca0071e84baa9399e0a25f7ebfb096c1a
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 3%

---

# Criar um [!DNL Salesforce] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Salesforce] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL Platform] para um [!DNL Salesforce] conta usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A variável [!DNL Salesforce] A origem oferece suporte à autenticação básica e à Credencial do Cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para conectar seu [!DNL Salesforce] conta para [!DNL Flow Service] usando a autenticação básica, forneça valores para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| `environmentUrl` | O URL do [!DNL Salesforce] instância de origem. |
| `username` | O nome de usuário para o [!DNL Salesforce] conta de usuário. |
| `password` | A senha para o [!DNL Salesforce] conta de usuário. |
| `securityToken` | O token de segurança para o [!DNL Salesforce] conta de usuário. |
| `apiVersion` | Opcional) A versão da API REST do [!DNL Salesforce] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre a introdução, visite [este documento do Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credencial do cliente OAuth 2]

Para conectar seu [!DNL Salesforce] conta para [!DNL Flow Service] usando a Credencial do cliente OAuth 2, forneça valores para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| `environmentUrl` | O URL do [!DNL Salesforce] instância de origem. |
| `clientId` | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo para [!DNL Salesforce]. |
| `clientSecret` | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo para [!DNL Salesforce]. |
| `apiVersion` | A versão da API REST do [!DNL Salesforce] instância que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, você deverá inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. Esse valor é obrigatório para autenticação de Credencial do cliente OAuth2. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce] é: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce], leia o [[!DNL Salesforce] guia sobre fluxos de autorização OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` e forneça seu [!DNL Salesforce] credenciais de autenticação no corpo da solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

>[!BEGINTABS]

>[!TAB Autenticação básica]

A solicitação a seguir cria uma conexão básica para [!DNL Salesforce] usando autenticação básica:

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
| `auth.params.environmentUrl` | O URL do seu [!DNL Salesforce] instância. |
| `auth.params.username` | O nome de usuário associado à [!DNL Salesforce] conta. |
| `auth.params.password` | A senha associada ao seu [!DNL Salesforce] conta. |
| `auth.params.securityToken` | O token de segurança associado à [!DNL Salesforce] conta. |
| `connectionSpec.id` | A variável [!DNL Salesforce] ID da especificação de conexão: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!TAB Credencial do cliente OAuth 2]

A solicitação a seguir cria uma conexão básica para [!DNL Salesforce] usando a credencial do cliente OAuth 2:

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
            "apiVersion": "60.0"
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
| `auth.params.environmentUrl` | O URL do seu [!DNL Salesforce] instância. |
| `auth.params.clientId` | A ID do cliente associada à [!DNL Salesforce] conta. |
| `auth.params.clientSecret` | O segredo do cliente associado à [!DNL Salesforce] conta. |
| `auth.params.apiVersion` | A versão da API REST do [!DNL Salesforce] instância que você está usando. |
| `connectionSpec.id` | A variável [!DNL Salesforce] ID da especificação de conexão: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!ENDTABS]

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Salesforce] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do CRM para a Platform usando o [!DNL Flow Service] API](../../collect/crm.md)
