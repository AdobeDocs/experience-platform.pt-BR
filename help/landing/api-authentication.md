---
keywords: Experience Platform;início;tópicos populares;Autenticar;acesso;;home;popular topics;Authenticate;access
solution: Experience Platform
title: Autenticar e acessar APIs de Experience Platform
type: Tutorial
description: Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor da Adobe Experience Platform para fazer chamadas para APIs da Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: fa4786b081b46c8f3c0030282ae3900891fbd652
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 8%

---


# Autenticar e acessar APIs da Experience Platform

Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor da Adobe Experience Platform para fazer chamadas para APIs da Experience Platform. Ao final deste tutorial, você terá gerado as seguintes credenciais, necessárias para todas as chamadas de API da plataforma:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

Para manter a segurança de seus aplicativos e usuários, todas as solicitações para APIs Adobe I/O devem ser autenticadas e autorizadas usando padrões como OAuth e JSON Web Tokens (JWT). Um JWT é usado junto com informações específicas do cliente para gerar seu token de acesso pessoal.

Este tutorial aborda como coletar as credenciais necessárias para autenticar chamadas de API da plataforma, conforme descrito no seguinte fluxograma:

![](./images/api-authentication/authentication-flowchart.png)

## Pré-requisitos

Para fazer chamadas com êxito para APIs Experience Platform, você deve ter o seguinte:

* Uma organização com acesso ao Adobe Experience Platform.
* Um administrador de Admin Console que pode adicioná-lo como desenvolvedor e usuário para um perfil de produto.

Você também deve ter uma Adobe ID para concluir este tutorial. Se você não tiver uma Adobe ID, poderá criar uma usando as seguintes etapas:

1. Ir para [Console do Adobe Developer](https://console.adobe.io).
2. Selecionar **[!UICONTROL Criar uma nova conta]**.
3. Conclua o processo de inscrição.

## Obter acesso de desenvolvedor e usuário para o Experience Platform

Antes de criar integrações no Console do Adobe Developer, sua conta deve ter permissões de desenvolvedor e usuário para um perfil de produto do Experience Platform no Adobe Admin Console.

### Obter acesso de desenvolvedor

Entre em contato com um [!DNL Admin Console] administrador na organização para adicioná-lo como desenvolvedor a um perfil de produto Experience Platform usando o [[!DNL Admin Console]](https://adminconsole.adobe.com/). Consulte a [!DNL Admin Console] para obter instruções específicas sobre como [gerenciar o acesso de desenvolvedor para perfis de produtos](https://helpx.adobe.com/br/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Depois de atribuído como desenvolvedor, você pode começar a criar integrações no [Console do Adobe Developer](https://www.adobe.com/go/devs_console_ui). Essas integrações são um pipeline de aplicativos e serviços externos para APIs Adobe.

### Obter acesso do usuário

Seu [!DNL Admin Console] O administrador também deve adicioná-lo como usuário ao mesmo perfil de produto. Consulte o guia sobre [gerenciamento de grupos de usuários no [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) para obter mais informações.

## Gerar uma chave de API, uma ID da organização e um segredo do cliente {#api-ims-secret}

>[!NOTE]
>
>Se você estiver seguindo este documento do [Guia da API do Privacy Service](../privacy-service/api/getting-started.md), agora você pode retornar a esse guia para gerar as credenciais de acesso exclusivas para [!DNL Privacy Service].

Depois de receber acesso de desenvolvedor e usuário à Platform por meio do [!DNL Admin Console], a próxima etapa é gerar o `{ORG_ID}` e `{API_KEY}` credenciais no Console do Adobe Developer. Essas credenciais só precisam ser geradas uma vez e podem ser reutilizadas em chamadas futuras da API da plataforma.

### Adicionar Experience Platform a um projeto

Acesse o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criação de um projeto vazio](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) na documentação do Console do Adobe Developer.

Depois de criar um novo projeto, selecione **[!UICONTROL Adicionar API]** no **[!UICONTROL Visão geral do projeto]** tela.

![](./images/api-authentication/add-api.png)

A tela **[!UICONTROL Adicionar uma API]** é exibida. Selecione o ícone de produto do Adobe Experience Platform e escolha **[!UICONTROL API EXPERIENCE PLATFORM]** antes de selecionar **[!UICONTROL Próxima]**.

![](./images/api-authentication/platform-api.png)

A partir daqui, siga as etapas descritas no tutorial em [adicionar uma API a um projeto usando uma conta de serviço (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (começando na etapa &quot;Configurar API&quot;) para concluir o processo.

>[!IMPORTANT]
>
>Em uma determinada etapa durante o processo vinculado acima, seu navegador baixa automaticamente uma chave privada e um certificado público associado. Observe onde essa chave privada está armazenada em sua máquina, já que ela é necessária em uma etapa posterior deste tutorial.

### Coletar credenciais

Depois que a API for adicionada ao projeto, o **[!UICONTROL API EXPERIENCE PLATFORM]** A página do projeto exibe as seguintes credenciais que são necessárias em todas as chamadas para as APIs Experience Platform:

* `{API_KEY}` ([!UICONTROL ID do cliente])
* `{ORG_ID}` ([!UICONTROL ID da organização])

![](././images/api-authentication/api-key-ims-org.png)

Além das credenciais acima, você também precisará do script **[!UICONTROL Segredo do cliente]** para uma etapa futura. Selecionar **[!UICONTROL Recuperar segredo do cliente]** para revelar o valor e, em seguida, copie-o para uso posterior.

![](././images/api-authentication/client-secret.png)

## Gerar um JSON Web Token (JWT) {#jwt}

A próxima etapa é gerar um JSON Web Token (JWT) com base nas credenciais da conta. Esse valor é usado para gerar o `{ACCESS_TOKEN}` credencial para uso em chamadas de API da plataforma, que devem ser geradas novamente a cada 24 horas.

>[!IMPORTANT]
>
>Para os fins deste tutorial, as etapas abaixo descrevem como gerar um JWT no Console do desenvolvedor. No entanto, esse método de geração só deve ser usado para fins de teste e avaliação.
>
>Para uso regular, o JWT deve ser gerado automaticamente. Para obter mais informações sobre como gerar JWTs programaticamente, consulte [guia de autenticação da conta de serviço](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) no Adobe Developer.

Selecionar **[!UICONTROL Conta de serviço (JWT)]** na navegação à esquerda, selecione **[!UICONTROL Gerar JWT]**.

![](././images/api-authentication/generate-jwt.png)

Na caixa de texto fornecida em **[!UICONTROL Gerar JWT personalizado]**, cole o conteúdo da chave privada gerada anteriormente ao adicionar a API da plataforma à sua conta de serviço. Em seguida, selecione **[!UICONTROL Gerar token]**.

![](././images/api-authentication/paste-key.png)

A página é atualizada para mostrar o JWT gerado, juntamente com um comando cURL de amostra que permite gerar um token de acesso. Para os fins deste tutorial, selecione **[!UICONTROL Copiar]** ao lado de **[!UICONTROL JWT gerado]** para copiar o token para a área de transferência.

![](././images/api-authentication/copy-jwt.png)

## Gerar um token de acesso

Depois de gerar um JWT, você pode usá-lo em uma chamada de API para gerar `{ACCESS_TOKEN}`. Ao contrário dos valores de `{API_KEY}` e `{ORG_ID}`, um novo token deve ser gerado a cada 24 horas para continuar usando as APIs da plataforma.

**Solicitação**

A solicitação a seguir gera um novo `{ACCESS_TOKEN}` com base nas credenciais fornecidas na carga. Esse endpoint só aceita dados de formulário como sua carga, portanto, deve receber um `Content-Type` cabeçalho de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propriedade | Descrição |
| --- | --- |
| `{API_KEY}` | A variável `{API_KEY}` ([!UICONTROL ID do cliente]) que você recuperou em um [etapa anterior](#api-ims-secret). |
| `{SECRET}` | O segredo do cliente que você recuperou em um [etapa anterior](#api-ims-secret). |
| `{JWT}` | O JWT gerado em um [etapa anterior](#jwt). |

>[!NOTE]
>
>Você pode usar a mesma chave de API, segredo do cliente e JWT para gerar um novo token de acesso para cada sessão. Isso permite automatizar a geração de token de acesso em seus aplicativos.

**Resposta**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| Propriedade | Descrição |
| --- | --- |
| `token_type` | O tipo de token que está sendo retornado. Para tokens de acesso, esse valor sempre é `bearer`. |
| `access_token` | O gerado `{ACCESS_TOKEN}`. Este valor, com prefixo da palavra `Bearer`, é obrigatório como a `Authentication` para todas as chamadas de API da plataforma. |
| `expires_in` | O número de milissegundos restantes até que o token de acesso expire. Quando esse valor atingir 0, um novo token de acesso deverá ser gerado para continuar usando as APIs da plataforma. |

## Testar credenciais de acesso

Depois de coletar todas as três credenciais necessárias, você pode tentar fazer a seguinte chamada de API. Essa chamada lista todas as chamadas padrão [!DNL Experience Data Model] Classes do (XDM) disponíveis para sua organização.

**Solicitação**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Se sua resposta for semelhante à mostrada abaixo, suas credenciais serão válidas e estarão funcionando. (Esta resposta foi truncada por questões de espaço.)

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

## Usar o Postman para autenticar e testar chamadas de API

[Postman](https://www.postman.com/) O é uma ferramenta popular que permite aos desenvolvedores explorar e testar as APIs RESTful. Este [Postagem média](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descreve como você pode configurar o Postman para executar automaticamente a autenticação JWT e usá-la para consumir APIs da plataforma.

## Desenvolvedor e controle de acesso à API com permissões de Experience Platform

>[!NOTE]
>
>Somente administradores do sistema têm a capacidade de exibir e gerenciar credenciais de API nas Permissões.

Antes de criar integrações no Console do Adobe Developer, sua conta deve ter permissões de desenvolvedor e usuário para um perfil de produto do Experience Platform no Adobe Admin Console.

### Adicionar desenvolvedores ao perfil do produto

Acesse [[!DNL Admin Console]](https://adminconsole.adobe.com/) e faça logon com sua Adobe ID.

Selecionar **[!UICONTROL Produtos]** e selecione **[!UICONTROL Adobe Experience Platform]** da lista de produtos.

![Lista de produtos no Admin Console](././images/api-authentication/products.png)

No **[!UICONTROL Perfis de produto]** selecione **[!UICONTROL AEP-Padrão-Todos-Usuários]**. Como alternativa, use a barra de pesquisa para pesquisar o perfil de produto inserindo o nome.

![Pesquisar o perfil de produto](././images/api-authentication/select-product-profile.png)

Selecione o **[!UICONTROL Desenvolvedores]** e selecione **[!UICONTROL Adicionar desenvolvedor]**.

![Adicionar desenvolvedor na guia Desenvolvedores](././images/api-authentication/add-developer1.png)

Insira o nome do desenvolvedor **[!UICONTROL Email ou nome de usuário]**. Um válido [!UICONTROL Email ou nome de usuário] exibirá os detalhes do desenvolvedor. Selecione **[!UICONTROL Salvar]**.

![Adicionar desenvolvedor usando seu email ou nome de usuário](././images/api-authentication/add-developer-email.png)

O desenvolvedor foi adicionado com sucesso e aparece no [!UICONTROL Desenvolvedores] guia.

![Desenvolvedores listados na guia Desenvolvedores](././images/api-authentication/developer-added.png)

### Configurar uma API

Um desenvolvedor pode adicionar e configurar uma API em um projeto no Console do Adobe Developer.

Selecione seu projeto e, em seguida, **[!UICONTROL Adicionar API]**.

![Adicionar API a um projeto](././images/api-authentication/add-api-project.png)

No **[!UICONTROL Adicionar uma API]** caixa de diálogo selecionar **[!UICONTROL Adobe Experience Platform]** e selecione **[!UICONTROL API EXPERIENCE PLATFORM]**.

![Adicionar uma API no Experience Platform](././images/api-authentication/add-api-platform.png)

No **[!UICONTROL Configurar API]** , selecione **[!UICONTROL AEP-Padrão-Todos-Usuários]**.

### Atribuir API a uma função

Um administrador do sistema pode atribuir APIs a funções na interface do usuário do Experience Platform.

Selecionar **[!UICONTROL Permissões]** e a função à qual você deseja adicionar a API. Selecione o **[!UICONTROL Credenciais da API]** e selecione **[!UICONTROL Adicionar credenciais de API]**.

![Guia de credenciais de API na função selecionada](././images/api-authentication/api-credentials.png)

Selecione a API que deseja adicionar à função e selecione **[!UICONTROL Salvar]**.

![Lista de APIs disponíveis para seleção](././images/api-authentication/select-api.png)

Você retornará à janela [!UICONTROL Credenciais da API] , onde a API recém-adicionada é listada.

![Guia Credenciais da API com API recém-adicionada](././images/api-authentication/api-credentials-with-added-api.png)

## Próximas etapas

Ao ler este documento, você reuniu e testou com êxito suas credenciais de acesso para APIs da plataforma. Agora você pode seguir junto com as chamadas de API de exemplo fornecidas em [documentação](../landing/documentation/overview.md).

Além dos valores de autenticação coletados neste tutorial, muitas APIs da Platform também exigem uma `{SANDBOX_NAME}` a ser fornecido como um cabeçalho. Consulte a [visão geral das sandboxes](../sandboxes/home.md) para obter mais informações.