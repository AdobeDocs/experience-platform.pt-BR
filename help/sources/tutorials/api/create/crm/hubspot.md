---
keywords: Experience Platform;home;popular topics;hubspot;Hubspot
solution: Experience Platform
title: Criar um conector HubSpot usando a API de Serviço de Fluxo
topic: overview
description: Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar o Experience Platform ao HubSpot.
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---


# Criar um [!DNL HubSpot] conector usando a [!DNL Flow Service] API

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [!DNL Flow Service] API para guiá-lo pelas etapas para se conectar [!DNL Experience Platform] a [!DNL HubSpot].

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL HubSpot] usando a [!DNL Flow Service] API.

### Reunir credenciais obrigatórias

Para [!DNL Flow Service] se conectar com [!DNL HubSpot], é necessário fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientId` | A ID do cliente associada ao seu [!DNL HubSpot] aplicativo. |
| `clientSecret` | O segredo do cliente associado ao seu [!DNL HubSpot] aplicativo. |
| `accessToken` | O token de acesso obtido ao autenticar inicialmente sua integração OAuth. |
| `refreshToken` | O token de atualização obtido ao autenticar inicialmente sua integração OAuth. |

Para obter mais informações sobre a introdução, consulte este documento [HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Pesquisar especificações de conexão

Para criar uma [!DNL HubSpot] conexão, um conjunto de especificações de [!DNL HubSpot] conexão deve existir dentro [!DNL Flow Service]. A primeira etapa para conectar-se [!DNL Platform] a [!DNL HubSpot] é recuperar essas especificações.

**Formato da API**

Cada fonte disponível tem seu próprio conjunto exclusivo de especificações de conexão para descrever propriedades do conector, como requisitos de autenticação. O envio de uma solicitação de GET para o ponto de extremidade `/connectionSpecs` retornará as especificações de conexão para todas as fontes disponíveis. Você também pode incluir o query `property=name=="hubspot"` para obter informações especificamente para [!DNL HubSpot].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="hubspot"
```

**Solicitação**

A solicitação a seguir recupera as especificações de conexão para [!DNL HubSpot].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="hubspot"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a especificação de conexão para [!DNL HubSpot], incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão para a API.

```json
{
    "items": [
        {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "name": "hubspot",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to HubSpot",
                        "properties": {
                            "clientId": {
                                "type": "string",
                                "description": "The client ID associated with your HubSpot application."
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret associated with your HubSpot application.",
                                "format": "password"
                            },
                            "accessToken": {
                                "type": "string",
                                "description": "The access token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientId",
                            "clientSecret",
                            "accessToken",
                            "refreshToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Criar uma conexão para a API

Uma conexão para a API especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão para a API é necessária por [!DNL HubSpot] conta, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
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
| `auth.params.clientId` | A ID do cliente associada ao seu [!DNL HubSpot] aplicativo. |
| `auth.params.clientSecret` | O segredo do cliente associado ao seu [!DNL HubSpot] aplicativo. |
| `auth.params.accessToken` | O token de acesso obtido ao autenticar inicialmente sua integração OAuth. |
| `auth.params.refreshToken` | O token de atualização obtido ao autenticar inicialmente sua integração OAuth. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada para a API, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2eb9c78b-e8b8-4400-b9c7-8be8b86400b2",
    "etag": "\"05026cf5-0000-0200-0000-5e4c42920000\""
}
```

Ao seguir este tutorial, você criou uma [!DNL HubSpot] conexão usando a [!DNL Flow Service] API e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar sistemas CRM usando a API](../../explore/crm.md)de Serviço de Fluxo.