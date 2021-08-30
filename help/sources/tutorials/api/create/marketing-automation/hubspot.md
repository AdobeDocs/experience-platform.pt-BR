---
keywords: Experience Platform, home, tópicos populares, hubspot, Hubspot
solution: Experience Platform
title: Criar uma conexão base HubSpot usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao HubSpot usando a API do Serviço de Fluxo.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# Crie uma conexão base [!DNL HubSpot] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL HubSpot] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL HubSpot] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL HubSpot], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientId` | A ID do cliente associada ao aplicativo [!DNL HubSpot]. |
| `clientSecret` | O segredo do cliente associado ao seu aplicativo [!DNL HubSpot]. |
| `accessToken` | O token de acesso obtido ao autenticar inicialmente sua integração OAuth. |
| `refreshToken` | O token de atualização obtido ao autenticar inicialmente sua integração OAuth. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL HubSpot] é: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Para obter mais informações sobre a introdução, consulte este [documento HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL HubSpot] como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL HubSpot]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.clientId` | A ID do cliente associada ao aplicativo [!DNL HubSpot]. |
| `auth.params.clientSecret` | O segredo do cliente associado ao seu aplicativo [!DNL HubSpot]. |
| `auth.params.accessToken` | O token de acesso obtido ao autenticar inicialmente sua integração OAuth. |
| `auth.params.refreshToken` | O token de atualização obtido ao autenticar inicialmente sua integração OAuth. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL HubSpot]: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Ao seguir este tutorial, você criou uma conexão [!DNL HubSpot] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar sistemas de automação de marketing usando a API do Serviço de Fluxo](../../explore/marketing-automation.md).
