---
keywords: Experience Platform, home, tópicos populares, REST genérico, repouso genérico
solution: Experience Platform
title: Criar uma conexão básica da API REST genérica usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar a API REST genérica ao Adobe Experience Platform usando a API do Serviço de fluxo.
source-git-commit: 1a9c4d5ba3ba9201378e78c0e92dea5101668a24
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 1%

---

# Crie uma conexão básica da API REST genérica usando o [!DNL Flow Service] API

>[!NOTE]
>
>O [!DNL Generic REST API] A fonte está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Generic REST API] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Generic REST API], você deve fornecer credenciais válidas para o tipo de autenticação de sua escolha. [!DNL Generic REST API] O suporta o código de atualização OAuth 2 e a autenticação básica. Consulte as tabelas a seguir para obter informações sobre as credenciais dos dois tipos de autenticação compatíveis.

#### Código de atualização do OAuth 2

| Credencial | Descrição |
| --- | --- |
| `host` | O URL do host da fonte para a qual você está fazendo sua solicitação. Este valor é necessário e não pode ser ignorado usando `requestParameterOverride`. |
| `authorizationTestUrl` | (Opcional) O URL do teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não for fornecido, as credenciais serão verificadas automaticamente durante a etapa de criação da conexão de origem. |
| `clientId` | (Opcional) A ID do cliente associada à sua conta de usuário. |
| `clientSecret` | (Opcional) O segredo do cliente associado à sua conta de usuário. |
| `accessToken` | A credencial de autenticação primária usada para acessar seu aplicativo. O token de acesso representa a autorização de seu aplicativo, para acessar aspectos específicos dos dados de um usuário. Este valor é necessário e não pode ser ignorado usando `requestParameterOverride`. |
| `refreshToken` | (Opcional) Um token usado para gerar um novo token de acesso, quando o token de acesso tiver expirado. |
| `expirationDate` | (Opcional) Um valor oculto que define a data de expiração do seu token de acesso. |
| `accessTokenUrl` | (Opcional) O endpoint do URL usado para buscar seu token de acesso. |
| `requestParameterOverride` | (Opcional) Uma propriedade que permite especificar quais parâmetros de credenciais serão substituídos. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Generic REST API] é: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Autenticação básica

| Credencial | Descrição |
| --- | --- |
| `host` | O URL do host da fonte para a qual você está fazendo sua solicitação. |
| `username` | O nome de usuário que corresponde à sua conta de usuário. |
| `password` | A senha que corresponde à sua conta de usuário. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Generic REST API] é: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

[!DNL Generic REST API] O suporta autenticação básica e código de atualização OAuth 2. Consulte os exemplos a seguir para obter orientação sobre como autenticar com qualquer um dos tipos de autenticação.

### Crie um [!DNL Generic REST API] conexão base usando o código de atualização OAuth 2

Para criar uma ID de conexão base usando o código de atualização do OAuth 2, faça uma solicitação de POST para a variável `/connections` endpoint ao fornecer suas credenciais do OAuth 2.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | O nome da sua conexão básica. Certifique-se de que o nome da sua conexão base seja descritivo, pois você pode usá-lo para pesquisar informações sobre a sua conexão base. |
| `description` | (Opcional) Uma propriedade que pode ser incluída para fornecer mais informações sobre a conexão básica. |
| `connectionSpec.id` | A ID de especificação de conexão associada ao [!DNL Generic REST API]. Essa ID fixa é: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | O tipo de autenticação que você está usando para autenticar sua origem na Plataforma. |
| `auth.params.host` | O URL raiz usado para se conectar ao seu [!DNL Generic REST API] fonte. |
| `auth.params.accessToken` | O token de acesso correspondente usado para autenticar sua fonte. Isso é necessário para a autenticação baseada em OAuth. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Crie um [!DNL Generic REST API] conexão básica usando autenticação básica

Para criar um [!DNL Generic REST API] conexão básica usando autenticação básica, faça uma solicitação de POST para `/connections` ponto final de [!DNL Flow Service] API ao fornecer suas credenciais básicas de autenticação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | O nome da sua conexão básica. Certifique-se de que o nome da sua conexão base seja descritivo, pois você pode usá-lo para pesquisar informações sobre a sua conexão base. |
| `description` | (Opcional) Uma propriedade que pode ser incluída para fornecer mais informações sobre a conexão básica. |
| `connectionSpec.id` | A ID de especificação de conexão associada ao [!DNL Generic REST API]. Essa ID fixa é: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | O tipo de autenticação que você está usando para conectar sua fonte à Platform. |
| `auth.params.host` | O URL raiz usado para se conectar ao seu [!DNL Generic REST API] fonte. |
| `auth.params.username` | O nome de usuário que corresponde a sua [!DNL Generic REST API] fonte. Isso é necessário para a autenticação básica. |
| `auth.params.password` | A senha que corresponde ao seu [!DNL Generic REST API] fonte. Isso é necessário para a autenticação básica. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão base recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar a estrutura e o conteúdo do arquivo da sua origem na próxima etapa.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Generic REST API] conexão usando o [!DNL Flow Service] API e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a usar [explore aplicativos de protocolos usando a API do Serviço de Fluxo](../../explore/protocols.md).
