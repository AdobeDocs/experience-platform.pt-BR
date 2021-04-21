---
keywords: Experience Platform, home, tópicos populares, hub de eventos, hub de eventos do Azure, Hub de eventos
solution: Experience Platform
title: Criar uma conexão de origem de Hubs de Eventos do Azure usando a API do Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma conta de Hubs de Eventos do Azure usando a API do Serviço de Fluxo.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 2%

---

# Crie uma conexão de origem [!DNL Azure Event Hubs] usando a API [!DNL Flow Service]

>[!NOTE]
>
> O conector [!DNL Azure Event Hubs] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para se conectar [!DNL Experience Platform] a uma conta [!DNL Azure Event Hubs].

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
- [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a uma conta [!DNL Azure Event Hubs] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte com sua conta [!DNL Azure Event Hubs], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecida como o nome da chave SAS. |
| `sasKey` | A assinatura de acesso compartilhado gerada. |
| `namespace` | O namespace dos Hubs de Eventos que você está acessando. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Azure Event Hubs]: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

Para obter mais informações sobre esses valores, consulte [este documento de Hubs de Eventos](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

- `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL Azure Event Hubs], pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.sasKeyName` | O nome da regra de autorização, que também é conhecida como o nome da chave SAS. |
| `auth.params.sasKey` | A assinatura de acesso compartilhado gerada. |
| `namespace` | O namespace do [!DNL Event Hubs] que você está acessando. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Azure Event Hubs]: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados de armazenamento em nuvem no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Azure Event Hubs] usando APIs e uma ID exclusiva foi obtida como parte do corpo da resposta. Você pode usar essa ID de conexão para [coletar dados de transmissão usando a API do Serviço de Fluxo](../../collect/streaming.md).
