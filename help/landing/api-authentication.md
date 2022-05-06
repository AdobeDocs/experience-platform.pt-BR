---
keywords: Experience Platform, home, tópicos populares, Autenticar, acesso
solution: Experience Platform
title: Autenticar e acessar APIs do Experience Platform
topic-legacy: tutorial
type: Tutorial
description: Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor da Adobe Experience Platform para fazer chamadas para APIs da Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 9%

---


# Autenticar e acessar APIs da Experience Platform

Este documento fornece um tutorial passo a passo para obter acesso a uma conta de desenvolvedor da Adobe Experience Platform para fazer chamadas para APIs da Experience Platform. No final deste tutorial, você gerou as seguintes credenciais necessárias para todas as chamadas de API da plataforma:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

Para manter a segurança de seus aplicativos e usuários, todas as solicitações para APIs do Adobe I/O devem ser autenticadas e autorizadas usando padrões como OAuth e JSON Web Tokens (JWT). Um JWT é usado junto com informações específicas do cliente para gerar seu token de acesso pessoal.

Este tutorial aborda como coletar as credenciais necessárias para autenticar chamadas da API do Platform, conforme descrito no fluxograma a seguir:

![](./images/api-authentication/authentication-flowchart.png)

## Pré-requisitos

Para fazer chamadas com êxito para APIs do Experience Platform, você deve ter o seguinte:

* Uma Organização IMS com acesso à Adobe Experience Platform.
* Um administrador do Admin Console que pode adicioná-lo como desenvolvedor e como usuário para um perfil de produto.

Você também deve ter uma Adobe ID para concluir este tutorial. Se você não tiver uma Adobe ID, poderá criar uma usando as seguintes etapas:

1. Ir para [Console do desenvolvedor do Adobe](https://console.adobe.io).
2. Selecionar **[!UICONTROL Criar uma nova conta]**.
3. Conclua o processo de inscrição.

## Obter acesso de desenvolvedor e usuário para o Experience Platform

Antes de criar integrações no Console do desenvolvedor do Adobe, sua conta deve ter permissões de desenvolvedor e de usuário para um perfil de produto do Experience Platform no Adobe Admin Console.

### Obter acesso do desenvolvedor

Entre em contato com um [!DNL Admin Console] administrador em sua organização para adicioná-lo como desenvolvedor a um perfil de produto do Experience Platform usando o [[!DNL Admin Console]](https://adminconsole.adobe.com/). Consulte a [!DNL Admin Console] documentação para obter instruções específicas sobre como [gerenciar o acesso do desenvolvedor para perfis de produtos](https://helpx.adobe.com/br/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Depois de ser atribuído como um desenvolvedor, você pode começar a criar integrações no [Console do desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui). Essas integrações são um pipeline de aplicativos e serviços externos para APIs do Adobe.

### Obter acesso do usuário

Seu [!DNL Admin Console] O administrador também deve adicioná-lo como usuário ao mesmo perfil de produto. Consulte o guia sobre [gerenciamento de grupos de usuários no [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) para obter mais informações.

## Gerar uma chave de API, ID de organização IMS e segredo do cliente {#api-ims-secret}

>[!NOTE]
>
>Se você estiver seguindo este documento da [Guia da API do Privacy Service](../privacy-service/api/getting-started.md), agora você pode retornar a esse guia para gerar as credenciais de acesso exclusivas do [!DNL Privacy Service].

Depois de ter recebido acesso de desenvolvedor e usuário à Platform por meio de [!DNL Admin Console], a próxima etapa é gerar `{ORG_ID}` e `{API_KEY}` credenciais no Adobe Developer Console. Essas credenciais só precisam ser geradas uma vez e podem ser reutilizadas em chamadas futuras da API da plataforma.

### Adicionar Experience Platform a um projeto

Acesse o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criação de um projeto vazio](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) na documentação do Console do desenvolvedor do Adobe.

Depois de criar um novo projeto, selecione **[!UICONTROL Adicionar API]** no **[!UICONTROL Visão geral do projeto]** tela.

![](./images/api-authentication/add-api.png)

A tela **[!UICONTROL Adicionar uma API]** é exibida. Selecione o ícone do produto para Adobe Experience Platform e escolha **[!UICONTROL API Experience Platform]** antes de selecionar **[!UICONTROL Próximo]**.

![](./images/api-authentication/platform-api.png)

A partir daqui, siga as etapas descritas no tutorial em [adicionar uma API a um projeto usando uma conta de serviço (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (começando pela etapa &quot;Configurar API&quot;) para concluir o processo.

>[!IMPORTANT]
>
>Em uma determinada etapa durante o processo vinculado acima, o navegador baixa automaticamente uma chave privada e um certificado público associado. Observe onde essa chave privada é armazenada em sua máquina, já que é necessária em uma etapa posterior deste tutorial.

### Obter credenciais

Depois que a API for adicionada ao projeto, a variável **[!UICONTROL API Experience Platform]** para o projeto exibe as credenciais a seguir, que são necessárias em todas as chamadas para APIs do Experience Platform:

* `{API_KEY}` ([!UICONTROL ID do cliente])
* `{ORG_ID}` ([!UICONTROL ID da organização])

![](././images/api-authentication/api-key-ims-org.png)

Além das credenciais acima, você também precisa do **[!UICONTROL Segredo do cliente]** para uma etapa futura. Selecionar **[!UICONTROL Recuperar segredo do cliente]** para revelar o valor e, em seguida, copiá-lo para uso posterior.

![](././images/api-authentication/client-secret.png)

## Gerar um JSON Web Token (JWT) {#jwt}

A próxima etapa é gerar um JSON Web Token (JWT) com base em suas credenciais de conta. Esse valor é usado para gerar `{ACCESS_TOKEN}` credencial para uso em chamadas da API da plataforma, que devem ser geradas novamente a cada 24 horas.

>[!IMPORTANT]
>
>Para os fins deste tutorial, as etapas abaixo descrevem como gerar uma JWT no Console do desenvolvedor. No entanto, este método de geração só deve ser utilizado para fins de ensaio e avaliação.
>
>Para uso regular, o JWT deve ser gerado automaticamente. Para obter mais informações sobre como gerar JWTs programaticamente, consulte o [guia de autenticação da conta de serviço](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) no Adobe Developer.

Selecionar **[!UICONTROL Conta de serviço (JWT)]** na navegação à esquerda, selecione **[!UICONTROL Gerar JWT]**.

![](././images/api-authentication/generate-jwt.png)

Na caixa de texto fornecida em **[!UICONTROL Gerar JWT personalizado]**, cole o conteúdo da chave privada gerada anteriormente ao adicionar a API da plataforma à conta de serviço. Em seguida, selecione **[!UICONTROL Gerar token]**.

![](././images/api-authentication/paste-key.png)

A página é atualizada para mostrar o JWT gerado, juntamente com um comando cURL de amostra que permite gerar um token de acesso. Para fins deste tutorial, selecione **[!UICONTROL Copiar]** ao lado de **[!UICONTROL JWT gerado]** para copiar o token para a área de transferência.

![](././images/api-authentication/copy-jwt.png)

## Gerar um token de acesso

Depois de gerar uma JWT, você pode usá-la em uma chamada de API para gerar `{ACCESS_TOKEN}`. Diferente dos valores de `{API_KEY}` e `{ORG_ID}`, um novo token deve ser gerado a cada 24 horas para continuar usando as APIs da plataforma.

**Solicitação**

A solicitação a seguir gera um novo `{ACCESS_TOKEN}` com base nas credenciais fornecidas no payload. Esse ponto de extremidade aceita apenas dados de formulário como sua carga, e portanto deve receber uma `Content-Type` cabeçalho de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propriedade | Descrição |
| --- | --- |
| `{API_KEY}` | O `{API_KEY}` ([!UICONTROL ID do cliente]) que você recuperou em um [etapa anterior](#api-ims-secret). |
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
| `token_type` | O tipo de token que está sendo retornado. Para tokens de acesso, esse valor é sempre `bearer`. |
| `access_token` | O `{ACCESS_TOKEN}`. Esse valor, com o prefixo da palavra `Bearer`, é obrigatório como `Authentication` para todas as chamadas de API do Platform. |
| `expires_in` | O número de milissegundos restantes até o token de acesso expirar. Quando esse valor atingir 0, um novo token de acesso deverá ser gerado para continuar usando as APIs da plataforma. |

## Testar credenciais de acesso

Depois de reunir todas as três credenciais necessárias, tente fazer a seguinte chamada de API. Esta chamada lista todos os padrões [!DNL Experience Data Model] (XDM) classes disponíveis para sua organização.

**Solicitação**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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

## Use o Postman para autenticar e testar chamadas da API

[Postman](https://www.postman.com/) O é uma ferramenta popular que permite aos desenvolvedores explorar e testar RESTful APIs. Essa [Postagem média](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descreve como você pode configurar o Postman para realizar automaticamente a autenticação JWT e usá-la para consumir APIs da plataforma.

## Próximas etapas

Ao ler este documento, você reuniu e testou com êxito suas credenciais de acesso para APIs da plataforma. Agora você pode seguir com o exemplo de chamadas de API fornecidas durante a [documentação](../landing/documentation/overview.md).

Além dos valores de autenticação coletados neste tutorial, muitas APIs da plataforma também exigem um `{SANDBOX_NAME}` a ser fornecido como um cabeçalho. Consulte a [visão geral das sandboxes](../sandboxes/home.md) para obter mais informações.