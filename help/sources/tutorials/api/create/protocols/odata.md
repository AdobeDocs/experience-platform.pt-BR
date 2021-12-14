---
keywords: Experience Platform, home, tópicos populares, Generic OData, dados genéricos
solution: Experience Platform
title: Criar uma conexão básica OData genérica usando a API do serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar OData genérico ao Adobe Experience Platform usando a API do Serviço de fluxo.
exl-id: 45b302cb-1a43-4fab-a8a2-cb4e1ee129f9
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 2%

---

# Crie um [!DNL Generic OData] conexão básica usando o [!DNL Flow Service] API

>[!NOTE]
>
>O [!DNL Generic OData] O conector está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Generic OData] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Generic OData] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Generic OData], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL raiz da variável [!DNL Generic OData] serviço. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Generic Generic OData] é: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Generic OData] documento](https://www.odata.org/getting-started/basic-tutorial/).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Generic OData] credenciais de autenticação como parte dos parâmetros da solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Generic OData]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Protocols",
        "description": "A test connection for a Protocols source",
        "auth": {
            "specName": "Anonymous Authentication",
        "params": {
            "url":  "{URL}"
            }
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.url` | O host do [!DNL Generic OData] servidor. |
| `connectionSpec.id` | O [!DNL Generic OData] ID de especificação de conexão: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL OData] conexão usando o [!DNL Flow Service] API e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a usar [explore aplicativos de protocolos usando a API do Serviço de Fluxo](../../explore/protocols.md).
