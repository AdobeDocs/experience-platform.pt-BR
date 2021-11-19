---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Configurar especificações de autenticação para o SDK do SDK do SDK do SDK do Sources
topic-legacy: overview
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar o SDK das Fontes.
hide: true
hidefromtoc: true
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: a3bfd3b87343ca1dd2d122f4f82926082965578c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 2%

---

# Configurar especificações de autenticação para o SDK do SDK do SDK do SDK do Sources

As especificações de autenticação definem como os usuários do Adobe Experience Platform podem se conectar à sua fonte.

O `authSpec` A matriz contém informações sobre os parâmetros de autenticação necessários para conectar uma fonte à Platform. Qualquer origem pode suportar vários tipos diferentes de autenticação.

## Especificações de autenticação

Atualmente, [!DNL Sources SDK] O suporta códigos de atualização OAuth 2 e autenticação básica. Consulte as tabelas abaixo para obter orientação sobre o uso de um código de atualização OAuth 2 e autenticação básica

### Código de atualização do OAuth 2

Um código de atualização OAuth 2 permite acesso seguro a um aplicativo gerando um token de acesso temporário e um token de atualização. O token de acesso permite acessar com segurança seus recursos sem precisar fornecer outras credenciais, enquanto o token de atualização permite gerar um novo token de acesso, uma vez que o token de acesso expire.

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource url host path."
      },
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
      "host",
      "accessToken"
    ]
  }
}
```

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `authSpec.name` | Exibe o nome do tipo de autenticação suportado. | `oAuth2-refresh-code` |
| `authSpec.type` | Define o tipo de autenticação suportado pela origem. | `oAuth2-refresh-code` |
| `authSpec.spec` | Contém informações sobre o esquema da autenticação, o tipo de dados e as propriedades. |
| `authSpec.spec.$schema` | Define o schema usado para a autenticação. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Define o tipo de dados do esquema. | `object` |
| `authSpec.spec.properties` | Contém informações sobre as credenciais usadas para a autenticação. |
| `authSpec.spec.properties.description` | Exibe uma breve descrição da credencial. |
| `authSpec.spec.properties.type` | Define o tipo de dados da credencial. | `string` |
| `authSpec.spec.properties.clientId` | A ID do cliente associada ao aplicativo. A ID do cliente é usada juntamente com o segredo do cliente para recuperar o token de acesso. |
| `authSpec.spec.properties.clientSecret` | O segredo do cliente associado ao seu aplicativo. O segredo do cliente é usado junto com a ID do cliente para recuperar o token de acesso. |
| `authSpec.spec.properties.accessToken` | O token de acesso autoriza o acesso seguro ao aplicativo. |
| `authSpec.spec.properties.refreshToken` | O token de atualização é usado para gerar um novo token de acesso, quando o token de acesso expira. |
| `authSpec.spec.properties.expirationDate` | Define a data de expiração do token de acesso. |
| `authSpec.spec.properties.refreshTokenUrl` | O URL usado para recuperar o token de atualização. |
| `authSpec.spec.properties.accessTokenUrl` | O URL usado para recuperar o token de atualização. |
| `authSpec.spec.properties.requestParameterOverride` | Permite que você especifique parâmetros de credencial a serem substituídos na autenticação. |
| `authSpec.spec.required` | Exibe as credenciais necessárias para a autenticação. | `accessToken` |

{style=&quot;table-layout:auto&quot;}


### Autenticação básica

Autenticação básica é um tipo de autenticação que permite acessar seu aplicativo usando uma combinação do URL de host do aplicativo, do nome de usuário da conta e da senha da conta.

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource url host path"
      },
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
      "host",
      "username",
      "password"
    ]
  }
}
```

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `authSpec.name` | Exibe o nome do tipo de autenticação suportado. | `Basic Authentication` |
| `authSpec.type` | Define o tipo de autenticação suportado pela origem. | `BasicAuthentication` |
| `authSpec.spec` | Contém informações sobre o esquema da autenticação, o tipo de dados e as propriedades. |
| `authSpec.spec.$schema` | Define o schema usado para a autenticação. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Define o tipo de dados do esquema. | `object` |
| `authSpec.spec.description` | Exibe mais informações específicas para o tipo de autenticação. |
| `authSpec.spec.properties` | Contém informações sobre as credenciais usadas para a autenticação. |
| `authSpec.spec.properties.host` | O URL de host do seu aplicativo. |
| `authSpec.spec.properties.username` | O nome de usuário da conta associado ao seu aplicativo. |
| `authSpec.spec.properties.password` | A senha da conta associada ao seu aplicativo. |
| `authSpec.spec.required` | Especifica os campos obrigatórios como valores obrigatórios a serem inseridos na Plataforma. | `host` |

{style=&quot;table-layout:auto&quot;}

## Exemplo de especificação de autenticação

Este é um exemplo de uma especificação de autenticação concluída usando um [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) fonte.

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
          "host": {
            "type": "string",
            "description": "Enter resource url host path"
          },
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
          "host",
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
          "host": {
            "type": "string",
            "description": "Enter resource url host path."
          },
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
          "host",
          "username",
          "password"
        ]
      }
    }
  ],
```

## Próximas etapas

Com suas especificações de autenticação preenchidas, você pode continuar a configurar as especificações de origem para a origem que deseja integrar à Platform. Veja o documento em [configuração de especificações de origem](./sourcespec.md) para obter mais informações.
