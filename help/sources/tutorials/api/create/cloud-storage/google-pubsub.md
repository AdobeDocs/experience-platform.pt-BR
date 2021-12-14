---
keywords: Experience Platform, home, tópicos populares, Google PubSub, google pubsub
solution: Experience Platform
title: Criar uma conexão Google PubSub-source usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma conta Google PubSub usando a API de Serviço de Fluxo.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 2%

---

# Crie um [!DNL Google PubSub] Conexão de origem usando a API de serviço de fluxo

>[!NOTE]
>
>O [!DNL Google PubSub] O conector está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Este tutorial o orienta pelas etapas para se conectar [!DNL Google PubSub] (a seguir designado por &quot;[!DNL PubSub]&quot;) para Experience Platform, usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL PubSub] para a plataforma usando a [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para se conectar a [!DNL PubSub], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `projectId` | A ID do projeto necessária para autenticação [!DNL PubSub]. |
| `credentials` | A credencial ou chave necessária para a autenticação [!DNL PubSub]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem do target. O [!DNL PubSub] a ID de especificação de conexão é: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Para obter mais informações sobre esses valores, consulte esta seção [[!DNL PubSub] autenticação](https://cloud.google.com/pubsub/docs/authentication) documento. Para usar a autenticação baseada em conta de serviço, consulte esta seção [[!DNL PubSub] guia sobre a criação de contas de serviço](https://cloud.google.com/docs/authentication/production#create_service_account) para obter etapas sobre como gerar suas credenciais.

>[!TIP]
>
>Se estiver usando a autenticação baseada em conta de serviço, certifique-se de ter concedido acesso suficiente ao usuário à sua conta de serviço e de não haver espaços em branco adicionais no JSON, ao copiar e colar suas credenciais.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

A primeira etapa na criação de uma conexão de origem é autenticar seu [!DNL PubSub] e gerar uma ID de conexão básica. Uma ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL PubSub] credenciais de autenticação como parte dos parâmetros da solicitação.

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
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.projectId` | A ID do projeto necessária para autenticação [!DNL PubSub]. |
| `auth.params.credentials` | A credencial ou chave necessária para a autenticação [!DNL PubSub]. |
| `connectionSpec.id` | O [!DNL PubSub] ID de especificação de conexão: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão básica é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Criar uma conexão de origem {#source}

Uma conexão de origem cria e gerencia a conexão com a fonte externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e uma ID de conexão de origem necessária para criar um fluxo de dados. Uma instância de conexão de origem é específica de um locatário e da Organização IMS.

Para criar uma conexão de origem, faça uma solicitação de POST para a variável `/sourceConnections` endpoint da variável [!DNL Flow Service] API.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_Org}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Google PubSub source connection",
        "description": "A source connection for Google PubSub",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser fornecido para incluir mais informações sobre a conexão de origem. |
| `baseConnectionId` | A ID de conexão básica da [!DNL PubSub] fonte gerada na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL PubSub]. Essa ID é: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | O formato do [!DNL PubSub] dados que você deseja assimilar. Atualmente, o único formato de dados compatível é `json`. |
| `params.topicId` | A ID do tópico define o recurso nomeado específico para o qual as mensagens são enviadas por editores |
| `params.subscriptionId` | A ID de assinatura define o recurso nomeado específico que representa o fluxo de mensagens de um único tópico específico a ser entregue ao aplicativo de assinatura. |
| `params.dataType` | Esse parâmetro define o tipo de dados que está sendo assimilado. Os tipos de dados compatíveis incluem: `raw` e `xdm`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária no próximo tutorial para criar um fluxo de dados.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL PubSub] conexão de origem usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão de origem no próximo tutorial para [crie um fluxo de dados de transmissão usando o [!DNL Flow Service] API](../../collect/streaming.md).
