---
keywords: Experience Platform, home, tópicos populares, google adwords, Google AdWords, adwords
solution: Experience Platform
title: Criar uma conexão de origem do Google AdWords usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Google AdWords usando a API do Serviço de fluxo.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Crie uma conexão de origem [!DNL Google AdWords] usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Google AdWords] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para se conectar [!DNL Experience Platform] a [!DNL Google AdWords].

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao Anúncio usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte ao AdWords, você deve fornecer valores para as seguintes propriedades de conexão:

| **Credencial** | **Descrição** |
| -------------- | --------------- |
| `clientCustomerId` | A ID do cliente da conta do AdWords. |
| `developerToken` | O token do desenvolvedor associado à conta do gerente. |
| `refreshToken` | O token de atualização obtido de [!DNL Google] para autorizar o acesso ao AdWords. |
| `clientId` | A ID do cliente do aplicativo [!DNL Google] usada para adquirir o token de atualização. |
| `clientSecret` | O segredo do cliente do aplicativo [!DNL Google] usado para adquirir o token de atualização. |
| `connectionSpec` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Google AdWords] é: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Para obter mais informações sobre esses valores, consulte este [documento do Google AdWords](https://developers.google.com/adwords/api/docs/guides/authentication).

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL Google AdWords], pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```https
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL Google AdWords], a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para [!DNL Google AdWords] é `d771e9c1-4f26-40dc-8617-ce58c4b53702`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
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

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Google AdWords] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar sistemas publicitários usando a API do Serviço de Fluxo](../../explore/advertising.md).
