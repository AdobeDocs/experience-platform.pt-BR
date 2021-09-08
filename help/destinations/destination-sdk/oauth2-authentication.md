---
description: Esta página descreve os vários fluxos de autenticação OAuth 2 compatíveis com o SDK de destino e fornece instruções para configurar a autenticação OAuth 2 para o seu destino.
title: Autenticação OAuth 2
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 5%

---

# Autenticação OAuth 2

## Visão geral {#overview}

Use o SDK de destino para permitir que o Adobe Experience Platform se conecte ao seu destino usando a [estrutura de autenticação OAuth 2](https://tools.ietf.org/html/rfc6749).

Esta página descreve os vários fluxos de autenticação OAuth 2 compatíveis com o SDK de destino e fornece instruções para configurar a autenticação OAuth 2 para o seu destino.

## Como adicionar detalhes de autenticação do OAuth 2 à configuração de destino {#how-to-setup}

### Pré-requisitos no seu sistema {#prerequisites}

Como primeira etapa, você deve criar um aplicativo no sistema para o Adobe Experience Platform ou registrar o Experience Platform no sistema. O objetivo é gerar uma ID de cliente e um segredo de cliente, que são necessários para autenticar o Experience Platform para o seu destino. Como parte dessa configuração em seu sistema, você precisa do URL de redirecionamento/retorno de chamada do Adobe Experience Platform OAuth 2, que pode ser obtido na tabela abaixo.

>[!IMPORTANT]
>
>A etapa para registrar um URL de redirecionamento/retorno de chamada para o Adobe Experience Platform em seu sistema é necessária somente para o [OAuth 2 com o tipo de concessão Código de autorização](./oauth2-authentication.md#authorization-code). Para os outros dois tipos de concessão compatíveis (senha e credenciais do cliente), ignore esta etapa.

| URL de redirecionamento/retorno de chamada | Ambiente |
|---------|----------|
| `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback` | Produção |
| `https://platform-stage.adobe.io/data/core/activation/oauth/api/v1/callback` | Armazenamento temporário |

{style=&quot;table-layout:auto&quot;}

No final desta etapa, você deve ter:
* Uma ID de cliente;
* Um segredo de cliente;
* URL de retorno de autorização (para concessão).

### O que você precisa fazer no SDK de destino {#to-do-in-destination-sdk}

Para configurar a autenticação OAuth 2 para seu destino no Experience Platform, você deve adicionar seus detalhes do OAuth 2 ao [configuração de destino](./destination-configuration.md), no parâmetro `customerAuthenticationConfigurations`, usando o `platform.adobe.io/data/core/activation/authoring/destinations` [endpoint da API](./destination-configuration-api.md). Consulte o [exemplo de configuração](./destination-configuration.md#example-configuration). Instruções específicas sobre quais campos você precisa adicionar ao modelo de configuração, dependendo do tipo de concessão de autenticação OAuth 2, estão mais abaixo nesta página.

## Tipos de concessão OAuth 2 suportados {#oauth2-grant-types}

O Experience Platform suporta os três tipos de concessão OAuth 2 na tabela abaixo. Se você tiver uma configuração OAuth 2 personalizada, o Adobe poderá suportá-la com a ajuda de campos personalizados em sua integração. Consulte as seções para cada tipo de concessão para obter mais informações.

>[!IMPORTANT]
>
>* Você fornece os parâmetros de entrada, conforme instruído nas seções abaixo. Os sistemas internos do Adobe se conectam ao sistema de autenticação da plataforma e capturam parâmetros de saída, que são usados para autenticar o usuário e manter a autenticação no destino.
>* Os parâmetros de entrada realçados em negrito na tabela são parâmetros obrigatórios no fluxo de autenticação do OAuth 2. Os outros parâmetros são opcionais. Há outros parâmetros de entrada personalizados que não são mostrados aqui, mas que são descritos em comprimento nas seções [Personalizar a configuração do OAuth 2](./oauth2-authentication.md#customize-configuration) e [Atualizar token](./oauth2-authentication.md#access-token-refresh).


| Subvenção OAuth 2 | Entradas | Saídas |
|---------|----------|---------|
| Código de autorização | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Senha | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>senha</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Credencial do cliente | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

A tabela acima lista os campos usados nos fluxos OAuth 2 padrão. Além desses campos padrão, várias integrações de parceiros podem exigir entradas e saídas adicionais. O Adobe projetou uma estrutura de autenticação/autorização OAuth 2 flexível para o SDK de Destino que pode lidar com variações no padrão de campos padrão acima, ao mesmo tempo em que oferece suporte a um mecanismo para gerar automaticamente saídas inválidas, como tokens de acesso expirados.

A saída em todos os casos inclui um token de acesso, que é usado pelo Experience Platform para autenticar e manter a autenticação no destino.

O sistema que o Adobe projetou para a autenticação OAuth 2:
* Suporta todas as três concessões OAuth 2, além de contabilizar quaisquer variações delas, como campos de dados adicionais, chamadas de API não padrão e muito mais.
* Suporta tokens de acesso com valores de vida variáveis, sejam eles 90 dias, 30 minutos ou qualquer outro valor de duração especificado.
* Suporta fluxos de autorização OAuth 2 com ou sem tokens de atualização.

## OAuth 2 com código de autorização {#authorization-code}

Se o destino suporta um fluxo de Código de Autorização OAuth 2.0 padrão (leia as [especificações de padrões RFC](https://tools.ietf.org/html/rfc6749#section-4.1)) ou uma variação dele, consulte os campos obrigatórios e opcionais abaixo:

| Subvenção OAuth 2 | Entradas | Saídas |
|---------|----------|---------|
| Código de autorização | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Para configurar esse método de autenticação para o seu destino, adicione as seguintes linhas à sua configuração, no `/destinations` [endpoint](./destination-configuration.md):

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
| `accessTokenUrl` | String | O URL do seu lado, que emite tokens de acesso e, opcionalmente, de atualização. |
| `authorizationUrl` | String | O URL do seu servidor de autorização, onde você redireciona o usuário para fazer logon em seu aplicativo. |
| `refreshTokenUrl` | String | *Opcional.* O URL do seu lado, que emite tokens de atualização. Geralmente, `refreshTokenUrl` é o mesmo que `accessTokenUrl`. |
| `clientId` | String | A ID do cliente que seu sistema atribui ao Adobe Experience Platform. |
| `clientSecret` | String | O segredo do cliente que seu sistema atribui ao Adobe Experience Platform. |
| `scope` | Lista de cadeias de caracteres | *Opcional*. Defina o escopo do que o token de acesso permite que o Experience Platform execute em seus recursos. Exemplo: &quot;leia, escreva&quot;. |

{style=&quot;table-layout:auto&quot;}

## OAuth 2 com concessão de senha

Para a concessão de Senha OAuth 2 (leia os [padrões RFC especificados](https://tools.ietf.org/html/rfc6749#section-4.3)), o Experience Platform exige o nome de usuário e a senha do usuário. No fluxo de autenticação, o Experience Platform troca essas credenciais por um token de acesso e, opcionalmente, por um token de atualização.
O Adobe usa as entradas padrão abaixo para simplificar a configuração de destino, com a capacidade de substituir valores:

| Subvenção OAuth 2 | Entradas | Saídas |
|---------|----------|---------|
| Senha | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>senha</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> Não é necessário adicionar parâmetros para `username` e `password` na configuração abaixo. Ao adicionar `"grant": "OAUTH2_PASSWORD"` na configuração de destino, o sistema solicitará que o usuário forneça um nome de usuário e senha na interface do usuário do Experience Platform, quando eles autenticarem para o seu destino.

Para configurar esse método de autenticação para o seu destino, adicione as seguintes linhas à sua configuração, no `/destinations` [endpoint](./destination-configuration.md):

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
| `accessTokenUrl` | String | O URL do seu lado, que emite tokens de acesso e, opcionalmente, de atualização. |
| `clientId` | String | A ID do cliente que seu sistema atribui ao Adobe Experience Platform. |
| `clientSecret` | String | O segredo do cliente que seu sistema atribui ao Adobe Experience Platform. |
| `scope` | Lista de cadeias de caracteres | *Opcional*. Defina o escopo do que o token de acesso permite que o Experience Platform execute em seus recursos. Exemplo: &quot;leia, escreva&quot;. |

{style=&quot;table-layout:auto&quot;}

## Concessão de credenciais de cliente do OAuth 2

Você pode configurar uma Credenciais do Cliente OAuth 2 (leia o destino [Padrões RFC especificado](https://tools.ietf.org/html/rfc6749#section-4.4)), que suporta as entradas e saídas padrão listadas abaixo. Você pode personalizar os valores. Consulte [Personalizar a configuração do OAuth 2](./oauth2-authentication.md#customize-configuration) para obter detalhes.

| Subvenção OAuth 2 | Entradas | Saídas |
|---------|----------|---------|
| Credenciais do Cliente | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>escopo</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Para configurar esse método de autenticação para o seu destino, adicione as seguintes linhas à sua configuração, no `/destinations` [endpoint](./destination-configuration.md):

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
| `accessTokenUrl` | String | O URL do seu servidor de autorização, que emite um token de acesso e um token de atualização opcional. |
| `refreshTokenUrl` | String | *Opcional.* O URL do seu lado, que emite tokens de atualização. Geralmente, `refreshTokenUrl` é o mesmo que `accessTokenUrl`. |
| `clientId` | String | A ID do cliente que seu sistema atribui ao Adobe Experience Platform. |
| `clientSecret` | String | O segredo do cliente que seu sistema atribui ao Adobe Experience Platform. |
| `scope` | Lista de cadeias de caracteres | *Opcional*. Defina o escopo do que o token de acesso permite que o Experience Platform execute em seus recursos. Exemplo: &quot;leia, escreva&quot;. |

{style=&quot;table-layout:auto&quot;}

## Personalizar a configuração do OAuth 2 {#customize-configuration}

As configurações descritas nas seções acima descrevem as concessões padrão do OAuth 2. No entanto, o sistema projetado pelo Adobe oferece flexibilidade para que você possa usar parâmetros personalizados para quaisquer variações na concessão do OAuth 2. Para personalizar as configurações padrão do OAuth 2, use os parâmetros `authenticationDataFields`, conforme mostrado nos exemplos abaixo.

### Exemplo 1: Usar `authenticationDataFields` para capturar informações provenientes da resposta de autenticação {#example-1}

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

### Exemplo 2: Usar `authenticationDataFields` para fornecer um token de atualização especial {#example-2}

Neste exemplo, um parceiro configura seu destino para fornecer um token de atualização especial. Além disso, a data de expiração dos tokens de acesso não é retornada na resposta da API para que possam codificar um valor padrão, neste caso, 3600 segundos.

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

### Exemplo 3: O usuário insere a ID do cliente e o segredo do cliente ao configurar o destino {#example-3}

Neste exemplo, em vez de criar uma ID de cliente global e um segredo de cliente como mostrado na seção [Pré-requisitos em seu sistema](./oauth2-authentication.md#prerequisites), o cliente é obrigado a inserir a ID do cliente, o segredo do cliente e a ID da conta (a ID que o cliente usa para fazer logon no destino)

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
                    "fieldType": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "fieldType": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "fieldType": "CUSTOMER"
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



Você pode usar os seguintes parâmetros em `authenticationDataFields` para personalizar a configuração do OAuth 2:

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authenticationDataFields.name` | String | O nome do campo personalizado. |
| `authenticationDataFields.title` | String | Um título que pode ser fornecido para o campo personalizado. |
| `authenticationDataFields.description` | String | Uma descrição do campo de dados personalizado que você configurou. |
| `authenticationDataFields.type` | String | Define o tipo do campo de dados personalizado. <br> Valores aceitos:  `string`,  `boolean`,  `integer` |
| `authenticationDataFields.isRequired` | Booleano | Especifica se o campo de dados personalizado é obrigatório no fluxo de autenticação. |
| `authenticationDataFields.format` | String | Quando você seleciona `"format":"password"`, o Adobe criptografa o valor do campo de dados de autenticação. Quando usado com `"fieldType": "CUSTOMER"`, isso também oculta a entrada na interface do usuário quando o usuário digita no campo . |
| `authenticationDataFields.fieldType` | String | Indica se a entrada é proveniente do parceiro (você) ou do usuário, quando ele configura seu destino no Experience Platform. |
| `authenticationDataFields.value` | String. Booleano. Número inteiro | O valor do campo de dados personalizado. O valor corresponde ao tipo escolhido de `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | String | Indica qual campo do caminho de resposta da API você está referenciando. |

{style=&quot;table-layout:auto&quot;}

## Atualizar token de acesso {#access-token-refresh}

O Adobe projetou um sistema que atualiza tokens de acesso expirados sem exigir que o usuário faça logon novamente na plataforma. O sistema pode gerar um novo token para que a ativação para seu destino continue perfeitamente para o cliente.

Para configurar a atualização do token de acesso, talvez seja necessário configurar uma solicitação HTTP templatizada que permita que o Adobe obtenha um novo token de acesso usando um token de atualização. Se o token de acesso tiver expirado, o Adobe aceitará a solicitação modelo fornecida por você, adicionando os parâmetros fornecidos. Use o parâmetro `accessTokenRequest` para configurar um mecanismo de atualização de token de acesso.


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

Você pode usar os seguintes parâmetros em `accessTokenRequest` para personalizar o processo de atualização de token:

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | String | Use  `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se usar modelos para o valor em `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.urlBasedDestination.url.value` for uma constante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | String | O URL no qual o Experience Platform solicita o token de acesso. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para os valores em `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.httpTemplate.requestBody.value` for uma constante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | String | Use a linguagem de modelo para personalizar campos na solicitação HTTP para o endpoint do token de acesso. Para obter informações sobre como usar modelos para personalizar campos, consulte a seção [convenções de modelo](./oauth2-authentication.md#templating-conventions) . |
| `accessTokenRequest.httpTemplate.httpMethod` | String | Especifica o método HTTP usado para chamar o endpoint do token de acesso. Na maioria dos casos, esse valor é `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | String | Especifica o tipo de conteúdo da chamada HTTP para o endpoint do token de acesso. <br> Por exemplo:  `application/x-www-form-urlencoded` ou  `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | String | Especifica se algum cabeçalho deve ser adicionado à chamada HTTP para seu ponto de extremidade de token de acesso. |
| `accessTokenRequest.responseFields.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para os valores em `accessTokenRequest.responseFields.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.responseFields.value` for uma constante. </li></li> |
| `accessTokenRequest.responseFields.value` | String | Use a linguagem de modelo para acessar campos na resposta HTTP do seu ponto de extremidade de token de acesso. Para obter informações sobre como usar modelos para personalizar campos, consulte a seção [convenções de modelo](./oauth2-authentication.md#templating-conventions) . |
| `accessTokenRequest.validations.name` | String | Indica o nome fornecido para esta validação. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para os valores em `accessTokenRequest.validations.actualValue.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.validations.actualValue.value` for uma constante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | String | Use a linguagem de modelo para acessar campos na resposta HTTP. Para obter informações sobre como usar modelos para personalizar campos, consulte a seção [convenções de modelo](./oauth2-authentication.md#templating-conventions) . |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | String | <ul><li>Use `PEBBLE_V1` se você usar modelos para os valores em `accessTokenRequest.validations.expectedValue.value`.</li><li> Use `NONE` se o valor no campo `accessTokenRequest.validations.expectedValue.value` for uma constante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | String | Use a linguagem de modelo para acessar campos na resposta HTTP. Para obter informações sobre como usar modelos para personalizar campos, consulte a seção [convenções de modelo](./oauth2-authentication.md#templating-conventions) . |

{style=&quot;table-layout:auto&quot;}

## Convenções de modelo {#templating-conventions}

Dependendo da personalização da autenticação, talvez seja necessário acessar campos de dados na resposta de autenticação, conforme mostrado na seção anterior. Para fazer isso, familiarize-se com o [Pebble template language](https://pebbletemplates.io/) usado pelo Adobe e consulte as convenções de modelo abaixo para personalizar a implementação do OAuth 2.


| Prefixo | Descrição | Exemplo |
|---------|----------|---------|
| authData | Acesse qualquer valor do campo de dados de parceiro ou cliente. | ``{{ authData.accessToken }}`` |
| response.body | Corpo de resposta HTTP | ``{{ response.body.access_token }}`` |
| response.status | Status da resposta HTTP | ``{{ response.status }}`` |
| response.headers | Cabeçalhos de resposta HTTP | ``{{ response.headers.server[0] }}`` |
| authContext | Acessar informações sobre a tentativa de autenticação atual | <ul><li>`{{ authContext.sandboxName }} `</li><li>`{{ authContext.sandboxId }} `</li><li>`{{ authContext.imsOrgId }} `</li><li>`{{ authContext.client }} // the client executing the authentication attempt `</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas {#next-steps}

Ao ler este artigo, agora você compreende os padrões de autenticação OAuth 2 compatíveis com o Adobe Experience Platform e sabe configurar seu destino com o suporte de autenticação OAuth 2. Em seguida, você pode configurar o destino compatível com o OAuth 2 usando o SDK de destino. Leia [Usar SDK de destino para configurar seu destino](./configure-destination-instructions.md) para as próximas etapas.
