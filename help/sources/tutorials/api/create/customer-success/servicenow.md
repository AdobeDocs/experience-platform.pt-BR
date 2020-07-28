---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector ServiceNow usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---


# Criar um [!DNL ServiceNow] conector usando a [!DNL Flow Service] API

>[!NOTE]
>O [!DNL ServiceNow] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [!DNL Flow Service] API para orientá-lo pelas etapas de conexão [!DNL Experience Platform] a um [!DNL ServiceNow] servidor.

## Introdução

Este guia exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um [!DNL ServiceNow] servidor usando a [!DNL Flow Service] API.

### Reunir credenciais obrigatórias

Para [!DNL Flow Service] se conectar a [!DNL ServiceNow], é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O terminal do [!DNL ServiceNow] servidor. |
| `username` | O nome de usuário usado para se conectar ao [!DNL ServiceNow] servidor para autenticação. |
| `password` | A senha para conectar-se ao [!DNL ServiceNow] servidor para autenticação. |

Para obter mais informações sobre a introdução, consulte [este documento](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)ServiceNow.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Pesquisar especificações de conexão

Para criar uma [!DNL ServiceNow] conexão, um conjunto de especificações de [!DNL ServiceNow] conexão deve existir dentro [!DNL Flow Service]. A primeira etapa para conectar-se [!DNL Platform] a [!DNL ServiceNow] é recuperar essas especificações.

**Formato da API**

Cada fonte disponível tem seu próprio conjunto exclusivo de especificações de conexão para descrever propriedades do conector, como requisitos de autenticação. O envio de uma solicitação de GET para o ponto de extremidade `/connectionSpecs` retornará as especificações de conexão para todas as fontes disponíveis. Você também pode incluir o query `property=name=="service-now"` para obter informações especificamente para [!DNL ServiceNow].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="service-now"
```

**Solicitação**

A solicitação a seguir recupera as especificações de conexão para [!DNL ServiceNow].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="service-now"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna as especificações de conexão para [!DNL ServiceNow], incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão básica.

```json
{
    "items": [
        {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "name": "service-now",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to ServiceNow server",
                        "properties": {
                            "endpoint": {
                                "type": "string",
                                "description": "The endpoint of the ServiceNow server (http://<instance>.service-now.com)."
                            },
                            "username": {
                                "type": "string",
                                "description": "The user name used to connect to the ServiceNow server for authentication."
                            },
                            "password": {
                                "type": "string",
                                "description": "password to connect to the ServiceNow server for authentication.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "endpoint",
                            "username",
                            "password"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Criar uma conexão básica

Uma conexão básica especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão básica é necessária por [!DNL ServiceNow] conta, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for service-now",
        "description": "Base connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| ------------- | --------------- |
| `auth.params.server` | O terminal do seu [!DNL ServiceNow] servidor. |
| `auth.params.username` | O nome de usuário usado para se conectar ao [!DNL ServiceNow] servidor para autenticação. |
| `auth.params.password` | A senha para conectar-se ao [!DNL ServiceNow] servidor para autenticação. |
| `connectionSpec.id` | A ID da especificação de conexão associada ao [!DNL ServiceNow]. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão básica recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar o CRM na próxima etapa.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL ServiceNow] básica usando a [!DNL Flow Service] API e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão básica no próximo tutorial à medida que aprende a [explorar sistemas bem-sucedidos do cliente usando a API](../../explore/customer-success.md)de Serviço de Fluxo.