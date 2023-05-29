---
keywords: Experience Platform;página inicial;tópicos populares;REST genérico;rest genérico
solution: Experience Platform
title: Criar uma conexão básica de API REST genérica usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar a REST API genérica ao Adobe Experience Platform usando a API do serviço de fluxo.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# Crie uma conexão básica de REST genérica usando o [!DNL Flow Service] API

>[!NOTE]
>
>A variável [!DNL Generic REST API] a fonte está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Generic REST API] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com [!DNL Generic REST API], você deve fornecer credenciais válidas para o tipo de autenticação de sua escolha. [!DNL Generic REST API] O oferece suporte ao código de atualização OAuth 2 e à autenticação básica. Consulte as tabelas a seguir para obter informações sobre as credenciais dos dois tipos de autenticação compatíveis.

#### Código de atualização do OAuth 2

| Credencial | Descrição |
| --- | --- |
| `host` | O URL do host da origem para a qual você está fazendo sua solicitação. Este valor é obrigatório e não pode ser ignorado usando `requestParameterOverride`. |
| `authorizationTestUrl` | (Opcional) O URL de teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não forem fornecidas, as credenciais serão automaticamente verificadas durante a etapa de criação da conexão de origem. |
| `clientId` | (Opcional) A ID do cliente associada à sua conta de usuário. |
| `clientSecret` | (Opcional) O segredo do cliente associado à sua conta de usuário. |
| `accessToken` | A credencial de autenticação primária usada para acessar seu aplicativo. O token de acesso representa a autorização do aplicativo para acessar aspectos específicos dos dados de um usuário. Este valor é obrigatório e não pode ser ignorado usando `requestParameterOverride`. |
| `refreshToken` | (Opcional) Um token usado para gerar um novo token de acesso, quando o token de acesso expirou. |
| `expirationDate` | (Opcional) Um valor oculto que define a data de expiração do token de acesso. |
| `accessTokenUrl` | (Opcional) O endpoint do URL usado para buscar seu token de acesso. |
| `requestParameterOverride` | (Opcional) Uma propriedade que permite especificar quais parâmetros de credencial serão substituídos. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Generic REST API] é: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Autenticação básica

| Credencial | Descrição |
| --- | --- |
| `host` | O URL do host da origem para a qual você está fazendo sua solicitação. |
| `username` | O nome de usuário que corresponde à sua conta de usuário. |
| `password` | A senha que corresponde à sua conta de usuário. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Generic REST API] é: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

[!DNL Generic REST API] O oferece suporte à autenticação básica e ao código de atualização do OAuth 2. Consulte os exemplos a seguir para obter orientação sobre como realizar a autenticação com qualquer um dos tipos de autenticação.

### Criar um [!DNL Generic REST API] conexão básica usando o código de atualização OAuth 2

Para criar uma ID de conexão base usando o código de atualização OAuth 2, faça uma solicitação POST para o `/connections` ao fornecer suas credenciais do OAuth 2.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `name` | O nome da sua conexão básica. Certifique-se de que o nome da sua conexão básica seja descritivo, pois você pode usá-lo para pesquisar informações sobre a sua conexão básica. |
| `description` | (Opcional) Uma propriedade que você pode incluir para fornecer mais informações sobre sua conexão básica. |
| `connectionSpec.id` | A ID de especificação de conexão associada a [!DNL Generic REST API]. Essa ID fixa é: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | O tipo de autenticação que você está usando para autenticar sua origem na Platform. |
| `auth.params.host` | O URL raiz usado para se conectar ao [!DNL Generic REST API] origem. |
| `auth.params.accessToken` | O token de acesso correspondente usado para autenticar sua origem. Isso é necessário para a autenticação baseada em OAuth. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Criar um [!DNL Generic REST API] conexão básica usando autenticação básica

Para criar um [!DNL Generic REST API] conexão básica usando autenticação básica, faça uma solicitação POST ao `/connections` endpoint de [!DNL Flow Service] ao fornecer suas credenciais básicas de autenticação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão básica para [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão básica. Certifique-se de que o nome da sua conexão básica seja descritivo, pois você pode usá-lo para pesquisar informações sobre a sua conexão básica. |
| `description` | (Opcional) Uma propriedade que você pode incluir para fornecer mais informações sobre sua conexão básica. |
| `connectionSpec.id` | A ID de especificação de conexão associada a [!DNL Generic REST API]. Essa ID fixa é: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | O tipo de autenticação que você está usando para conectar sua origem à Platform. |
| `auth.params.host` | O URL raiz usado para se conectar ao [!DNL Generic REST API] origem. |
| `auth.params.username` | O nome de usuário que corresponde ao seu [!DNL Generic REST API] origem. Isso é necessário para a autenticação básica. |
| `auth.params.password` | A senha que corresponde ao seu [!DNL Generic REST API] origem. Isso é necessário para a autenticação básica. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar a estrutura de arquivos e o conteúdo da fonte na próxima etapa.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Generic REST API] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de protocolos para a Platform usando o [!DNL Flow Service] API](../../collect/protocols.md)
