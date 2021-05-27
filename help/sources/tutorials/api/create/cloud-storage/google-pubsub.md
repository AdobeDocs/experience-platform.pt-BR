---
keywords: Experience Platform, home, tópicos populares, Google PubSub, google pubsub
solution: Experience Platform
title: Criar uma conexão do Google PubSub-Source usando a API do Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma conta do Google PubSub usando a API de Serviço de Fluxo.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: f13afbd70db18e5faa1a101300f3dc7ec944baa3
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Google PubSub] usando a API do Serviço de fluxo

>[!NOTE]
>
>O conector [!DNL Google PubSub] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Este tutorial o orienta pelas etapas para conectar [!DNL Google PubSub] (a seguir denominado &quot;[!DNL PubSub]&quot;) ao Experience Platform, usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar [!DNL PubSub] com êxito à Plataforma usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL PubSub], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `projectId` | A ID do projeto necessária para autenticar [!DNL PubSub]. |
| `credentials` | A credencial ou chave necessária para autenticar [!DNL PubSub]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem do target. A ID da especificação de conexão [!DNL PubSub] é: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Para obter mais informações sobre esses valores, consulte este documento [[!DNL PubSub] authentication](https://cloud.google.com/pubsub/docs/authentication). Para usar a autenticação baseada em conta de serviço, consulte este [[!DNL PubSub] guia sobre a criação de contas de serviço](https://cloud.google.com/docs/authentication/production#create_service_account) para obter as etapas sobre como gerar suas credenciais.

>[!TIP]
>
>Se estiver usando a autenticação baseada em conta de serviço, certifique-se de ter concedido acesso suficiente ao usuário à sua conta de serviço e de não haver espaços em branco adicionais no JSON, ao copiar e colar suas credenciais.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

A primeira etapa na criação de uma conexão de origem é autenticar sua fonte [!DNL PubSub] e gerar uma ID de conexão básica. Uma ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL PubSub] como parte dos parâmetros da solicitação.

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
| `auth.params.projectId` | A ID do projeto necessária para autenticar [!DNL PubSub]. |
| `auth.params.credentials` | A credencial ou chave necessária para autenticar [!DNL PubSub]. |
| `connectionSpec.id` | A ID de especificação da conexão [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

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

Para criar uma conexão de origem, faça uma solicitação de POST ao endpoint `/sourceConnections` da API [!DNL Flow Service].

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
| `baseConnectionId` | A ID de conexão básica da fonte [!DNL PubSub] gerada na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL PubSub]. Essa ID é : `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | O formato dos dados [!DNL PubSub] que você deseja assimilar. Atualmente, o único formato de dados compatível é `json`. |
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

Ao seguir este tutorial, você criou uma conexão de origem [!DNL PubSub] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão de origem no próximo tutorial para [criar um fluxo de dados de transmissão usando a [!DNL Flow Service] API](../../collect/streaming.md).
