---
title: Criar uma conexão Google PubSub Source usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a uma conta Google PubSub usando a API do Serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 2%

---

# Criar uma Conexão do Source [!DNL Google PubSub] usando a API do Serviço de Fluxo

>[!IMPORTANT]
>
>A origem [!DNL Google PubSub] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Este tutorial guiará você pelas etapas para conectar o [!DNL Google PubSub] (a seguir denominado &quot;[!DNL PubSub]&quot;) ao Experience Platform, usando a [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL PubSub] ao Experience Platform usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Você deve fornecer valores para as propriedades de conexão descritas abaixo para conectar sua conta do [!DNL PubSub] ao [!DNL Flow Service]. Para obter mais informações sobre autenticação e configuração de pré-requisito, leia a [[!DNL PubSub source] visão geral](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB Autenticação baseada em projeto]

| Credencial | Descrição |
| --- | --- |
| `projectId` | A ID do projeto necessária para autenticar [!DNL PubSub]. |
| `credentials` | A credencial necessária para autenticar [!DNL PubSub]. Certifique-se de colocar o arquivo JSON completo após remover os espaços em branco de suas credenciais. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de origem e de destino de base. A ID da especificação de conexão [!DNL PubSub] é: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Autenticação baseada em assinatura e tópico]

| Credencial | Descrição |
| --- | --- |
| `credentials` | A credencial necessária para autenticar [!DNL PubSub]. Certifique-se de colocar o arquivo JSON completo após remover os espaços em branco de suas credenciais. |
| `topicName` | O nome do recurso que representa um feed de mensagens. Você deve especificar um nome de tópico se quiser fornecer acesso a um fluxo específico de dados em sua origem [!DNL PubSub]. O formato do nome do tópico é: `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | O nome da sua assinatura do [!DNL PubSub]. No [!DNL PubSub], as assinaturas permitem que você receba mensagens inscrevendo-se no tópico no qual as mensagens foram publicadas. **Observação**: uma única assinatura [!DNL PubSub] só pode ser usada para um fluxo de dados. Para fazer vários fluxos de dados, você deve ter várias assinaturas. O formato do nome da assinatura é: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de origem e de destino de base. A ID da especificação de conexão [!DNL PubSub] é: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

Para obter mais informações sobre esses valores, leia este documento de [[!DNL PubSub] autenticação](https://cloud.google.com/pubsub/docs/authentication). Para usar a autenticação baseada em conta de serviço, leia este [[!DNL PubSub] guia sobre criação de contas de serviço](https://cloud.google.com/docs/authentication/production#create_service_account) para obter etapas sobre como gerar suas credenciais.

>[!TIP]
>
>Se estiver usando autenticação baseada em conta de serviço, verifique se você concedeu acesso de usuário suficiente à conta de serviço e se não há espaços em branco adicionais no JSON ao copiar e colar suas credenciais.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

>[!TIP]
>
>Depois de criada, você não pode alterar o tipo de autenticação de uma conexão de base [!DNL Google PubSub]. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

A primeira etapa na criação de uma conexão de origem é autenticar sua origem [!DNL PubSub] e gerar uma ID de conexão base. Uma ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL PubSub] como parte dos parâmetros de solicitação.

A origem [!DNL PubSub] permite especificar o tipo de acesso que você deseja permitir durante a autenticação. Você pode configurar sua conta para ter acesso raiz ou restringir o acesso a um determinado tópico e assinatura do [!DNL PubSub].

>[!NOTE]
>
>As principais (funções) atribuídas a um projeto [!DNL PubSub] são herdadas em todos os tópicos e assinaturas criadas dentro de um projeto [!DNL PubSub]. Se você quiser que um principal (função) tenha acesso a um tópico específico, esse principal (função) também deverá ser adicionado à assinatura correspondente do tópico. Para obter mais informações, leia a [[!DNL PubSub] documentação sobre controle de acesso](<https://cloud.google.com/pubsub/docs/access-control>).

**Formato da API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticação baseada em projeto]

Para criar uma conexão base com autenticação baseada em projeto, faça uma solicitação POST para o ponto de extremidade `/connections` e forneça seus `projectId` e `credentials` no corpo da solicitação.

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
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
| `connectionSpec.id` | A ID de especificação de conexão [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

++++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão básica é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB Autenticação baseada em assinatura e tópico]

Para criar uma conexão base com autenticação baseada em assinatura e tópico, faça uma solicitação POST para o ponto de extremidade `/connections` e forneça seus `credentials`, `topicName` e `subscriptionName` no corpo da solicitação.

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
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
| `auth.params.credentials` | A credencial ou chave necessária para autenticar [!DNL PubSub]. |
| `auth.params.topicName` | O par de ID de projeto e ID de tópico para a origem [!DNL PubSub] à qual você deseja fornecer acesso. |
| `auth.params.subscriptionName` | O par da ID do projeto e da ID da assinatura para a origem [!DNL PubSub] à qual você deseja fornecer acesso. |
| `connectionSpec.id` | A ID de especificação de conexão [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

+++

+++Resposta

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão básica é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## Criar uma conexão de origem {#source}

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
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser fornecido para incluir mais informações sobre a conexão de origem. |
| `baseConnectionId` | A ID da conexão base da sua origem [!DNL PubSub] que foi gerada na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL PubSub]. Esta ID é: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | O formato dos dados [!DNL PubSub] que você deseja assimilar. Atualmente, o único formato de dados com suporte é `json`. |
| `params.topicName` | O nome do tópico [!DNL PubSub]. Em [!DNL PubSub], um tópico é um recurso nomeado que representa um feed de mensagens. |
| `params.subscriptionName` | O nome da assinatura que corresponde a um determinado tópico. No [!DNL PubSub], as assinaturas permitem que você leia mensagens de um tópico. Uma ou várias assinaturas podem ser atribuídas a um único tópico. |
| `params.dataType` | Esse parâmetro define o tipo de dados que está sendo assimilado. Os tipos de dados suportados incluem: `raw` e `xdm`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária no próximo tutorial para criar um fluxo de dados.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de origem [!DNL PubSub] usando a API [!DNL Flow Service]. Você pode usar esta ID de conexão de origem no próximo tutorial para [criar um fluxo de dados de streaming usando a [!DNL Flow Service] API](../../collect/streaming.md).
