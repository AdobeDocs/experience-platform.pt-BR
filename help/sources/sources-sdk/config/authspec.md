---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
title: Configurar especificações de autenticação para fontes de autoatendimento (SDK em lote)
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Origens de Autoatendimento (SDK em Lote).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# Configurar especificações de autenticação para fontes de autoatendimento (SDK em lote)

As especificações de autenticação definem como os usuários do Adobe Experience Platform podem se conectar à origem.

A matriz `authSpec` contém informações sobre os parâmetros de autenticação necessários para conectar uma origem à Experience Platform. Qualquer origem fornecida pode suportar vários tipos diferentes de autenticação.

## Especificações de autenticação

As Fontes de autoatendimento (SDK em lote) são compatíveis com códigos de atualização OAuth 2 e autenticação básica. Consulte as tabelas abaixo para obter orientação sobre como usar um código de atualização OAuth 2 e uma autenticação básica

### Código de atualização do OAuth 2

Um código de atualização OAuth 2 permite acesso seguro a um aplicativo gerando um token de acesso temporário e um token de atualização. O token de acesso permite acessar com segurança os recursos sem precisar fornecer outras credenciais, enquanto o token de atualização permite gerar um novo token de acesso depois que ele expirar.

+++Exibir exemplo de um código de atualização OAuth 2

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `authSpec.name` | Exibe o nome do tipo de autenticação suportado. | `oAuth2-refresh-code` |
| `authSpec.type` | Define o tipo de autenticação aceito pela origem. | `oAuth2-refresh-code` |
| `authSpec.spec` | Contém informações sobre o esquema, o tipo de dados e as propriedades da autenticação. |  |
| `authSpec.spec.$schema` | Define o esquema usado para a autenticação. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Define o tipo de dados do esquema. | `object` |
| `authSpec.spec.properties` | Contém informações sobre as credenciais usadas para a autenticação. |  |
| `authSpec.spec.properties.description` | Exibe uma breve descrição da credencial. |  |
| `authSpec.spec.properties.type` | Define o tipo de dados da credencial. | `string` |
| `authSpec.spec.properties.clientId` | A ID do cliente associada ao aplicativo. A ID do cliente é usada juntamente com o segredo do cliente para recuperar o token de acesso. |  |
| `authSpec.spec.properties.clientSecret` | O segredo do cliente associado ao aplicativo. O segredo do cliente é usado em conjunto com a ID do cliente para recuperar o token de acesso. |  |
| `authSpec.spec.properties.accessToken` | O token de acesso autoriza o acesso seguro ao aplicativo. |  |
| `authSpec.spec.properties.refreshToken` | O token de atualização é usado para gerar um novo token de acesso, quando o token de acesso expira. |  |
| `authSpec.spec.properties.expirationDate` | Define a data de expiração do token de acesso. |  |
| `authSpec.spec.properties.refreshTokenUrl` | O URL usado para recuperar o token de atualização. |  |
| `authSpec.spec.properties.accessTokenUrl` | O URL usado para recuperar o token de atualização. |  |
| `authSpec.spec.properties.requestParameterOverride` | Permite que você especifique parâmetros de credencial a serem substituídos na autenticação. |  |
| `authSpec.spec.required` | Exibe as credenciais necessárias para a autenticação. | `accessToken` |

{style="table-layout:auto"}

+++

### Autenticação básica

A autenticação básica é um tipo de autenticação que permite acessar seu aplicativo usando uma combinação do nome de usuário da conta e da senha da conta.

+++ Ver exemplo de autenticação básica

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `authSpec.name` | Exibe o nome do tipo de autenticação suportado. | `Basic Authentication` |
| `authSpec.type` | Define o tipo de autenticação aceito pela origem. | `BasicAuthentication` |
| `authSpec.spec` | Contém informações sobre o esquema, o tipo de dados e as propriedades da autenticação. |  |
| `authSpec.spec.$schema` | Define o esquema usado para a autenticação. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Define o tipo de dados do esquema. | `object` |
| `authSpec.spec.description` | Exibe mais informações específicas para o seu tipo de autenticação. |  |
| `authSpec.spec.properties` | Contém informações sobre as credenciais usadas para a autenticação. |  |
| `authSpec.spec.properties.username` | O nome de usuário da conta associado ao aplicativo. |  |
| `authSpec.spec.properties.password` | A senha da conta associada ao aplicativo. |  |
| `authSpec.spec.required` | Especifica os campos obrigatórios a serem inseridos no Experience Platform. | `username` |

{style="table-layout:auto"}

+++

### Autenticação da chave de API {#api-key-authentication}

A autenticação da chave de API é um método seguro para acessar APIs, fornecendo uma chave de API e outros parâmetros de autenticação relevantes em solicitações. Dependendo das suas informações de API específicas, você pode enviar a chave de API como parte do cabeçalho da solicitação, dos parâmetros de consulta ou do corpo.

Normalmente, os seguintes parâmetros são necessários ao usar a autenticação de chave de API:

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `host` | sequência de caracteres | Não | O URL do recurso. |
| `authKey1` | sequência de caracteres | Sim | A primeira chave de autenticação necessária para acessar a API. Normalmente, é enviado no cabeçalho da solicitação ou nos parâmetros de consulta. |
| `authKey2` | sequência de caracteres | Opcional | Uma segunda chave de autenticação. Se necessário, essa chave é usada com frequência para validar ainda mais as solicitações. |
| `authKeyN` | sequência de caracteres | Opcional | Uma variável de autenticação adicional que pode ser usada conforme necessário, exceto a API. |

{style="table-layout:auto"}

+++Exibir autenticação de chave de API

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### Comportamento de autenticação

Você pode usar o parâmetro `restAttributes` para definir como a chave de API deve ser incluída na solicitação. Por exemplo, no exemplo abaixo, o atributo `headerParamName` indica que `X-Auth-Key1` deve ser enviado como um cabeçalho.

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

Cada chave de autenticação (como `authKey1`, `authKey2`, etc.) pode ser associada a `restAttributes` para determinar como elas são enviadas como solicitações.

Se `authKey1` tiver `"headerParamName": "X-Auth-Key1"`. Isso significa que o cabeçalho da solicitação deve incluir `X-Auth-Key:{YOUR_AUTH_KEY1}`. Além disso, o nome da chave e `headerParamName` não precisam ser necessariamente os mesmos. Por exemplo:

* O `authKey1` pode ter `headerParamName: X-Custom-Auth-Key`. Isso significa que o cabeçalho da solicitação usará `X-Custom-Auth-Key` em vez de `authKey1`.
* Por outro lado, `authKey1` pode ter `headerParamName: authKey1`. Isso significa que o nome do cabeçalho da solicitação permanece inalterado.

**Exemplo de formato de API**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## Exemplo de especificação de autenticação

Este é um exemplo de uma especificação de autenticação concluída usando uma origem [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md).

+++Ver exemplo de especificação de autenticação

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

+++

## Próximas etapas

Com suas especificações de autenticação preenchidas, você pode continuar a configurar as especificações de origem para a origem que deseja integrar ao Experience Platform. Consulte o documento sobre [configuração de especificações de origem](./sourcespec.md) para obter mais informações.
