---
title: Criar uma conexão Google PubSub-source usando a API do Serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a uma conta Google PubSub usando a API de Serviço de Fluxo.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# Crie um [!DNL Google PubSub] Conexão de origem usando a API de serviço de fluxo

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
| `topicId` | A ID da variável [!DNL PubSub] que representa um feed de mensagens. Você deve especificar uma ID de tópico se desejar fornecer acesso a um fluxo específico de dados no [!DNL Google PubSub] fonte. |
| `subscriptionId` | A ID do [!DNL PubSub] assinatura. Em [!DNL PubSub], as subscrições permitem receber mensagens, assinando o tópico no qual as mensagens foram publicadas. |
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

Durante essa etapa, é possível definir os dados aos quais sua conta tem acesso fornecendo uma ID de tópico. Somente as subscrições associadas à ID de tópico estarão acessíveis.

>[!NOTE]
>
>Os principais (funções) atribuídos a um projeto público são herdados em todos os tópicos e subscrições criados dentro de um [!DNL PubSub] projeto. Se você quiser adicionar um principal (função) para ter acesso a um tópico específico, esse principal (função) também deverá ser adicionado à assinatura correspondente do tópico. Para obter mais informações, leia a [[!DNL PubSub] documentação sobre o controle de acesso](https://cloud.google.com/pubsub/docs/access-control).

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Google PubSub authentication credentials",
          "params": {
              "projectId": "acme-project",
              "credentials": "{CREDENTIALS}",
              "topicId": "acmeProjectAPI",
              "subscriptionId": "acme-project-api-new"
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
| `auth.params.topicId` | A ID do tópico da sua [!DNL PubSub] fonte à qual você deseja fornecer acesso. |
| `auth.params.subscriptionId` | A ID da assinatura em relação ao seu [!DNL PubSub] tópico. |
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

Uma conexão de origem cria e gerencia a conexão com a fonte externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e uma ID de conexão de origem necessária para criar um fluxo de dados. Uma instância de conexão de origem é específica de um locatário e de uma organização.

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
          "topicId": "acme-project",
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
| `params.topicId` | O nome ou a ID do [!DNL PubSub] tópico. Em [!DNL PubSub], um tópico é um recurso nomeado que representa um feed de mensagens. |
| `params.subscriptionId` | A ID de assinatura que corresponde a um determinado tópico. Em [!DNL PubSub], as assinaturas permitem ler mensagens de um tópico. Uma ou várias subscrições podem ser atribuídas a um único tópico. |
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
