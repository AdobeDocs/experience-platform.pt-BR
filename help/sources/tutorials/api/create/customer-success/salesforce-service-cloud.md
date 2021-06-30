---
keywords: Experience Platform, home, tópicos populares, Salesforce Service Cloud, salesforce service cloud
solution: Experience Platform
title: Criar uma conexão de origem da nuvem do Salesforce Service usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform à Salesforce Service Cloud usando a API de Serviço de Fluxo.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: ff0f6bc6b8a57b678b329fe2b47c53919e0e2d64
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# Crie uma conexão de origem [!DNL Salesforce Service Cloud] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Salesforce Service Cloud] usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL Salesforce Service Cloud] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Salesforce Service Cloud], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `username` | O nome de usuário da sua conta de usuário [!DNL Salesforce Service Cloud]. |
| `password` | A senha da sua conta [!DNL Salesforce Service Cloud]. |
| `securityToken` | O token de segurança da sua conta [!DNL Salesforce Service Cloud]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Salesforce Service Cloud] é: `b66ab34-8619-49cb-96d1-39b37ede86ea`. |

Para obter mais informações sobre a introdução, consulte [este documento do Salesforce Service Cloud](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL Salesforce Service Cloud] como parte dos parâmetros da solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Salesforce Service Cloud]:

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
| `auth.params.username` | O nome de usuário associado à sua conta [!DNL Salesforce Service Cloud]. |
| `auth.params.password` | A senha associada à sua conta [!DNL Salesforce Service Cloud]. |
| `auth.params.securityToken` | O token de segurança associado à sua conta [!DNL Salesforce Service Cloud]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Salesforce Service Cloud]: `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seu sistema CRM na próxima etapa.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão [!DNL Salesforce Service Cloud] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão no próximo tutorial à medida que aprende a [explorar sistemas bem-sucedidos do cliente usando a API do Serviço de Fluxo](../../explore/customer-success.md).
