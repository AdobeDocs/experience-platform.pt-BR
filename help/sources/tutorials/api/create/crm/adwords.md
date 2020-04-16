---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector Google AdWords usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: a456dce58c32348c9e680cd672b71dd7bbdc1a04

---


# Criar um conector Google AdWords usando a API de Serviço de Fluxo

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar a Plataforma de experiência ao Google AdWords (a seguir, &quot;AdWords&quot;).

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): A Plataforma de experiência permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao AdWords usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

Para que o Serviço de fluxo se conecte com AdWords, é necessário fornecer valores para as seguintes propriedades de conexão:

| **Credencial** | **Descrição** |
| -------------- | --------------- |
| `clientCustomerID` | A ID do cliente associada ao público alvo Google AdWords | account. |
| `developerToken` | A string usada para identificar um desenvolvedor da API AdWords. |
| `refreshToken` | O token de atualização obtido do Google usado para autorizar o acesso ao AdWords. |
| `clientID` | A ID do aplicativo usada para gerar o token de atualização. |
| `clientSecret` | O segredo do cliente para o aplicativo usado para gerar o token de atualização. |

Para obter mais informações sobre esses valores, consulte este documento [do](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos na plataforma Experience, incluindo os pertencentes ao Serviço de Fluxo, são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Pesquisar especificações de conexão

Para criar uma conexão AdWords, um conjunto de especificações de conexão AdWords deve existir no Serviço de fluxo. A primeira etapa na conexão da Plataforma ao AdWords é recuperar essas especificações.

**Formato da API**

Cada fonte disponível tem seu próprio conjunto exclusivo de especificações de conexão para descrever propriedades do conector, como requisitos de autenticação. Você pode procurar especificações de conexão para AdWords executando uma solicitação GET e usando parâmetros de query.

Enviar uma solicitação GET sem parâmetros de query retornará especificações de conexão para todas as fontes disponíveis. Você pode incluir o query `property=name=="google-adwords"` para obter informações especificamente para o AdWords.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="google-adwords"
```

**Solicitação**

A solicitação a seguir recupera a especificação de conexão para AdWords.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?{QUERY_PARAMS}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a especificação de conexão para AdWords, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão básica.

```json
{
    "items": [
        {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "name": "google-adwords",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for google-adwords",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "clientCustomerID": {
                                "type": "string",
                                "description": "The Client customer ID of the AdWords account"
                            },
                            "developerToken": {
                                "type": "string",
                                "description": "The developer token associated with the manager account",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained from Google for authorizing access to AdWords",
                                "format": "password"
                            },
                            "clientId": {
                                "type": "string",
                                "description": "The client ID of the Google application used to acquire the refresh token"
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret of the google application used to acquire the refresh token",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientCustomerID",
                            "developerToken",
                            "refreshToken",
                            "clientId",
                            "clientSecret"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Criar uma conexão básica

Uma conexão básica especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão básica é necessária por conta AdWords, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-adwords base connection",
        "description": "Base connection for google-adwords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.clientCustomerID` | A ID do cliente da sua conta AdWords. |
| `auth.params.developerToken` | O token de desenvolvedor da sua conta AdWords. |
| `auth.params.refreshToken` | O token de atualização da sua conta AdWords. |
| `auth.params.clientID` | A ID do cliente da sua conta AdWords. |
| `auth.params.clientSecret` | O segredo do cliente da sua conta AdWords. |
| `connectionSpec.id` | A especificação de conexão `id` da sua conta AdWords recuperada na etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão base recém-criada. Essa ID é necessária para explorar os dados do AdWords no próximo tutorial.

```json
{
    "id": "e6ce1eab-416b-4a20-8e1e-ab416b1a206f",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão básica AdWords usando a API de Serviço de Fluxo e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão básica no próximo tutorial à medida que aprende a [explorar sistemas CRM usando a API](../../explore/crm.md)de Serviço de Fluxo.
