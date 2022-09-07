---
keywords: Experience Platform, home, tópicos populares, google ads, Google Ads, google ads, anúncios
title: Criar uma conexão básica do Google Ads usando a API do Serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform aos anúncios da Google usando a API do Serviço de fluxo.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# Crie uma conexão básica do Google Ads usando o [!DNL Flow Service] API

>[!NOTE]
>
>A origem dos anúncios do Google está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para Anúncios do Google usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância de Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com sucesso aos anúncios do Google usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para se conectar ao Google Ads, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientCustomerId` | A ID do cliente é o número da conta que corresponde à conta de cliente do Google Ads que você deseja gerenciar com a API do Google Ads. Essa ID segue o modelo de `123-456-7890`. |
| `developerToken` | O token do desenvolvedor permite acessar a API de anúncios do Google. Você pode usar o mesmo token de desenvolvedor para fazer solicitações em relação a todas as suas contas do Google Ads. Recupere o token do desenvolvedor por [fazer logon em sua conta do gerente](https://ads.google.com/home/tools/manager-accounts/) e navegar até a [!DNL API Center] página. |
| `refreshToken` | O token de atualização faz parte de [!DNL OAuth2] autenticação. Esse token permite gerar seus tokens de acesso novamente após expirarem. |
| `clientId` | A ID do cliente é usada em conjunto com o segredo do cliente como parte de [!DNL OAuth2] autenticação. Juntas, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando seu aplicativo para a Google. |
| `clientSecret` | O segredo do cliente é usado em conjunto com a ID do cliente como parte de [!DNL OAuth2] autenticação. Juntas, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando seu aplicativo para a Google. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para anúncios do Google é: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Leia o documento de visão geral da API para [mais informações sobre a introdução ao Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint ao fornecer suas credenciais de autenticação do Google Ads como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para os Anúncios do Google:

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
| `auth.params.developerToken` | O token de desenvolvedor da sua conta do Google Ads. |
| `auth.params.refreshToken` | O token de atualização da sua conta do Google Ads. |
| `auth.params.clientID` | A ID do cliente da sua conta do Google Ads. |
| `auth.params.clientSecret` | O segredo do cliente de sua conta do Google Ads. |
| `connectionSpec.id` | A ID de especificação de conexão do Google Ads: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão básica do Google Ads usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de publicidade para a plataforma usando o [!DNL Flow Service] API](../../collect/advertising.md)
