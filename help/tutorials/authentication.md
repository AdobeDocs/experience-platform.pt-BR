---
keywords: Experience Platform;home;popular topics;Authenticate;access
solution: Experience Platform
title: Autenticar e acessar APIs Experience Platform
topic: tutorial
type: Tutorial
description: 'Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor da Adobe Experience Platform para fazer chamadas para APIs da Experience Platform. '
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 4%

---


# Autenticar e acessar [!DNL Experience Platform] APIs

Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor Adobe Experience Platform para fazer chamadas para [!DNL Experience Platform] APIs.

## Autenticar para fazer chamadas de API

Para manter a segurança de seus aplicativos e usuários, todas as solicitações para APIs da Adobe I/O devem ser autenticadas e autorizadas usando padrões como OAuth e JSON Web Tokens (JWT). O JWT é então usado junto com informações específicas do cliente para gerar seu token de acesso pessoal.

Este tutorial aborda as etapas de autenticação através da criação de um token de acesso descrito no seguinte fluxograma:
![](images/authentication/authentication-flowchart.png)

## Pré-requisitos

Para realizar chamadas com êxito para [!DNL Experience Platform] APIs, é necessário o seguinte:

* Uma organização IMS com acesso ao Adobe Experience Platform
* Uma conta Adobe ID registrada
* Um administrador de Admin Console para adicioná-lo como **desenvolvedor** e um **usuário** para um produto.

As seções a seguir abordam as etapas para criar um Adobe ID e se tornar um desenvolvedor e usuário de uma organização.

### Criar um Adobe ID

Se você não tiver um Adobe ID, poderá criar um usando as seguintes etapas:

1. Vá para [Console do Desenvolvedor do Adobe](https://console.adobe.io)
2. Selecione **[!UICONTROL criar uma nova conta]**
3. Concluir o processo de inscrição

## Torne-se um desenvolvedor e usuário para [!DNL Experience Platform] de uma organização

Antes de criar integrações no Adobe I/O, sua conta deve ter permissões de desenvolvedor para um produto em uma organização IMS. Informações detalhadas sobre contas de desenvolvedor no Admin Console podem ser encontradas no documento [support](https://helpx.adobe.com/br/enterprise/using/manage-developers.html) para gerenciamento de desenvolvedores.

**Obter acesso do desenvolvedor**

Entre em contato com um administrador [!DNL Admin Console] em sua organização para adicioná-lo como desenvolvedor para um dos produtos da organização usando [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

O administrador deve atribuí-lo como desenvolvedor a pelo menos um perfil de produto para continuar.

![](images/authentication/add-developer.png)

Depois que você for atribuído como um desenvolvedor, terá privilégios de acesso para criar integrações em [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Essas integrações são um pipeline de aplicativos e serviços externos para a API do Adobe.

**Obter acesso do usuário**

O administrador [!DNL Admin Console] também deve adicioná-lo ao produto como usuário.

![](images/authentication/assign-users.png)

Semelhante ao processo de adição de um desenvolvedor, o administrador deve atribuí-lo a pelo menos um perfil de produto para continuar.

![](images/authentication/assign-user-details.png)

## Gerar credenciais de acesso no Adobe Developer Console

>[!NOTE]
>
>Se você estiver seguindo esse documento do [guia do desenvolvedor do Privacy Service](../privacy-service/api/getting-started.md), agora você pode voltar para esse guia para gerar as credenciais de acesso exclusivas de [!DNL Privacy Service].

Usando o Console do desenvolvedor do Adobe, você deve gerar as três credenciais de acesso a seguir:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Seus `{IMS_ORG}` e `{API_KEY}` precisam ser gerados apenas uma vez e podem ser reutilizados em futuras chamadas da API [!DNL Platform]. No entanto, seu `{ACCESS_TOKEN}` é temporário e deve ser regenerado a cada 24 horas.

As etapas são abordadas em detalhes abaixo.

### Configuração única

Vá para [Console do desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criar um projeto vazio](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) na documentação do Console do desenvolvedor do Adobe.

Depois de criar um novo projeto, selecione **[!UICONTROL Adicionar API]** na tela **Visão geral do projeto**.

![](images/authentication/add-api-button.png)

A tela **Adicionar uma API** é exibida. Selecione o ícone do produto para Adobe Experience Platform e escolha **[!UICONTROL API Experience Platform]** antes de selecionar **[!UICONTROL Próximo]**.

![](images/authentication/add-platform-api.png)

Depois de selecionar [!DNL Experience Platform] como a API a ser adicionada ao projeto, siga as etapas descritas no tutorial em [adicionar uma API a um projeto usando uma conta de serviço (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partir da etapa &quot;Configurar API&quot;) para concluir o processo.

Depois que a API for adicionada ao projeto, a página **Visão geral do projeto** exibirá as seguintes credenciais necessárias em todas as chamadas para [!DNL Experience Platform] APIs:

* `{API_KEY}` (ID do cliente)
* `{IMS_ORG}` (ID da organização)

![](./images/authentication/api-key-ims-org.png)

### Autenticação para cada sessão

A credencial final necessária que você deve coletar é seu `{ACCESS_TOKEN}`. Ao contrário dos valores para `{API_KEY}` e `{IMS_ORG}`, um novo token deve ser gerado a cada 24 horas para continuar usando [!DNL Platform] APIs.

Para gerar um novo `{ACCESS_TOKEN}`, siga as etapas para [gerar um token JWT](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) no guia de credenciais do Developer Console.

## Testar credenciais de acesso

Depois de coletar as três credenciais necessárias, você pode tentar fazer a seguinte chamada de API. Esta chamada lista todas as classes [!DNL Experience Data Model] (XDM) no container `global` do Registro do Schema:

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

Se sua resposta for semelhante à mostrada abaixo, suas credenciais serão válidas e estarão funcionando. (Essa resposta foi truncada para espaço.)

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

[O ](https://www.postman.com/) Postmanis é uma ferramenta popular para trabalhar com RESTful APIs. Esta [publicação média](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descreve como configurar o carteiro para executar automaticamente a autenticação JWT e usá-la para consumir APIs Adobe Experience Platform.

## Próximas etapas

Ao ler este documento, você reuniu e testou com êxito suas credenciais de acesso para [!DNL Platform] APIs. Agora você pode seguir com as chamadas de API de exemplo fornecidas em toda a [documentação](../landing/documentation/overview.md).

Além dos valores de autenticação reunidos neste tutorial, muitas [!DNL Platform] APIs também exigem que um `{SANDBOX_NAME}` válido seja fornecido como um cabeçalho. Consulte [sandboxes overview](../sandboxes/home.md) para obter mais informações.