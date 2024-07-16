---
title: Criar uma conexão básica do Google Ads usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Google Ads usando a API do serviço de fluxo.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 3%

---

# Criar uma conexão básica do Google Ads usando a API [!DNL Flow Service]

>[!WARNING]
>
>A origem [!DNL Google Ads] está temporariamente indisponível. O Adobe está trabalhando para resolver problemas com esta fonte.

>[!NOTE]
>
>A fonte do Google Ads está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para o Google Ads usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, além de fornecer a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância de Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisará saber para se conectar com êxito ao Google Ads usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte ao Google Ads, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientCustomerId` | A ID do cliente é o número da conta que corresponde à conta do cliente do Google Ads que você deseja gerenciar com a API do Google Ads. Esta ID segue o modelo de `123-456-7890`. |
| `loginCustomerId` | A ID do cliente de logon é o número da conta que corresponde à sua conta de gerente do Google Ads e é usada para buscar dados de relatório de um cliente operacional específico. Para obter mais informações sobre como fazer logon na ID do cliente, leia a [documentação da API do Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | O token do desenvolvedor permite acessar a API do Google Ads. Você pode usar o mesmo token do desenvolvedor para fazer solicitações em relação a todas as suas contas do Google Ads. Recupere seu token de desenvolvedor [fazendo logon em sua conta de gerente](https://ads.google.com/home/tools/manager-accounts/) e navegando até a página [!DNL API Center]. |
| `refreshToken` | O token de atualização faz parte da autenticação [!DNL OAuth2]. Esse token permite gerar novamente os tokens de acesso após a expiração. |
| `clientId` | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação [!DNL OAuth2]. Juntas, a ID do cliente e a senha do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo na Google. |
| `clientSecret` | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação [!DNL OAuth2]. Juntas, a ID do cliente e a senha do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo na Google. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para o Google Ads é: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Leia o documento de visão geral da API para [mais informações sobre a introdução ao Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` enquanto fornece suas credenciais de autenticação do Google Ads como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para o Google Ads:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.clientCustomerID` | A ID do cliente da sua conta do Google Ads. |
| `auth.params.loginCustomerID` | A ID do cliente de logon que corresponde à sua conta de gerente do Google Ads. |
| `auth.params.developerToken` | O token do desenvolvedor da sua conta do Google Ads. |
| `auth.params.refreshToken` | O token de atualização da sua conta do Google Ads. |
| `auth.params.clientID` | A ID do cliente da sua conta do Google Ads. |
| `auth.params.clientSecret` | A frase secreta do cliente da sua conta do Google Ads. |
| `connectionSpec.id` | A ID da especificação de conexão do Google Ads: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão básica do Google Ads usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de publicidade para a Platform usando a API  [!DNL Flow Service] ](../../collect/advertising.md)
