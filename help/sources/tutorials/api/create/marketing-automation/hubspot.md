---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector HubSpot usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# Criar um conector HubSpot usando a API de Serviço de Fluxo

>[!NOTE]
>O conector HubSpot está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar o Experience Platform ao HubSpot.

## Introdução

Este guia exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, ao mesmo tempo em que lhe fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços Platform.
* [Caixas de proteção](../../../../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao HubSpot usando a API de Serviço de Fluxo.

### Reunir credenciais obrigatórias

Para que o Serviço de Fluxo se conecte ao HubSpot, é necessário fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| ID do cliente | A ID do cliente associada ao aplicativo HubSpot. |
| Segredo do cliente | O segredo do cliente associado ao aplicativo HubSpot. |
| Token de acesso | O token de acesso obtido ao autenticar inicialmente sua integração OAuth. |
| Atualizar token | O token de atualização obtido ao autenticar inicialmente sua integração OAuth. |
| ID da especificação da conexão | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para HubSpot é: `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Para obter mais informações sobre a introdução, consulte este documento [HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para as APIs da Platform, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform, incluindo os pertencentes ao Serviço de Fluxo, são isolados para caixas de proteção virtuais específicas. Todas as solicitações às APIs do Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta HubSpot, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```https
POST /connections
```

**Solicitação**

Para criar uma conexão HubSpot, sua ID exclusiva de especificação de conexão deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para HubSpot é `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

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
| `auth.params.clientId` | A ID do cliente associada ao aplicativo HubSpot. |
| `auth.params.clientSecret` | O segredo do cliente associado ao aplicativo HubSpot. |
| `auth.params.accessToken` | O token de acesso obtido ao autenticar inicialmente sua integração OAuth. |
| `auth.params.refreshToken` | O token de atualização obtido ao autenticar inicialmente sua integração OAuth. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada para a API, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Ao seguir este tutorial, você criou uma conexão HubSpot usando a API de Serviço de Fluxo e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar os sistemas de automação de marketing usando a API](../../explore/marketing-automation.md)de Serviço de Fluxo.