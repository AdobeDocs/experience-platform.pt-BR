---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Autenticar e acessar APIs da plataforma Experience
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# Autenticar e acessar as APIs da plataforma Experience

Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor da plataforma Adobe Experience para fazer chamadas às APIs da plataforma Experience.

## Autenticar para fazer chamadas de API

Para manter a segurança de seus aplicativos e usuários, todas as solicitações para APIs de E/S da Adobe devem ser autenticadas e autorizadas usando padrões como OAuth e JSON Web Tokens (JWT). O JWT é então usado junto com informações específicas do cliente para gerar seu token de acesso pessoal.

Este tutorial aborda as etapas de autenticação através da criação de um token de acesso descrito no seguinte fluxograma:
![](images/authentication/authentication-flowchart.png)

## Pré-requisitos

Para fazer chamadas com êxito para APIs da plataforma Experience, é necessário o seguinte:

* Uma organização IMS com acesso à Adobe Experience Platform
* Uma conta da Adobe ID registrada
* Um administrador do Admin Console para adicioná-lo como um **desenvolvedor** e um **usuário** para um produto.

As seções a seguir percorrem as etapas para criar uma Adobe ID e se tornarem desenvolvedores e usuários de uma organização.

### Criar uma Adobe ID

Se você não tiver uma Adobe ID, poderá criar uma usando as seguintes etapas:

1. Ir para o console de E/S [da Adobe](https://console.adobe.io)
2. Clique em **criar uma nova conta**
3. Concluir o processo de inscrição


### Torne-se um desenvolvedor e usuário da Experience Platform para uma organização

Antes de criar integrações em E/S da Adobe, sua conta deve ter permissões de desenvolvedor para um produto em uma organização IMS. Informações detalhadas sobre contas de desenvolvedor no Admin Console podem ser encontradas no documento [de](https://helpx.adobe.com/enterprise/using/manage-developers.html) suporte para o gerenciamento de desenvolvedores.

**Obter acesso do desenvolvedor**

Entre em contato com um administrador do Admin Console em sua organização para adicioná-lo como desenvolvedor para um dos produtos da organização usando o [Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

O administrador deve atribuí-lo como desenvolvedor a pelo menos um perfil de produto para continuar.

![](images/authentication/add-developer.png)

Depois que você for atribuído como desenvolvedor, terá privilégios de acesso para criar integrações em E/S [da Adobe](https://console.adobe.io/). Essas integrações são um pipeline de aplicativos e serviços externos para a API da Adobe.

**Obter acesso do usuário**

O administrador do Admin Console também deve adicioná-lo ao produto como usuário.

![](images/authentication/assign-users.png)

Semelhante ao processo de adição de um desenvolvedor, o administrador deve atribuí-lo a pelo menos um perfil de produto para continuar.

![](images/authentication/assign-user-details.png)


## Configuração única

As etapas a seguir só precisam ser executadas uma vez:

* Faça logon no console de E/S da Adobe
* Criar integração
* Copiar Valores de Acesso para Baixo

Depois de ter seus valores de integração e acesso, você poderá reutilizá-los para autenticação no futuro. Cada etapa é abordada em detalhes abaixo.

### Faça logon no Adobe I/O Console

Vá para o console [de E/S da](https://console.adobe.io/) Adobe e faça logon com sua Adobe ID.

Depois que você estiver conectado, clique na guia **Integrações** na parte superior da tela. Uma Integração é uma conta de serviço criada para a Organização IMS selecionada. Você só pode fazer chamadas para a Organização IMS na qual a Integração é criada.

>[!NOTE]
>Se sua conta estiver associada a várias organizações, o menu suspenso na parte superior direita da tela permite alternar facilmente entre elas.

### Criar integração

Na página **Integrações** , clique em **Nova integração** para start do processo. O processo contém três etapas:
* Escolher tipo de integração
* Escolha com qual serviço da Adobe se integrar
* Adicionar detalhes de integração, chave pública e perfil de produto

![](images/authentication/integrations.png)

#### Escolher tipo de integração

A tela seguinte pergunta se você deseja acessar uma API ou receber quase eventos em tempo real. Selecione **Acessar uma API** e **Continuar**.

![](images/authentication/create-new-integration.png)

#### Escolha com qual serviço da Adobe se integrar

Se sua conta estiver associada a várias organizações IMS, você pode alternar entre elas usando o menu suspenso na parte superior direita. Selecione **Workshop** e API **da plataforma** Experience em Plataforma **** Adobe Experience para acessar as APIs.

![](images/authentication/integration-select-service.png)

Clique em **Continuar** para ir para a próxima seção.

#### Adicionar detalhes de integração, chave pública e perfil de produto

A tela seguinte solicita que você preencha seus detalhes de integração, insira seu certificado de chave pública e selecione um perfil de produto.

![](images/authentication/integration-details.png)

Primeiro, insira os detalhes de integração. Em seguida, selecione um perfil de produto. Os perfis de produtos concedem acesso granular a um grupo de recursos pertencentes ao serviço selecionado em etapas anteriores.

Para a seção de certificado, você deve gerar um certificado:

**Para plataformas MacOS e Linux:**

Abra a linha de comando e execute o seguinte comando:

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**Para plataformas Windows:**

1. Baixar um cliente openssl para gerar certificados públicos (por exemplo, cliente [](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip)Openssl windows)

1. Extraia a pasta e copie-a para C:/libs/ location.

1. Abra o prompt de linha de comando e execute os seguintes comandos:

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

Você receberá uma resposta semelhante à seguinte, solicitando que você insira algumas informações sobre si mesmo:

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

Depois de inserir as informações, dois arquivos são gerados: `certificate_pub.crt` e `private.key`.

>[!NOTE]
>`certificate_pub.crt` expirará em 365 dias. Você pode tornar o período mais longo alterando o valor de `days` no `openssl` comando acima, mas girar as credenciais periodicamente é uma boa prática de segurança.

O `private.key` será usado para gerar nosso JWT na seção posterior.

O `certificate_pub.crt` é usado para criar uma chave de API. Retorne ao console de E/S da Adobe e clique em **Selecionar um arquivo** para fazer upload do seu `certificate_pub.crt` arquivo.

Clique em **Criar integração** para concluir o processo.

### Copiar valores de acesso para baixo

Depois de criar sua integração, você pode visualização seus detalhes. Clique em **Recuperar segredo** do cliente e sua tela será semelhante a esta:

![](images/authentication/access-values.png)

Copie os valores para `{API KEY}`, `{IMS ORG}` que é a ID da organização, e `{CLIENT SECRET}` como eles serão usados na próxima etapa.

## Autenticação para cada sessão

A etapa final é gerar suas chamadas `{ACCESS_TOKEN}` que serão usadas para autenticar suas chamadas de API. O token de acesso deve ser incluído no cabeçalho Autorização de cada chamada de API feita para a Adobe Experience Platform. Os Tokens de acesso expiram após 24 horas, após as quais novos tokens devem ser gerados para continuar usando as APIs.

### Criar JWT

Enquanto estiver na página de detalhes da integração no Console de E/S da Adobe, navegue até a guia **JWT** :

![](images/authentication/generate-jwt.png)

A página solicita que você insira o `private.key` que você criou na seção anterior. Abra a linha de comando para visualização do conteúdo do seu `private.key` arquivo:

```shell
cat private.key
```

Sua saída será parecida com esta:

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

Copie a saída inteira e cole-a no campo de texto, em seguida, clique em **Gerar JWT**. Copie seu JWT gerado para a próxima etapa.

![](images/authentication/generated-jwt.png)

### Gerar token de acesso

Você pode gerar um token de acesso por meio de um comando cURL. Se você não tiver cURL instalado, poderá instalá-lo usando `npm install curl`. Você pode ler mais sobre cURL [aqui](https://curl.haxx.se/)

Depois que cURL estiver instalado, você precisará trocar os campos no seguinte comando por seus próprios `{API_KEY}`, `{CLIENT_SECRET}`e `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

Se o resultado for bem-sucedido, a saída será algo como:

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

Seu token de acesso é o valor sob a `access_token` chave. Este token de acesso é de `expires_in` 86399947 milissegundos (24 horas). Depois, você terá que gerar um novo token de acesso seguindo as mesmas etapas acima.

Agora você está pronto para fazer solicitações de API na Adobe Experience Platform!

### Testar código de acesso

Para testar se o token de acesso é válido, tente fazer a seguinte chamada de API. Esta chamada irá lista em todas as classes dentro do `global` container:

>[!NOTE]
>`{API_KEY}` e `{IMS_ORG}` se referem aos valores que você gerou acima.

**Solicitação**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


Se sua resposta for semelhante à mostrada abaixo, então sua resposta `access_token` é válida e está funcionando. (Essa resposta foi truncada para espaço.)

**Resposta**

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Usar o Postman para autenticação JWT e chamadas de API

[O Postman](https://www.getpostman.com/) é uma ferramenta popular para trabalhar com RESTful APIs. Esta publicação [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Média descreve como você pode configurar o carteiro para executar automaticamente a autenticação JWT e usá-la para consumir as APIs da plataforma Adobe Experience.