---
keywords: Experience Platform, home, tópicos populares, ssc, SSC, Salesforce Service Cloud, salesforce service cloud
solution: Experience Platform
title: Criar uma conexão de origem da nuvem do Salesforce Service usando a API do Serviço de fluxo
topic: visão geral
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform à Salesforce Service Cloud usando a API de Serviço de Fluxo.
translation-type: tm+mt
source-git-commit: a0b016e8adc519bc79701f9fd850b6ddf7d46127
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 2%

---


# Crie uma conexão de origem [!DNL Salesforce Service Cloud] usando a API [!DNL Flow Service]

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para se conectar [!DNL Experience Platform] a [!DNL Salesforce Service Cloud] (a seguir chamada &quot;SSC&quot;).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao SSC usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte ao SSC, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `username` | O nome de usuário da conta de usuário. |
| `password` | A senha da conta de usuário. |
| `securityToken` | O token de segurança da conta do usuário. |

Para obter mais informações sobre a introdução, consulte [este documento do Salesforce Service Cloud](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

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

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta SSC, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão SSC, a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para SSC é `b66ab34-8619-49cb-96d1-39b37ede86ea`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.username` | O nome de usuário associado à sua conta SSC. |
| `auth.params.password` | A senha associada à sua conta do SSC. |
| `auth.params.securityToken` | O token de segurança associado à sua conta SSC. |
| `connectionSpec.id` | A especificação de conexão `id` da sua conta SSC recuperada na etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão SSC usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar sistemas bem-sucedidos do cliente usando a API do Serviço de Fluxo](../../explore/customer-success.md).
