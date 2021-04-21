---
keywords: Experience Platform, home, tópicos populares, Microsoft Dynamics, microsoft dynamics, dinâmica, Dynamics
solution: Experience Platform
title: Criar uma conexão de origem do Microsoft Dynamics usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar a Platform a uma conta do Microsoft Dynamics usando a API de Serviço de Fluxo.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 2%

---

# Crie uma conexão de origem [!DNL Microsoft Dynamics] usando a API [!DNL Flow Service]

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para conectar a Platform a uma conta [!DNL Microsoft Dynamics] (a seguir denominada &quot;Dinâmica&quot;) usando a API do Serviço de fluxo.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito do Platform a uma conta do Dynamics usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Dynamics], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUri` | O URL de serviço da sua instância [!DNL Dynamics]. |
| `username` | O nome de usuário para sua conta de usuário [!DNL Dynamics]. |
| `password` | A senha da sua conta [!DNL Dynamics]. |
| `servicePrincipalId` | A ID do cliente da sua conta [!DNL Dynamics]. Essa ID é necessária ao usar a principal de serviço e a autenticação baseada em chave. |
| `servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |

Para obter mais informações sobre a introdução, visite [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs da plataforma, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos no Experience Platform, incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária por conta [!DNL Dynamics], pois pode ser usada para criar vários fluxos de dados para trazer dados diferentes.

### Criar uma conexão [!DNL Dynamics] usando autenticação básica

Para criar uma conexão [!DNL Dynamics] usando a autenticação básica, faça uma solicitação POST para a API [!DNL Flow Service], fornecendo valores para as `serviceUri`, `username` e `password` da sua conexão.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão [!DNL Dynamics], a ID de especificação de conexão exclusiva deve ser fornecida como parte da solicitação POST. A ID de especificação de conexão para [!DNL Dynamics] é `38ad80fe-8b06-4938-94f4-d4ee80266b07`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.serviceUri` | O URI de serviço associado à instância [!DNL Dynamics]. |
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Dynamics]. |
| `auth.params.password` | A senha associada à sua conta [!DNL Dynamics]. |
| `connectionSpec.id` | A especificação de conexão `id` da sua conta [!DNL Dynamics] recuperada na etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Criar uma conexão [!DNL Dynamics] usando a autenticação baseada em chave principal de serviço

Para criar uma conexão [!DNL Dynamics] usando a autenticação com chave principal de serviço, faça uma solicitação POST para a API [!DNL Flow Service], fornecendo valores para as `serviceUri`, `servicePrincipalId` e `servicePrincipalKey` da sua conexão.

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
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.serviceUri` | O URI de serviço associado à instância [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | A ID do cliente da sua conta [!DNL Dynamics]. Essa ID é necessária ao usar a principal de serviço e a autenticação baseada em chave. |
| `auth.params.servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Dynamics] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar sistemas CRM usando a API do Serviço de Fluxo](../../explore/crm.md).
