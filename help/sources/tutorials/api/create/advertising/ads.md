---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector Google AdWords usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---


# Criar um conector Google AdWords usando a API de Serviço de Fluxo

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar a Plataforma de experiência ao Google AdWords.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): A Plataforma de experiência permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao anúncio usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

Para que o Serviço de fluxo se conecte com AdWords, é necessário fornecer valores para as seguintes propriedades de conexão:

| **Credencial** | **Descrição** |
| -------------- | --------------- |
| ID do cliente | A ID do cliente do cliente da conta AdWords. |
| Token do desenvolvedor | O token do desenvolvedor associado à conta do gerente. |
| Atualizar token | O token de atualização obtido do Google para autorizar o acesso ao AdWords. |
| ID do cliente | A ID do cliente do aplicativo Google usada para adquirir o token de atualização. |
| Segredo do cliente | O segredo do cliente do aplicativo google usado para adquirir o token de atualização. |
| ID da especificação da conexão | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para Google AdWords é: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Para obter mais informações sobre esses valores, consulte este documento [do](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos na plataforma Experience, incluindo os pertencentes ao Serviço de fluxo, estão isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta do Google AdWords, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma nova conexão AdWords, configurada pelas propriedades fornecidas na carga:


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
| `auth.params.clientCustomerID` | A ID do cliente da sua conta AdWords. |
| `auth.params.developerToken` | O token de desenvolvedor da sua conta AdWords. |
| `auth.params.refreshToken` | O token de atualização da sua conta AdWords. |
| `auth.params.clientID` | A ID do cliente da sua conta AdWords. |
| `auth.params.clientSecret` | O segredo do cliente da sua conta AdWords. |
| `connectionSpec.id` | A ID de especificação de conexão do Google AdWords: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão Google AdWords usando a API de Serviço de Fluxo e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar sistemas de publicidade usando a API](../../explore/advertising.md)de Serviço de Fluxo.
