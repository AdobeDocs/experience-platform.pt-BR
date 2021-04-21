---
keywords: Experience Platform, home, tópicos populares, Autenticar, acesso
solution: Experience Platform
title: Autenticar e acessar APIs do Experience Platform
topic-legacy: tutorial
type: Tutorial
description: 'Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor da Adobe Experience Platform para fazer chamadas para APIs da Experience Platform. '
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 4%

---


# Autentique e acesse APIs [!DNL Experience Platform]

Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor do Adobe Experience Platform para fazer chamadas para [!DNL Experience Platform] APIs.

## Autenticar para fazer chamadas de API

Para manter a segurança de seus aplicativos e usuários, todas as solicitações para APIs do Adobe I/O devem ser autenticadas e autorizadas usando padrões como OAuth e JSON Web Tokens (JWT). O JWT é então usado junto com informações específicas do cliente para gerar seu token de acesso pessoal.

Este tutorial aborda as etapas de autenticação através da criação de um token de acesso descrito no seguinte fluxograma:
![](images/authentication/authentication-flowchart.png)

## Pré-requisitos

Para fazer chamadas com êxito para APIs [!DNL Experience Platform], você precisa do seguinte:

* Uma Organização IMS com acesso à Adobe Experience Platform
* Uma conta Adobe ID registrada
* Um administrador do Admin Console para adicioná-lo como um **desenvolvedor** e um **usuário** para um produto.

As seções a seguir abordam as etapas para criar uma Adobe ID e se tornar um desenvolvedor e usuário de uma organização.

### Criar uma Adobe ID

Se você não tiver uma Adobe ID, poderá criar uma usando as seguintes etapas:

1. Vá para [Console do Desenvolvedor do Adobe](https://console.adobe.io)
2. Selecione **[!UICONTROL create a new account]**
3. Concluir o processo de inscrição

## Torne-se um desenvolvedor e usuário para [!DNL Experience Platform] de uma organização

Antes de criar integrações no Adobe I/O, sua conta deve ter permissões de desenvolvedor para um produto em uma Organização IMS. Informações detalhadas sobre contas de desenvolvedores no Admin Console podem ser encontradas no [support document](https://helpx.adobe.com/br/enterprise/using/manage-developers.html) para gerenciar desenvolvedores.

**Obter acesso do desenvolvedor**

Entre em contato com um administrador [!DNL Admin Console] em sua organização para adicioná-lo como desenvolvedor de um dos produtos de sua organização usando o [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

O administrador deve atribuir você como desenvolvedor a pelo menos um perfil de produto para continuar.

![](images/authentication/add-developer.png)

Depois de ser atribuído como um desenvolvedor, você terá privilégios de acesso para criar integrações em [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Essas integrações são um pipeline de aplicativos e serviços externos para a API do Adobe.

**Obter acesso do usuário**

O administrador [!DNL Admin Console] também deve adicioná-lo ao produto como usuário.

![](images/authentication/assign-users.png)

Semelhante ao processo de adição de desenvolvedor, o administrador deve atribuir você a pelo menos um perfil de produto para prosseguir.

![](images/authentication/assign-user-details.png)

## Gerar credenciais de acesso no Console do desenvolvedor do Adobe

>[!NOTE]
>
>Se você estiver seguindo este documento do [Guia do desenvolvedor do Privacy Service](../privacy-service/api/getting-started.md), agora poderá retornar a esse guia para gerar as credenciais de acesso exclusivas de [!DNL Privacy Service].

Usando o Console do Desenvolvedor do Adobe, você deve gerar as três credenciais de acesso a seguir:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Seu `{IMS_ORG}` e `{API_KEY}` precisam ser gerados apenas uma vez e podem ser reutilizados em futuras chamadas de API [!DNL Platform]. No entanto, seu `{ACCESS_TOKEN}` é temporário e deve ser gerado novamente a cada 24 horas.

As etapas são abordadas detalhadamente abaixo.

### Configuração única

Vá para [Console do desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui) e faça logon com sua Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criar um projeto vazio](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) na documentação do Console do desenvolvedor do Adobe.

Depois de criar um novo projeto, selecione **[!UICONTROL Add API]** na tela **Visão geral do projeto**.

![](images/authentication/add-api-button.png)

A tela **Adicionar uma API** é exibida. Selecione o ícone do produto para Adobe Experience Platform e escolha **[!UICONTROL Experience Platform API]** antes de selecionar **[!UICONTROL Next]**.

![](images/authentication/add-platform-api.png)

Depois de selecionar [!DNL Experience Platform] como a API a ser adicionada ao projeto, siga as etapas descritas no tutorial em [adicionar uma API a um projeto usando uma conta de serviço (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (começando pela etapa &quot;Configurar API&quot;) para concluir o processo.

Depois que a API tiver sido adicionada ao projeto, a página **Visão geral do projeto** exibirá as credenciais a seguir que são necessárias em todas as chamadas para APIs [!DNL Experience Platform]:

* `{API_KEY}` (ID do cliente)
* `{IMS_ORG}` (ID da organização)

![](./images/authentication/api-key-ims-org.png)

### Autenticação para cada sessão

A credencial final necessária que você deve coletar é seu `{ACCESS_TOKEN}`. Ao contrário dos valores para `{API_KEY}` e `{IMS_ORG}`, um novo token deve ser gerado a cada 24 horas para continuar usando [!DNL Platform] APIs.

Para gerar um novo `{ACCESS_TOKEN}`, siga as etapas para [gerar um token JWT](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) no guia de credenciais do Console do Desenvolvedor.

## Testar credenciais de acesso

Depois de reunir todas as três credenciais necessárias, tente fazer a seguinte chamada de API. Essa chamada listará todas as classes [!DNL Experience Data Model] (XDM) no contêiner `global` do Registro de Schema:

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

**Resposta**

Se sua resposta for semelhante à mostrada abaixo, suas credenciais serão válidas e funcionarão. (Essa resposta foi truncada para espaço.)

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

[](https://www.postman.com/) O Postmanis é uma ferramenta popular para trabalhar com APIs RESTful. Este [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descreve como você pode configurar o postman para executar automaticamente a autenticação JWT e usá-lo para consumir APIs do Adobe Experience Platform.

## Próximas etapas

Ao ler este documento, você reuniu e testou com êxito suas credenciais de acesso para [!DNL Platform] APIs. Agora você pode seguir com as chamadas de API de exemplo fornecidas em toda a [documentação](../landing/documentation/overview.md).

Além dos valores de autenticação coletados neste tutorial, muitas APIs [!DNL Platform] também exigem que um `{SANDBOX_NAME}` válido seja fornecido como um cabeçalho. Consulte a [visão geral das sandboxes](../sandboxes/home.md) para obter mais informações.