---
title: Conectar o Google Ads ao Experience Platform usando APIs
description: Saiba como conectar o Adobe Experience Platform ao Google Ads usando a API do serviço de fluxo.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Conectar o [!DNL Google Ads] ao Experience Platform usando a API [!DNL Flow Service]

>[!NOTE]
>
>A origem [!DNL Google Ads] está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Leia este tutorial para saber como conectar sua conta do [!DNL Google Ads] à Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Google Ads] usando a API [!DNL Flow Service].

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

### Coletar credenciais necessárias

Para obter informações sobre autenticação, leia a [[!DNL Google Ads] visão geral da origem](../../../../connectors/advertising/ads.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

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
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v17"

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
| `auth.params.clientCustomerID` | A ID do cliente da sua conta [!DNL Google Ads]. |
| `auth.params.loginCustomerID` | A ID do cliente de logon que corresponde à sua conta de gerente do [!DNL Google Ads]. |
| `auth.params.developerToken` | O token de desenvolvedor da sua conta [!DNL Google Ads]. |
| `auth.params.refreshToken` | O token de atualização da sua conta [!DNL Google Ads]. |
| `auth.params.clientID` | A ID de cliente da sua conta [!DNL Google Ads]. |
| `auth.params.clientSecret` | O segredo do cliente da sua conta [!DNL Google Ads]. |
| `auth.params.googleAdsApiVersion` | A versão da API [!DNL Google Ads] que você está usando. A última versão com suporte no Experience Platform é `v17`. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Google Ads]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Criar um fluxo de dados para assimilar dados de publicidade

Seguindo este tutorial, você criou uma conexão de base [!DNL Google Ads] usando a API [!DNL Flow Service] e conectou sua conta do [!DNL Google Ads] à Experience Platform. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de publicidade para o Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/advertising.md)
