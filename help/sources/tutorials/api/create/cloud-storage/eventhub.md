---
keywords: Experience Platform, home, tópicos populares, hub de eventos, hub de eventos do Azure, Hub de eventos
solution: Experience Platform
title: Criar uma conexão de origem de Hubs de Eventos do Azure usando a API do Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma conta de Hubs de Eventos do Azure usando a API do Serviço de Fluxo.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 2%

---


# Crie uma conexão de origem [!DNL Azure Event Hubs] usando a API [!DNL Flow Service]

Este tutorial o orienta pelas etapas para conectar [!DNL Azure Event Hubs] (a seguir denominado &quot;[!DNL Event Hubs]&quot;) ao Experience Platform, usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
- [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar [!DNL Event Hubs] com êxito à Plataforma usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte com sua conta [!DNL Event Hubs], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecida como o nome da chave SAS. |
| `sasKey` | A assinatura de acesso compartilhado gerada. |
| `namespace` | O namespace do [!DNL Event Hubs] que você está acessando. Um namespace [!DNL Event Hubs] fornece um contêiner de escopo exclusivo, no qual você pode criar um ou mais [!DNL Event Hubs]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID da especificação de conexão [!DNL Event Hubs] é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Para obter mais informações sobre esses valores, consulte [este documento de Hubs de Eventos](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

A primeira etapa na criação de uma conexão de origem é autenticar sua fonte [!DNL Event Hubs] e gerar uma ID de conexão básica. Uma ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL Event Hubs] como parte dos parâmetros da solicitação.

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
| `auth.params.namespace` | O namespace do [!DNL Event Hubs] que você está acessando. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Event Hubs] é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Criar uma conexão de origem

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
        "name": "Azure Event Hubs source connection",
        "description": "A source connection for Azure Event Hubs",
        "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser fornecido para incluir mais informações sobre a conexão de origem. |
| `baseConnectionId` | O ID de conexão da sua fonte [!DNL Event Hubs] que foi gerada na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL Event Hubs]. Essa ID é : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | O formato dos dados [!DNL Event Hubs] que você deseja assimilar. Atualmente, o único formato de dados compatível é `json`. |
| `params.eventHubName` | O nome da origem [!DNL Event Hubs]. |
| `params.dataType` | Esse parâmetro define o tipo de dados que está sendo assimilado. Os tipos de dados compatíveis incluem: `raw` e `xdm`. |
| `params.reset` | Esse parâmetro define como os dados serão lidos. Use `latest` para começar a ler a partir dos dados mais recentes e use `earliest` para começar a ler a partir dos primeiros dados disponíveis no fluxo. Esse parâmetro é opcional e o padrão é `earliest` se não for fornecido. |
| `params.consumerGroup` | O mecanismo de publicação ou assinatura a ser usado para [!DNL Event Hubs]. Esse parâmetro é opcional e o padrão é `$Default` se não for fornecido. Consulte este [[!DNL Event Hubs] guia sobre consumidores de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) para obter mais informações. |

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão de origem [!DNL Event Hubs] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão de origem no próximo tutorial para [criar um fluxo de dados de transmissão usando a [!DNL Flow Service] API](../../collect/streaming.md).
