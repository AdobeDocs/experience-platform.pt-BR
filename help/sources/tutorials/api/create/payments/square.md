---
keywords: Experience Platform;página inicial;tópicos populares;Quadrado;quadrado
title: Criar uma conexão de base quadrada usando a API do serviço de fluxo
description: Saiba como conectar o Square ao Adobe Experience Platform usando a API do Serviço de fluxo.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 4%

---

# Criar uma conexão de base [!DNL Square] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Square] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Square] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Square], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `host` | A URL da instância [!DNL Square]. |
| `clientId` | A ID do cliente associada à sua conta do [!DNL Square]. |
| `clientSecret` | O segredo do cliente associado à sua conta do [!DNL Square]. |
| `accessToken` | O token de acesso é usado para autenticar sua conta do [!DNL Square] com a autenticação OAuth 2.0. O token de acesso pode ser obtido de [!DNL Square]. |
| `refreshToken` | O token de atualização é usado para gerar novos tokens de acesso depois que o token de acesso atual expira. O token de atualização pode ser obtido de [!DNL Square]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Square] é: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Para obter mais informações sobre essas credenciais e como obtê-las, consulte a [[!DNL Square] documentação sobre OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Square] como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.host` | A URL da instância [!DNL Square]. |
| `auth.params.clientId` | A ID do cliente associada à sua conta do [!DNL Square]. |
| `auth.params.clientSecret` | O segredo do cliente associado à sua conta do [!DNL Square]. |
| `auth.params.accessToken` | O token de acesso é usado para autenticar sua conta do [!DNL Square] com a autenticação OAuth 2.0. O token de acesso pode ser obtido de [!DNL Square]. |
| `auth.params.refreshToken` | O token de atualização é usado para gerar novos tokens de acesso depois que o token de acesso atual expira. O token de atualização pode ser obtido de [!DNL Square]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Square]: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão [!DNL Square] usando a API [!DNL Flow Service] e obteve o valor de identificador exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a [explorar o aplicativo de pagamentos usando a API de Serviço de Fluxo](../../explore/payments.md).
