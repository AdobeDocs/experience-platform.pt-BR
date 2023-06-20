---
title: Criar uma conexão de origem Google PubSub usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a uma conta Google PubSub usando a API do Serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 1%

---

# Criar um [!DNL Google PubSub] Conexão de origem usando a API de serviço de fluxo

>[!IMPORTANT]
>
>A variável [!DNL Google PubSub] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial guiará você pelas etapas para se conectar [!DNL Google PubSub] (a seguir designado por &quot;[!DNL PubSub]&quot;) para Experience Platform, usando o [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL PubSub] para a Platform usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar a [!DNL PubSub], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `projectId` | A ID do projeto necessária para a autenticação [!DNL PubSub]. |
| `credentials` | A credencial ou chave necessária para autenticar [!DNL PubSub]. |
| `topicName` | O nome do recurso que representa um feed de mensagens. Você deve especificar um nome de tópico se quiser fornecer acesso a um fluxo específico de dados em seu [!DNL PubSub] origem. O formato do nome do tópico é: `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | O nome do seu [!DNL PubSub] assinatura. Entrada [!DNL PubSub], assinaturas permitem que você receba mensagens inscrevendo-se no tópico no qual as mensagens foram publicadas. **Nota**: Uma única [!DNL PubSub] a assinatura só pode ser usada para um fluxo de dados. Para fazer vários fluxos de dados, você deve ter várias assinaturas. O formato do nome da assinatura é: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de origem e de destino de base. A variável [!DNL PubSub] A ID da especificação de conexão é: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Para obter mais informações sobre esses valores, consulte esta [[!DNL PubSub] autenticação](https://cloud.google.com/pubsub/docs/authentication) documento. Para usar autenticação baseada em conta de serviço, consulte esta [[!DNL PubSub] guia sobre a criação de contas de serviço](https://cloud.google.com/docs/authentication/production#create_service_account) para obter etapas sobre como gerar suas credenciais.

>[!TIP]
>
>Se estiver usando autenticação baseada em conta de serviço, verifique se você concedeu acesso de usuário suficiente à conta de serviço e se não há espaços em branco adicionais no JSON ao copiar e colar suas credenciais.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

A primeira etapa na criação de uma conexão de origem é autenticar seu [!DNL PubSub] origem e gere uma ID de conexão básica. Uma ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL PubSub] credenciais de autenticação como parte dos parâmetros de solicitação.

A variável [!DNL PubSub] source permite especificar o tipo de acesso que você deseja permitir durante a autenticação. Você pode configurar sua conta para ter acesso de raiz ou restringir o acesso a um específico [!DNL PubSub] tópico e assinatura.

>[!NOTE]
>
>Principal (funções) atribuído a um [!DNL PubSub] projetos são herdados em todos os tópicos e assinaturas criadas dentro de um [!DNL PubSub] projeto. Se você quiser que um principal (função) tenha acesso a um tópico específico, esse principal (função) também deverá ser adicionado à assinatura correspondente do tópico. Para obter mais informações, leia a [[!DNL PubSub] documentação sobre o controle de acesso](<https://cloud.google.com/pubsub/docs/access-control>).

**Formato da API**

```http
POST /connections
```

**Solicitação**

>[!BEGINTABS]

>[!TAB Autenticação baseada em projeto]

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
| `auth.params.projectId` | A ID do projeto necessária para a autenticação [!DNL PubSub]. |
| `auth.params.credentials` | A credencial ou chave necessária para autenticar [!DNL PubSub]. |
| `connectionSpec.id` | A variável [!DNL PubSub] ID de especificação da conexão: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Tópico e autenticação por assinatura]

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
| `auth.params.topicName` | O par de ID de projeto e ID de tópico para o [!DNL PubSub] fonte à qual você deseja fornecer acesso. |
| `auth.params.subscriptionName` | O par da ID do projeto e da ID de assinatura para o [!DNL PubSub] fonte à qual você deseja fornecer acesso. |
| `connectionSpec.id` | A variável [!DNL PubSub] ID de especificação da conexão: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID de conexão básica é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Criar uma conexão de origem {#source}

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
| `baseConnectionId` | A ID de conexão básica de seu [!DNL PubSub] que foi gerado na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL PubSub]. Essa ID é: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | O formato do [!DNL PubSub] dados que você deseja assimilar. No momento, o único formato de dados compatível é `json`. |
| `params.topicName` | O nome do seu [!DNL PubSub] tópico. Entrada [!DNL PubSub], um tópico é um recurso nomeado que representa um feed de mensagens. |
| `params.subscriptionName` | O nome da assinatura que corresponde a um determinado tópico. Entrada [!DNL PubSub], assinaturas permitem ler mensagens de um tópico. Uma ou várias assinaturas podem ser atribuídas a um único tópico. |
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
