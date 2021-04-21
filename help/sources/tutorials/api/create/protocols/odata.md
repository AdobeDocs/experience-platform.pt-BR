---
keywords: Experience Platform, home, tópicos populares, Generic OData, dados genéricos
solution: Experience Platform
title: Criar uma conexão de fonte OData genérica usando a API do serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar OData genérico ao Adobe Experience Platform usando a API do Serviço de fluxo.
exl-id: 45b302cb-1a43-4fab-a8a2-cb4e1ee129f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 2%

---

# Crie uma conexão de origem [!DNL Generic OData] usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Generic OData] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para se conectar [!DNL Generic OData] a [!DNL Experience Platform].

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao OData usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte com OData, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL raiz do serviço [!DNL OData]. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL OData] é: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3` |

Para obter mais informações sobre a introdução, consulte [este documento OData](https://www.odata.org/getting-started/basic-tutorial/).

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL OData], pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL OData], a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para [!DNL OData] é `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`.

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
            "url" :  "{URL}"
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
| `auth.params.url` | O host do servidor [!DNL OData]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL OData]: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL OData] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar aplicativos de protocolos usando a API do Serviço de Fluxo](../../explore/protocols.md).
