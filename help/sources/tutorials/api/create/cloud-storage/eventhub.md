---
title: Criar uma conexão do Source com os Hubs de Eventos do Azure usando a API do Serviço de Fluxo
description: Saiba como conectar o Adobe Experience Platform a uma conta do Azure Event Hubs usando a API do Serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL Azure Event Hubs] usando a API [!DNL Flow Service]

>[!IMPORTANT]
>
>A origem [!DNL Azure Event Hubs] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Leia este tutorial para saber como conectar [!DNL Azure Event Hubs] (a seguir denominado &quot;[!DNL Event Hubs]&quot;) ao Experience Platform, usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

- [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
- [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Event Hubs] ao Experience Platform usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte à sua conta [!DNL Event Hubs], você deve fornecer valores para as seguintes propriedades de conexão:

>[!BEGINTABS]

>[!TAB Autenticação padrão]

| Credencial | Descrição |
| --- | --- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecido como o nome da chave SAS. |
| `sasKey` | A chave primária do namespace [!DNL Event Hubs]. O `sasPolicy` ao qual `sasKey` corresponde deve ter direitos `manage` configurados para que a lista [!DNL Event Hubs] seja preenchida. |
| `namespace` | O namespace do [!DNL Event Hub] que você está acessando. Um namespace [!DNL Event Hub] fornece um contêiner de escopo exclusivo, no qual você pode criar um ou mais [!DNL Event Hubs]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão [!DNL Event Hubs] é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB Autenticação SAS]

| Credencial | Descrição |
| --- | --- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecido como o nome da chave SAS. |
| `sasKey` | A chave primária do namespace [!DNL Event Hubs]. O `sasPolicy` ao qual `sasKey` corresponde deve ter direitos `manage` configurados para que a lista [!DNL Event Hubs] seja preenchida. |
| `namespace` | O namespace do [!DNL Event Hub] que você está acessando. Um namespace [!DNL Event Hub] fornece um contêiner de escopo exclusivo, no qual você pode criar um ou mais [!DNL Event Hubs]. |
| `eventHubName` | Preencha seu nome [!DNL Azure Event Hub]. Leia a [documentação do Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) para obter mais informações sobre os nomes de [!DNL Event Hub]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão [!DNL Event Hubs] é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Para obter mais informações sobre a autenticação SAS (assinaturas de acesso compartilhado) para [!DNL Event Hubs], leia o [[!DNL Azure] guia sobre como usar SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Autenticação do Ative Diretory do Azure Hub de Eventos]

| Credencial | Descrição |
| --- | --- |
| `tenantId` | A ID do locatário da qual você deseja solicitar permissão. Sua ID de locatário pode ser formatada como um GUID ou como um nome amigável. **Observação**: a ID do locatário é chamada de &quot;ID do Diretório&quot; na interface [!DNL Microsoft Azure]. |
| `clientId` | A ID do aplicativo atribuída ao seu aplicativo. Você pode recuperar essa ID do portal do [!DNL Microsoft Entra ID] no qual você registrou o [!DNL Azure Active Directory]. |
| `clientSecretValue` | O segredo do cliente usado com a ID do cliente para autenticar seu aplicativo. Você pode recuperar o segredo do cliente no portal [!DNL Microsoft Entra ID] em que registrou o [!DNL Azure Active Directory]. |
| `namespace` | O namespace do [!DNL Event Hub] que você está acessando. Um namespace [!DNL Event Hub] fornece um contêiner de escopo exclusivo, no qual você pode criar um ou mais [!DNL Event Hubs]. |

Para obter mais informações sobre [!DNL Azure Active Directory], leia o [Guia do Azure sobre o uso da Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Autenticação do Azure Ative Diretory com Escopo do Hub de Eventos]

| Credencial | Descrição |
| --- | --- |
| `tenantId` | A ID do locatário da qual você deseja solicitar permissão. Sua ID de locatário pode ser formatada como um GUID ou como um nome amigável. **Observação**: a ID do locatário é chamada de &quot;ID do Diretório&quot; na interface [!DNL Microsoft Azure]. |
| `clientId` | A ID do aplicativo atribuída ao seu aplicativo. Você pode recuperar essa ID do portal do [!DNL Microsoft Entra ID] no qual você registrou o [!DNL Azure Active Directory]. |
| `clientSecretValue` | O segredo do cliente usado com a ID do cliente para autenticar seu aplicativo. Você pode recuperar o segredo do cliente no portal [!DNL Microsoft Entra ID] em que registrou o [!DNL Azure Active Directory]. |
| `namespace` | O namespace do [!DNL Event Hub] que você está acessando. Um namespace [!DNL Event Hub] fornece um contêiner de escopo exclusivo, no qual você pode criar um ou mais [!DNL Event Hubs]. |
| `eventHubName` | Preencha seu nome [!DNL Azure Event Hub]. Leia a [documentação do Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) para obter mais informações sobre os nomes de [!DNL Event Hub]. |

>[!ENDTABS]

Para obter mais informações sobre esses valores, consulte [este documento dos Hubs de Eventos](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

>[!TIP]
>
>Depois de criada, você não pode alterar o tipo de autenticação de uma conexão de base [!DNL Event Hubs]. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

A primeira etapa na criação de uma conexão de origem é autenticar sua origem [!DNL Event Hubs] e gerar uma ID de conexão base. Uma ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Event Hubs] como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticação padrão]

Para criar uma conta usando a autenticação padrão, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer valores para os seus `sasKeyName`, `sasKey` e `namespace`.

+++Solicitação

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
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Event Hubs] é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Autenticação SAS]

Para criar uma conta usando a autenticação SAS, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer valores para seus `sasKeyName`, `sasKey`,`namespace` e `eventHubName`.

+++Solicitação

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
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
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
| `params.eventHubName` | O nome da sua origem [!DNL Event Hubs]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Event Hubs] é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Autenticação do Ative Diretory do Azure Hub de Eventos]

Para criar uma conta usando a Autenticação do Azure Ative Diretory, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer valores para seus `tenantId`, `clientId`,`clientSecretValue` e `namespace`.

+++Solicitação

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
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
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
| `auth.params.tenantId` | A ID do locatário do seu aplicativo. **Observação**: a ID do locatário é chamada de &quot;ID do Diretório&quot; na interface [!DNL Microsoft Azure]. |
| `auth.params.clientId` | A ID do cliente da sua organização. |
| `auth.params.clientSecretValue` | O valor do segredo do cliente da sua organização. |
| `auth.params.namespace` | O namespace do [!DNL Event Hubs] que você está acessando. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Event Hubs] é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Autenticação do Azure Ative Diretory com Escopo do Hub de Eventos]

Para criar uma conta usando a Autenticação do Azure Ative Diretory, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer valores para seus `tenantId`, `clientId`,`clientSecretValue`, `namespace` e `eventHubName`.

+++Solicitação

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
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
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
| `auth.params.tenantId` | A ID do locatário do seu aplicativo. **Observação**: a ID do locatário é chamada de &quot;ID do Diretório&quot; na interface [!DNL Microsoft Azure]. |
| `auth.params.clientId` | A ID do cliente da sua organização. |
| `auth.params.clientSecretValue` | O valor do segredo do cliente da sua organização. |
| `auth.params.namespace` | O namespace do [!DNL Event Hubs] que você está acessando. |
| `auth.params.eventHubName` | O nome da sua origem [!DNL Event Hubs]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Event Hubs] é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## Criar uma conexão de origem

>[!TIP]
>
>Um grupo de consumidores [!DNL Event Hubs] só pode ser usado para um único fluxo em um determinado momento.

Uma conexão de origem cria e gerencia a conexão com a origem externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e uma ID de conexão de origem necessária para criar um fluxo de dados. Uma instância de conexão de origem é específica para um locatário e uma organização.

Para criar uma conexão de origem, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` da API [!DNL Flow Service].

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
          "eventHubName": "{EVENT_HUB_NAME}",
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
| `baseConnectionId` | A ID de conexão da origem [!DNL Event Hubs] que foi gerada na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL Event Hubs]. Esta ID é: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | O formato dos dados [!DNL Event Hubs] que você deseja assimilar. Atualmente, o único formato de dados com suporte é `json`. |
| `params.eventHubName` | O nome da sua origem [!DNL Event Hubs]. |
| `params.dataType` | Esse parâmetro define o tipo de dados que está sendo assimilado. Os tipos de dados suportados incluem: `raw` e `xdm`. |
| `params.reset` | Esse parâmetro define como os dados serão lidos. Use `latest` para começar a ler os dados mais recentes e use `earliest` para começar a ler os primeiros dados disponíveis no fluxo. Este parâmetro é opcional e o padrão é `earliest` se não for fornecido. |
| `params.consumerGroup` | O mecanismo de publicação ou assinatura a ser usado para [!DNL Event Hubs]. Este parâmetro é opcional e o padrão é `$Default` se não for fornecido. Consulte este [[!DNL Event Hubs] guia sobre consumidores de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) para obter mais informações. **Observação**: um grupo de consumidores [!DNL Event Hubs] só pode ser usado para um único fluxo em um determinado momento. |

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de origem [!DNL Event Hubs] usando a API [!DNL Flow Service]. Você pode usar esta ID de conexão de origem no próximo tutorial para [criar um fluxo de dados de streaming usando a [!DNL Flow Service] API](../../collect/streaming.md).
