---
keywords: Experience Platform, home, tópicos populares, Quadrado, quadrado
title: Criar uma conexão base quadrada usando a API do Serviço de fluxo
description: Saiba como conectar Quadrado ao Adobe Experience Platform usando a API de Serviço de Fluxo.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%

---

# Crie um [!DNL Square] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Square] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Square] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Square], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `host` | O URL do [!DNL Square] instância. |
| `clientId` | A ID do cliente associada à [!DNL Square] conta. |
| `clientSecret` | O segredo do cliente associado ao seu [!DNL Square] conta. |
| `accessToken` | O token de acesso é usado para autenticar seu [!DNL Square] com autenticação OAuth 2.0. O token de acesso pode ser obtido de [!DNL Square]. |
| `refreshToken` | O token de atualização é usado para gerar novos tokens de acesso depois que o token de acesso atual expirar. O token de atualização pode ser obtido de [!DNL Square]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Square] é: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Para obter mais informações sobre essas credenciais e como obtê-las, consulte o [[!DNL Square] documentação sobre o OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Square] credenciais de autenticação como parte dos parâmetros da solicitação.

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
| `auth.params.host` | O URL do [!DNL Square] instância. |
| `auth.params.clientId` | A ID do cliente associada à [!DNL Square] conta. |
| `auth.params.clientSecret` | O segredo do cliente associado ao seu [!DNL Square] conta. |
| `auth.params.accessToken` | O token de acesso é usado para autenticar seu [!DNL Square] com autenticação OAuth 2.0. O token de acesso pode ser obtido de [!DNL Square]. |
| `auth.params.refreshToken` | O token de atualização é usado para gerar novos tokens de acesso depois que o token de acesso atual expirar. O token de atualização pode ser obtido de [!DNL Square]. |
| `connectionSpec.id` | O [!DNL Square] ID de especificação de conexão: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Square] conexão usando o [!DNL Flow Service] API e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a usar [explorar aplicativos de pagamentos usando a API do Serviço de Fluxo](../../explore/payments.md).
