---
keywords: Experience Platform;página inicial;tópicos populares;hubspot;Hubspot
solution: Experience Platform
title: Crie uma conexão básica de HubSpot usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao HubSpot usando a API do Serviço de fluxo.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 5%

---

# Criar uma conexão de base [!DNL HubSpot] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL HubSpot] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL HubSpot] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL HubSpot], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientId` | A ID do cliente associada ao aplicativo [!DNL HubSpot]. |
| `clientSecret` | O segredo do cliente associado ao aplicativo [!DNL HubSpot]. |
| `accessToken` | O token de acesso obtido ao autenticar inicialmente a integração OAuth. |
| `refreshToken` | O token de atualização obtido ao autenticar inicialmente a integração OAuth. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL HubSpot] é: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Para obter mais informações sobre a introdução, consulte este [documento do HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` enquanto fornece suas credenciais de autenticação [!DNL HubSpot] como parte dos parâmetros de solicitação.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.clientSecret` | O segredo do cliente associado ao aplicativo [!DNL HubSpot]. |
| `auth.params.accessToken` | O token de acesso obtido ao autenticar inicialmente a integração OAuth. |
| `auth.params.refreshToken` | O token de atualização obtido ao autenticar inicialmente a integração OAuth. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL HubSpot]: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL HubSpot] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de automação de marketing para a Platform usando a API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
