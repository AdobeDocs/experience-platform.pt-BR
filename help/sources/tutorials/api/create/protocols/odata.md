---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector OData genérico usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---


# Criar um [!DNL Generic OData] conector usando a [!DNL Flow Service] API

>[!NOTE]
>O [!DNL Generic OData] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [!DNL Flow Service] API para guiá-lo pelas etapas para se conectar [!DNL Generic OData] a [!DNL Experience Platform].

## Introdução

Este guia exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao OData usando a [!DNL Flow Service] API.

### Reunir credenciais obrigatórias

Para [!DNL Flow Service] se conectar com OData, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| url | O URL raiz do [!DNL OData] serviço. |
| connectionSpec.id | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL OData] é: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3` |

Para obter mais informações sobre a introdução, consulte [este documento](https://www.odata.org/getting-started/basic-tutorial/)OData.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por [!DNL OData] conta, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma [!DNL OData] conexão, sua ID exclusiva de especificação de conexão deve ser fornecida como parte da solicitação de POST. A ID de especificação de conexão para [!DNL OData] é `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`.

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
| `auth.params.url` | O host do [!DNL OData] servidor. |
| `connectionSpec.id` | A ID da especificação da [!DNL OData] conexão: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma [!DNL OData] conexão usando a [!DNL Flow Service] API e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar os aplicativos de protocolos usando a API](../../explore/protocols.md)do Serviço de Fluxo.