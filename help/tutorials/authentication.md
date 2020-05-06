---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Autenticar e acessar APIs da plataforma Experience
topic: tutorial
translation-type: tm+mt
source-git-commit: e1ba476fffc164b78decd7168192714993c791bc
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 1%

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

1. Ir para o console do desenvolvedor [Adobe](https://console.adobe.io)
2. Clique em **criar uma nova conta**
3. Concluir o processo de inscrição

## Torne-se um desenvolvedor e usuário da Experience Platform para uma organização

Antes de criar integrações em E/S da Adobe, sua conta deve ter permissões de desenvolvedor para um produto em uma organização IMS. Informações detalhadas sobre contas de desenvolvedor no Admin Console podem ser encontradas no documento [de](https://helpx.adobe.com/br/enterprise/using/manage-developers.html) suporte para o gerenciamento de desenvolvedores.

**Obter acesso do desenvolvedor**

Entre em contato com um administrador do Admin Console em sua organização para adicioná-lo como desenvolvedor para um dos produtos da organização usando o [Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

O administrador deve atribuí-lo como desenvolvedor a pelo menos um perfil de produto para continuar.

![](images/authentication/add-developer.png)

Depois que você for atribuído como desenvolvedor, terá privilégios de acesso para criar integrações em E/S [da Adobe](https://www.adobe.com/go/devs_console_ui). Essas integrações são um pipeline de aplicativos e serviços externos para a API da Adobe.

**Obter acesso do usuário**

O administrador do Admin Console também deve adicioná-lo ao produto como usuário.

![](images/authentication/assign-users.png)

Semelhante ao processo de adição de um desenvolvedor, o administrador deve atribuí-lo a pelo menos um perfil de produto para continuar.

![](images/authentication/assign-user-details.png)


## Gerar credenciais de acesso no Adobe Developer Console

Usando o Adobe Developer Console, você deve gerar as três credenciais de acesso a seguir:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Sua `{IMS_ORG}` e `{API_KEY}` só precisam ser geradas uma vez e podem ser reutilizadas em futuras chamadas à API da plataforma. No entanto, o seu `{ACCESS_TOKEN}` é temporário e precisa ser regenerado a cada 24 horas.

As etapas são abordadas em detalhes abaixo.

### Configuração única

Acesse o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e faça logon com sua Adobe ID. Em seguida, siga as etapas descritas no tutorial sobre como [criar um projeto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vazio na documentação do Adobe Developer Console.

Depois de criar um novo projeto, clique em **[!UICONTROL Adicionar API]** na tela Visão geral _do_ projeto.

![](images/authentication/add-api-button.png)

A tela _Adicionar uma API_ é exibida. Clique no ícone de produto da Adobe Experience Platform e selecione API **[!UICONTROL da plataforma de]** experiência antes de clicar em **[!UICONTROL Avançar]**.

![](images/authentication/add-platform-api.png)

Depois de selecionar a Plataforma de experiência como a API a ser adicionada ao projeto, siga as etapas descritas no tutorial sobre como [adicionar uma API a um projeto usando uma conta de serviço (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partir da etapa &quot;Configurar API&quot;) para concluir o processo.

Depois que a API é adicionada ao projeto, a página de visão geral _do_ projeto exibe as seguintes credenciais necessárias em todas as chamadas às APIs da plataforma Experience:

* `{API_KEY}` (ID do cliente)
* `{IMS_ORG}` (ID da organização)

![](./images/authentication/api-key-ims-org.png)

### Autenticação para cada sessão

A credencial final necessária que você deve coletar é sua `{ACCESS_TOKEN}`. Diferentemente dos valores para `{API_KEY}` e `{IMS_ORG}`, um novo token deve ser gerado a cada 24 horas para continuar usando as APIs de plataforma.

Para gerar um novo `{ACCESS_TOKEN}`, siga as etapas para [gerar um token](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) JWT no guia de credenciais do Developer Console.

## Testar credenciais de acesso

Depois de coletar as três credenciais necessárias, você pode tentar fazer a seguinte chamada de API. Esta chamada fará a lista de todas as classes do Modelo de Dados de Experiência (XDM) no `global` container do Registro do Schema:

**Formato da API**

```http
GET /global/classes
```

**Solicitação**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

Se sua resposta for semelhante à mostrada abaixo, suas credenciais serão válidas e estarão funcionando. (Essa resposta foi truncada para espaço.)

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

## Próximas etapas

Ao ler este documento, você reuniu e testou com êxito suas credenciais de acesso para APIs de plataforma. Agora você pode seguir com as chamadas de API de exemplo fornecidas na [documentação](../landing/documentation/overview.md).

Além dos valores de autenticação reunidos neste tutorial, muitas APIs de plataforma também exigem um valor válido `{SANDBOX_NAME}` para ser fornecido como cabeçalho. Consulte a visão geral [das](../sandboxes/home.md) caixas de proteção para obter mais informações.