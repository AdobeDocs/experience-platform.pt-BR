---
keywords: Experience Platform, home, tópicos populares, google adwords, Google AdWords, adwords
solution: Experience Platform
title: Criar uma conexão básica do Google AdWords usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Google AdWords usando a API do Serviço de fluxo.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# Crie uma conexão base [!DNL Google AdWords] usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Google AdWords] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Google AdWords] (a seguir chamada &quot;[!DNL AdWords]&quot;) usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL AdWords] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL AdWords], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientCustomerId` | A ID do cliente da conta [!DNL AdWords]. |
| `developerToken` | O token do desenvolvedor associado à conta do gerente. |
| `refreshToken` | O token de atualização obtido de [!DNL Google] para autorizar acesso a [!DNL AdWords]. |
| `clientId` | A ID do cliente do aplicativo [!DNL Google] usada para adquirir o token de atualização. |
| `clientSecret` | O segredo do cliente do aplicativo [!DNL Google] usado para adquirir o token de atualização. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL AdWords] é: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Para obter mais informações sobre esses valores, consulte este [documento do Google AdWords](https://developers.google.com/adwords/api/docs/guides/authentication).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL AdWords] como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL AdWords]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
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
| `auth.params.clientCustomerID` | A ID do cliente da sua conta [!DNL AdWords]. |
| `auth.params.developerToken` | O token do desenvolvedor da sua conta [!DNL AdWords]. |
| `auth.params.refreshToken` | O token de atualização da sua conta [!DNL AdWords]. |
| `auth.params.clientID` | A ID do cliente da sua conta [!DNL AdWords]. |
| `auth.params.clientSecret` | O segredo do cliente da sua conta [!DNL AdWords]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Google AdWords]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão base [!DNL AdWords] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar sistemas publicitários usando a API do Serviço de Fluxo](../../explore/advertising.md).
