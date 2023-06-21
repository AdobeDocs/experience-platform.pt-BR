---
title: Criar uma conexão de origem dos Hubs de eventos do Azure usando a API do Serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a uma conta do Azure Event Hubs usando a API do Serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b76bc6ddb0d49bbd089627c8df8b31703d0e50b1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# Criar um [!DNL Azure Event Hubs] conexão de origem usando o [!DNL Flow Service] API

>[!IMPORTANT]
>
>A variável [!DNL Azure Event Hubs] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial guiará você pelas etapas para se conectar [!DNL Azure Event Hubs] (a seguir designado por &quot;[!DNL Event Hubs]&quot;) para Experience Platform, usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
- [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL Event Hubs] para a Platform usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com o seu [!DNL Event Hubs] você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecido como o nome da chave SAS. |
| `sasKey` | A chave primária do [!DNL Event Hubs] namespace. A variável `sasPolicy` que o `sasKey` corresponde a deve ter `manage` direitos configurados para a variável [!DNL Event Hubs] lista a ser preenchida. |
| `namespace` | O namespace do [!DNL Event Hubs] que você está acessando. Um [!DNL Event Hubs] O namespace fornece um contêiner de escopo exclusivo, no qual você pode criar um ou mais [!DNL Event Hubs]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A variável [!DNL Event Hubs] A ID da especificação de conexão é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Para obter mais informações sobre esses valores, consulte [este documento de Hubs de Eventos](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

A primeira etapa na criação de uma conexão de origem é autenticar seu [!DNL Event Hubs] origem e gere uma ID de conexão básica. Uma ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL Event Hubs] credenciais de autenticação como parte dos parâmetros de solicitação.

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
| `auth.params.sasKeyName` | O nome da regra de autorização, que também é conhecido como o nome da chave SAS. |
| `auth.params.sasKey` | A assinatura de acesso compartilhado gerada. |
| `auth.params.namespace` | O namespace do [!DNL Event Hubs] que você está acessando. |
| `connectionSpec.id` | A variável [!DNL Event Hubs] A ID da especificação de conexão é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Criar uma conexão de origem

>[!TIP]
>
>Um [!DNL Event Hubs] o grupo de consumidores só pode ser usado para um único fluxo em um determinado momento.

Uma conexão de origem cria e gerencia a conexão com a origem externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e uma ID de conexão de origem necessária para criar um fluxo de dados. Uma instância de conexão de origem é específica para um locatário e uma organização.

Para criar uma conexão de origem, faça uma solicitação POST ao `/sourceConnections` endpoint do [!DNL Flow Service] API.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `baseConnectionId` | A ID da conexão do [!DNL Event Hubs] que foi gerado na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL Event Hubs]. Essa ID é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | O formato do [!DNL Event Hubs] dados que você deseja assimilar. No momento, o único formato de dados compatível é `json`. |
| `params.eventHubName` | O nome do seu [!DNL Event Hubs] origem. |
| `params.dataType` | Esse parâmetro define o tipo de dados que está sendo assimilado. Os tipos de dados compatíveis incluem: `raw` e `xdm`. |
| `params.reset` | Esse parâmetro define como os dados serão lidos. Uso `latest` para começar a ler os dados mais recentes e use `earliest` para começar a ler os primeiros dados disponíveis no fluxo. Esse parâmetro é opcional e assume como padrão `earliest` se não fornecido. |
| `params.consumerGroup` | O mecanismo de publicação ou subscrição a ser usado para [!DNL Event Hubs]. Esse parâmetro é opcional e assume como padrão `$Default` se não fornecido. Consulte esta [[!DNL Event Hubs] guia sobre consumidores de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) para obter mais informações. **Nota**: Um [!DNL Event Hubs] o grupo de consumidores só pode ser usado para um único fluxo em um determinado momento. |

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Event Hubs] conexão de origem usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão de origem no próximo tutorial para [crie um fluxo de dados de transmissão usando o [!DNL Flow Service] API](../../collect/streaming.md).
