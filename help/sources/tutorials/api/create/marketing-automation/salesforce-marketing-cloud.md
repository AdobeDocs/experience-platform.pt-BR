---
keywords: Experience Platform, home, tópicos populares, salesforce marketing cloud, Marketing Cloud Salesforce
solution: Experience Platform
title: Criar uma conexão base de Marketing Cloud do Salesforce usando a API do Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Salesforce Marketing Cloud usando a API de Serviço de Fluxo.
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# Crie uma conexão base [!DNL Salesforce Marketing Cloud] usando a API [!DNL Flow Service]

>[!NOTE]
>
>A origem [!DNL Salesforce Marketing Cloud] está em beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Salesforce Marketing Cloud] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito a [!DNL Salesforce Marketing Cloud] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Salesforce Marketing Cloud], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O servidor host do seu aplicativo. Esse é frequentemente o seu subdomínio. |
| `clientId` | A ID do cliente associada ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | O segredo do cliente associado ao seu aplicativo [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Salesforce Marketing Cloud] é: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL Salesforce Marketing Cloud] como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "cea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.clientId` | A ID do cliente associada ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | O segredo do cliente associado ao seu aplicativo [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Salesforce Marketing Cloud]: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Ao seguir este tutorial, você criou uma conexão [!DNL Salesforce Marketing Cloud] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar sistemas de automação de marketing usando a API do Serviço de Fluxo](../../explore/marketing-automation.md).
