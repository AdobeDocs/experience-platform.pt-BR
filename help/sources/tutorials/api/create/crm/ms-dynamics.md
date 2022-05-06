---
keywords: Experience Platform, home, tópicos populares, Microsoft Dynamics, microsoft dynamics, dinâmica, Dynamics
solution: Experience Platform
title: Criar uma conexão básica do Microsoft Dynamics usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar a Platform a uma conta do Microsoft Dynamics usando a API de Serviço de Fluxo.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# Crie um [!DNL Microsoft Dynamics] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Microsoft Dynamics] (a seguir designado por &quot;[!DNL Dynamics]&quot;) usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito do Platform a uma conta do Dynamics usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para se conectar a [!DNL Dynamics], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUri` | O URL de serviço do [!DNL Dynamics] instância. |
| `username` | O nome de usuário para seu [!DNL Dynamics] conta do usuário. |
| `password` | A senha de seu [!DNL Dynamics] conta. |
| `servicePrincipalId` | A ID de cliente do [!DNL Dynamics] conta. Essa ID é necessária ao usar a principal de serviço e a autenticação baseada em chave. |
| `servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Dynamics] é: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Para obter mais informações sobre a introdução, visite [this [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Dynamics] credenciais de autenticação como parte dos parâmetros da solicitação.

### Crie um [!DNL Dynamics] conexão básica usando autenticação básica

Para criar um [!DNL Dynamics] conexão básica usando autenticação básica, faça uma solicitação de POST para [!DNL Flow Service] API enquanto fornece valores para o `serviceUri`, `username`e `password`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | O URI de serviço associado ao [!DNL Dynamics] instância. |
| `auth.params.username` | O nome de usuário associado à [!DNL Dynamics] conta. |
| `auth.params.password` | A senha associada à sua [!DNL Dynamics] conta. |
| `connectionSpec.id` | O [!DNL Dynamics] ID de especificação de conexão: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Crie um [!DNL Dynamics] conexão básica usando autenticação baseada na chave principal de serviço

Para criar um [!DNL Dynamics] conexão básica usando a autenticação baseada na chave principal de serviço, faça uma solicitação POST para o [!DNL Flow Service] API enquanto fornece valores para o `serviceUri`, `servicePrincipalId`e `servicePrincipalKey`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | O URI de serviço associado ao [!DNL Dynamics] instância. |
| `auth.params.servicePrincipalId` | A ID de cliente do [!DNL Dynamics] conta. Essa ID é necessária ao usar a principal de serviço e a autenticação baseada em chave. |
| `auth.params.servicePrincipalKey` | A chave secreta da entidade de serviço. Essa credencial é necessária ao usar a entidade de serviço e a autenticação baseada em chave. |
| `connectionSpec.id` | O [!DNL Dynamics] ID de especificação de conexão: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Microsoft Dynamics] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do CRM para a plataforma usando o [!DNL Flow Service] API](../../collect/crm.md)
