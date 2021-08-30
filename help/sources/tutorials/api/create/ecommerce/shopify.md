---
keywords: Experience Platform, home, tópicos populares, Shopify, shopify, comércio eletrônico
solution: Experience Platform
title: Criar uma conexão base do conector Shopify usando a API do serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Shopify à Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# Crie uma conexão base [!DNL Shopify] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Shopify] (a seguir chamada &quot;[!DNL Shopify]&quot;) usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Sources]](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL Shopify] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Shopify], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O ponto final do seu servidor [!DNL Shopify]. |
| `accessToken` | O token de acesso para sua conta de usuário [!DNL Shopify]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Shopify] é: `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

Para obter mais informações sobre a introdução, consulte este [Shopify authentication document](https://shopify.dev/concepts/about-apis/authentication).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL Shopify] como parte dos parâmetros da solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Shopify]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.host` | O endpoint do servidor [!DNL Shopify]. |
| `auth.params.accessToken` | O token de acesso para sua conta de usuário [!DNL Shopify]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Shopify]: `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Shopify] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar conexões de eCommerce usando a API do Serviço de Fluxo](../../explore/ecommerce.md).
