---
description: Esta página descreve os vários fluxos de autorização OAuth 2 compatíveis com o Destination SDK e fornece instruções para configurar a autorização OAuth 2 para o seu destino.
title: Autorização OAuth 2
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 0cde918c693d06d735397aad721fd3cd5c4e760e
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 2%

---


# Autorização OAuth 2

O Destination SDK oferece suporte a vários métodos de autorização para o seu destino. Entre eles está a opção para autenticar em seu destino usando a [estrutura de autorização OAuth 2](https://tools.ietf.org/html/rfc6749).

Esta página descreve os vários fluxos de autorização OAuth 2 compatíveis com o Destination SDK e fornece instruções para configurar a autorização OAuth 2 para o seu destino.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Não |

## Como adicionar detalhes de autorização do OAuth 2 à configuração de destino {#how-to-setup}

### Pré-requisitos em seu sistema {#prerequisites}

Como primeira etapa, você deve criar um aplicativo no sistema para o Adobe Experience Platform ou registrar o Experience Platform no sistema. O objetivo é gerar uma ID do cliente e um segredo do cliente, que são necessários para autenticar o Experience Platform no seu destino.

Como parte dessa configuração no seu sistema, você precisa dos URLs de redirecionamento/retorno de chamada OAuth 2 do Adobe Experience Platform, que podem ser obtidos na lista abaixo.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-can2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-gbr9.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>A etapa para registrar uma URL de redirecionamento/retorno de chamada para o Adobe Experience Platform em seu sistema é necessária somente para o tipo de concessão [OAuth 2 com Código de Autorização](#authorization-code). Para os outros dois tipos de concessão suportados (senha e credenciais do cliente), você pode ignorar esta etapa.

No final desta etapa, você deve ter:

* Uma ID de cliente;
* Um segredo de cliente;
* URL de retorno de chamada da Adobe (para a concessão de código de autorização).

### O que é necessário fazer no Destination SDK {#to-do-in-destination-sdk}

Para configurar a autorização OAuth 2 para o seu destino no Experience Platform, adicione os detalhes do OAuth 2 à [configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md), no parâmetro `customerAuthenticationConfigurations`. Consulte [autenticação do cliente](../../functionality/destination-configuration/customer-authentication.md) para obter exemplos detalhados. Instruções específicas sobre quais campos você precisa adicionar ao seu modelo de configuração, dependendo do tipo de concessão de autorização OAuth 2, estão mais abaixo nesta página.

## Tipos de concessão OAuth 2 compatíveis {#oauth2-grant-types}

A Experience Platform aceita os três tipos de concessão do OAuth 2 na tabela abaixo. Se você tiver uma configuração OAuth 2 personalizada, o Adobe poderá oferecer suporte a ela com a ajuda de campos personalizados na integração. Consulte as seções para cada tipo de concessão para obter mais informações.

>[!IMPORTANT]
>
>* Você fornece os parâmetros de entrada conforme instruído nas seções abaixo. Os sistemas internos da Adobe se conectam ao sistema de autorização da sua plataforma e capturam parâmetros de saída, que são usados para autenticar o usuário e manter a autorização no seu destino.
>* Os parâmetros de entrada destacados em negrito na tabela são parâmetros obrigatórios no fluxo de autorização do OAuth 2. Os outros parâmetros são opcionais. Há outros parâmetros de entrada personalizados que não são mostrados aqui, mas que estão descritos detalhadamente nas seções [Personalizar a configuração do OAuth 2](#customize-configuration) e [Atualizar o token de acesso](#access-token-refresh).

| Concessão do OAuth 2 | Entradas | Saídas |
|---------|----------|---------|
| Código de autorização | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Senha | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>senha</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Credencial do cliente | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

A tabela acima lista os campos usados em fluxos OAuth 2 padrão. Além desses campos padrão, várias integrações de parceiros podem exigir entradas e saídas adicionais. A Adobe projetou uma estrutura de autorização OAuth 2 flexível para o Destination SDK que pode lidar com variações no padrão de campos padrão acima, enquanto oferece suporte a um mecanismo para regenerar automaticamente saídas inválidas, como tokens de acesso expirados.

A saída em todos os casos inclui um token de acesso, que é usado pelo Experience Platform para autenticar e manter a autorização no seu destino.

O sistema que a Adobe projetou para autorização OAuth 2:

* Suporta todas as três concessões OAuth 2 enquanto contabiliza quaisquer variações entre elas, como campos de dados adicionais, chamadas de API não padrão e muito mais.
* Suporta tokens de acesso com valores de tempo de vida variáveis. A Adobe recomenda que você defina o valor do tempo de vida do token para um mínimo de 24 horas.
* Oferece suporte a fluxos de autorização OAuth 2 com ou sem tokens de atualização.

## OAuth 2 com código de autorização {#authorization-code}

Se o seu destino suportar um fluxo de código de autorização OAuth 2.0 padrão (leia as [especificações de padrões RFC](https://tools.ietf.org/html/rfc6749#section-4.1)) ou uma variação dele, consulte os campos obrigatórios e opcionais abaixo:

| Concessão do OAuth 2 | Entradas | Saídas |
|---------|----------|---------|
| Código de autorização | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Para definir esse método de autorização para o seu destino, adicione as seguintes linhas à sua configuração quando você [criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authType` | String | Use &quot;OAUTH2&quot;. |
| `grant` | String | Use &quot;OAUTH2_AUTHORIZATION_CODE&quot;. |
| `accessTokenUrl` | String | A URL ao seu lado, que emite tokens de acesso e, opcionalmente, atualiza tokens. |
| `authorizationUrl` | String | O URL do servidor de autorização, para o qual você redireciona o usuário para fazer logon no aplicativo. |
| `refreshTokenUrl` | String | *Opcional.* A URL no seu lado, que emite tokens de atualização. Frequentemente, `refreshTokenUrl` é o mesmo que `accessTokenUrl`. |
| `clientId` | String | A ID do cliente que seu sistema atribui à Adobe Experience Platform. |
| `clientSecret` | String | O segredo do cliente que seu sistema atribui à Adobe Experience Platform. |
| `scope` | Lista de strings | *Opcional*. Defina o escopo do que o token de acesso permite que o Experience Platform execute em seus recursos. Exemplo: &quot;ler, gravar&quot;. |

{style="table-layout:auto"}

## OAuth 2 com concessão de senha

Para a concessão de Senha do OAuth 2 (leia as [especificações de padrões RFC](https://tools.ietf.org/html/rfc6749#section-4.3)), o Experience Platform exige o nome de usuário e a senha do usuário. No fluxo de autorização, o Experience Platform troca essas credenciais por um token de acesso e, opcionalmente, um token de atualização.
O Adobe usa as entradas padrão abaixo para simplificar a configuração de destino, com a capacidade de substituir valores:

| Concessão do OAuth 2 | Entradas | Saídas |
|---------|----------|---------|
| Senha | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>senha</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> Você não precisa adicionar nenhum parâmetro para `username` e `password` na configuração abaixo. Quando você adicionar `"grant": "OAUTH2_PASSWORD"` na configuração de destino, o sistema solicitará que o usuário forneça um nome de usuário e senha na interface do usuário do Experience Platform quando ele se autenticar no seu destino.

Para definir esse método de autorização para o seu destino, adicione as seguintes linhas à sua configuração quando você [criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authType` | String | Use &quot;OAUTH2&quot;. |
| `grant` | String | Use &quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | String | A URL ao seu lado, que emite tokens de acesso e, opcionalmente, atualiza tokens. |
| `clientId` | String | A ID do cliente que seu sistema atribui à Adobe Experience Platform. |
| `clientSecret` | String | O segredo do cliente que seu sistema atribui à Adobe Experience Platform. |
| `scope` | Lista de strings | *Opcional*. Defina o escopo do que o token de acesso permite que o Experience Platform execute em seus recursos. Exemplo: &quot;ler, gravar&quot;. |

{style="table-layout:auto"}

## OAuth 2 com concessão de credenciais do cliente

Você pode configurar um destino de Credenciais de Cliente OAuth 2 (leia as [especificações de padrões RFC](https://tools.ietf.org/html/rfc6749#section-4.4)), que oferece suporte às entradas e saídas padrão listadas abaixo. Você pode personalizar os valores. Consulte [Personalizar a configuração do OAuth 2](#customize-configuration) para obter detalhes.

| Concessão do OAuth 2 | Entradas | Saídas |
|---------|----------|---------|
| Credenciais do cliente | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Para definir esse método de autorização para o seu destino, adicione as seguintes linhas à sua configuração quando você [criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authType` | String | Use &quot;OAUTH2&quot;. |
| `grant` | String | Use &quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | String | O URL do servidor de autorização, que emite um token de acesso e um token de atualização opcional. |
| `refreshTokenUrl` | String | *Opcional.* A URL no seu lado, que emite tokens de atualização. Frequentemente, `refreshTokenUrl` é o mesmo que `accessTokenUrl`. |
| `clientId` | String | A ID do cliente que seu sistema atribui à Adobe Experience Platform. |
| `clientSecret` | String | O segredo do cliente que seu sistema atribui à Adobe Experience Platform. |
| `scope` | Lista de strings | *Opcional*. Defina o escopo do que o token de acesso permite que o Experience Platform execute em seus recursos. Exemplo: &quot;ler, gravar&quot;. |

{style="table-layout:auto"}

## Personalizar a configuração do OAuth 2 {#customize-configuration}

As configurações descritas nas seções acima descrevem as concessões OAuth 2 padrão. No entanto, o sistema criado pelo Adobe oferece flexibilidade para que você possa usar parâmetros personalizados para quaisquer variações na concessão do OAuth 2. Para personalizar as configurações padrão do OAuth 2, use os parâmetros `authenticationDataFields`, conforme mostrado nos exemplos abaixo.

### Exemplo 1: uso de `authenticationDataFields` para capturar informações provenientes da resposta de autorização {#example-1}

Neste exemplo, uma plataforma de destino tem tokens de atualização que expiram após um determinado período. Nesse caso, o parceiro configura o campo personalizado `refreshTokenExpiration` para obter a expiração do token de atualização do campo `refresh_token_expires_in` na resposta da API.

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### Exemplo 2: usar `authenticationDataFields` para fornecer um token de atualização especial {#example-2}

Neste exemplo, um parceiro configura seu destino para fornecer um token de atualização especial. Além disso, a data de expiração dos tokens de acesso não é retornada na resposta da API para que eles possam codificar um valor padrão, nesse caso, 3600 segundos.

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### Exemplo 3: o usuário insere a ID do cliente e o segredo do cliente quando configura o destino {#example-3}

Neste exemplo, em vez de criar uma ID de cliente global e um segredo de cliente como mostrado na seção [Pré-requisitos em seu sistema](#prerequisites), o cliente precisa inserir a ID do cliente, o segredo do cliente e a ID da conta (a ID que o cliente usa para fazer logon no destino)

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



Você pode usar os seguintes parâmetros no `authenticationDataFields` para personalizar sua configuração do OAuth 2:

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authenticationDataFields.name` | String | O nome do campo personalizado. |
| `authenticationDataFields.title` | String | Um título que pode ser fornecido para o campo personalizado. |
| `authenticationDataFields.description` | String | Uma descrição do campo de dados personalizado que você configurou. |
| `authenticationDataFields.type` | String | Define o tipo de campo de dados personalizado. <br> Valores aceitos: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Booleano | Especifica se o campo de dados personalizado é necessário no fluxo de autorização. |
| `authenticationDataFields.format` | String | Quando você seleciona `"format":"password"`, o Adobe criptografa o valor do campo de dados de autorização. Quando usado com `"fieldType": "CUSTOMER"`, isso também oculta a entrada na interface do usuário quando o usuário digita no campo. |
| `authenticationDataFields.fieldType` | String | Indica se a entrada vem do parceiro (você) ou do usuário, quando ele configura seu destino no Experience Platform. |
| `authenticationDataFields.value` | String. Booleano. Número inteiro | O valor do campo de dados personalizado. O valor corresponde ao tipo escolhido de `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | String | Indica a qual campo do caminho de resposta da API você está fazendo referência. |

{style="table-layout:auto"}

## Atualização do token de acesso {#access-token-refresh}

A Adobe projetou um sistema que atualiza tokens de acesso expirados sem exigir que o usuário faça logon novamente em sua plataforma. O sistema é capaz de gerar um novo token para que a ativação no destino continue perfeitamente para o cliente.

Para configurar a atualização do token de acesso, talvez seja necessário configurar uma solicitação HTTP modelada que permita ao Adobe obter um novo token de acesso, usando um token de atualização. Se o token de acesso tiver expirado, o Adobe pegará a solicitação de modelo fornecida por você, adicionando os parâmetros fornecidos. Use o parâmetro `accessTokenRequest` para configurar um mecanismo de atualização do token de acesso.


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

Você pode usar os seguintes parâmetros no `accessTokenRequest` para personalizar o processo de atualização do token:

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | String | Usar `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para o valor em `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.urlBasedDestination.url.value` for uma constante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | String | O URL no qual o Experience Platform solicita o token de acesso. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para os valores em `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.httpTemplate.requestBody.value` for uma constante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | String | Use a linguagem de modelo para personalizar campos na solicitação HTTP para o endpoint do token de acesso. Para obter informações sobre como usar modelos para personalizar campos, consulte a seção [convenções de modelos](#templating-conventions). |
| `accessTokenRequest.httpTemplate.httpMethod` | String | Especifica o método HTTP usado para chamar o ponto de extremidade do token de acesso. Na maioria dos casos, esse valor é `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | String | Especifica o tipo de conteúdo da chamada HTTP para o seu ponto de extremidade de token de acesso. <br> Por exemplo: `application/x-www-form-urlencoded` ou `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | String | Especifica se algum cabeçalho deve ser adicionado à chamada HTTP para o ponto de extremidade do token de acesso. |
| `accessTokenRequest.responseFields.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para os valores em `accessTokenRequest.responseFields.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.responseFields.value` for uma constante. </li></li> |
| `accessTokenRequest.responseFields.value` | String | Use a linguagem de modelo para acessar campos na resposta HTTP a partir do endpoint do token de acesso. Para obter informações sobre como usar modelos para personalizar campos, consulte a seção [convenções de modelos](#templating-conventions). |
| `accessTokenRequest.validations.name` | String | Indica o nome fornecido para esta validação. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para os valores em `accessTokenRequest.validations.actualValue.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.validations.actualValue.value` for uma constante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | String | Use a linguagem de modelo para acessar campos na resposta HTTP. Para obter informações sobre como usar modelos para personalizar campos, consulte a seção [convenções de modelos](#templating-conventions). |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para os valores em `accessTokenRequest.validations.expectedValue.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.validations.expectedValue.value` for uma constante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | String | Use a linguagem de modelo para acessar campos na resposta HTTP. Para obter informações sobre como usar modelos para personalizar campos, consulte a seção [convenções de modelos](#templating-conventions). |

{style="table-layout:auto"}

## Convenções de modelos {#templating-conventions}

Dependendo da sua personalização de autorização, talvez seja necessário acessar campos de dados na resposta de autorização, como mostrado na seção anterior. Para fazer isso, familiarize-se com a [linguagem de modelo Pebble](https://pebbletemplates.io/) usada pelo Adobe e consulte as convenções de modelo abaixo para personalizar a implementação do OAuth 2.


| Prefixo | Descrição | Exemplo |
|---------|----------|---------|
| authData | Acesse qualquer valor do campo de dados do parceiro ou do cliente. | `{{ authData.accessToken }}` |
| response.body | Corpo da resposta HTTP | `{{ response.body.access_token }}` |
| response.status | Status de resposta HTTP | `{{ response.status }}` |
| response.headers | Cabeçalhos de resposta HTTP | `{{ response.headers.server[0] }}` |
| userContext | Acessar informações sobre a tentativa de autorização atual | <ul><li>`{{ userContext.sandboxName }}`</li><li>`{{ userContext.sandboxId }}`</li><li>`{{ userContext.imsOrgId }}`</li><li>`{{ userContext.client }} // the client executing the authorization attempt`</li></ul> |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Ao ler este artigo, você agora entende os padrões de autorização OAuth 2 compatíveis com o Adobe Experience Platform e sabe como configurar seu destino com suporte à autorização OAuth 2. Em seguida, você pode configurar o destino compatível com OAuth 2 usando o Destination SDK. Leia [Usar o Destination SDK para configurar seu destino](../../guides/configure-destination-instructions.md) para as próximas etapas.
