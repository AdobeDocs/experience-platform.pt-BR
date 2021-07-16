---
title: Introdução à API do reator
description: Saiba como começar a usar a API do Reator, incluindo etapas para gerar as credenciais de acesso necessárias.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 1%

---

# Introdução à API do reator

Para usar a [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml), cada solicitação deve incluir os seguintes cabeçalhos de autenticação:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Este guia aborda como usar o Console do desenvolvedor do Adobe para coletar os valores de cada um desses cabeçalhos para que você possa começar a fazer chamadas para a API do reator.

## Obter acesso do desenvolvedor ao Adobe Experience Platform

Antes de gerar valores de autenticação para a API do Reator, você deve ter acesso de desenvolvedor ao Experience Platform. Para obter acesso de desenvolvedor, siga as etapas iniciais no [tutorial de autenticação do Experience Platform](http://www.adobe.com/go/platform-api-authentication-en). Depois de chegar à etapa &quot;Gerar credenciais de acesso no Console do Desenvolvedor do Adobe&quot;, retorne a este tutorial para gerar as credenciais específicas da API do Reator.

## Gerar credenciais de acesso

Usando o Console do Desenvolvedor do Adobe, você deve gerar as três credenciais de acesso a seguir:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

A ID da organização IMS (`{IMS_ORG}`) e a chave da API (`{API_KEY}`) podem ser reutilizadas em chamadas de API futuras depois de terem sido geradas inicialmente. No entanto, seu token de acesso (`{ACCESS_TOKEN}`) é temporário e deve ser gerado novamente a cada 24 horas.

As etapas para gerar esses valores são abordadas detalhadamente abaixo.

### Configuração única

Vá para [Console do desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui) e faça logon com sua Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criar um projeto vazio](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) na documentação do Console do desenvolvedor.

Depois de criar um projeto, selecione **Adicionar API** na tela **Visão geral do projeto**.

![](../images/api/getting-started/add-api-button.png)

A tela **Adicionar uma API** é exibida. Selecione **Experience Platform Reator API** na lista de APIs disponíveis antes de selecionar **Next**.

![](../images/api/getting-started/add-launch-api.png)

Na próxima tela, você será solicitado a criar uma credencial JSON Web Token (JWT) para gerar um novo par de chaves ou fazer upload de sua própria chave pública. Para este tutorial, selecione a opção **Generate a key pair** e selecione **Generate keypair** no canto inferior direito.

![](../images/api/getting-started/create-jwt.png)

A próxima tela confirma que o par de chaves foi gerado com êxito e uma pasta compactada contendo um certificado público e uma chave privada é baixada automaticamente no computador. Essa chave privada é necessária em uma etapa posterior para gerar um token de acesso.

Selecione **Next** para continuar.

![](../images/api/getting-started/keypair-generated.png)

A próxima tela solicita que você selecione um ou mais perfis de produto para associar à integração com a API.

>[!NOTE]
>
>Os perfis de produto são gerenciados por sua organização por meio da Adobe Admin Console e contêm conjuntos específicos de permissões para recursos granulares no Adobe Experience Platform Launch. Os perfis de produto e suas permissões só podem ser gerenciados por usuários com privilégios de administrador na organização. Se não tiver certeza sobre quais perfis de produto selecionar para a API, entre em contato com o administrador.

Selecione os perfis de produto desejados na lista e selecione **Salvar API configurada** para concluir o registro da API.

![](../images/api/getting-started/select-product-profile.png)

Depois que a API for adicionada ao projeto, a página do projeto será exibida novamente na página da API do Reator do Experience Platform. A partir daqui, role para baixo até a seção **Conta de Serviço (JWT)** , que fornece as seguintes credenciais de acesso que são necessárias em todas as chamadas para a API do Reator:

* **ID** DO CLIENTE: A ID do cliente é a ID necessária,  `{API_KEY}` que deve ser fornecida no  `x-api-key` cabeçalho.
* **ID** DA ORGANIZAÇÃO: A ID da organização é o  `{IMS_ORG}` valor que deve ser usado no  `x-gw-ims-org-id` cabeçalho.

![](../images/api/getting-started/access-creds.png)

### Autenticação para cada sessão

Agora que você tem seus valores `{API_KEY}` e `{IMS_ORG}`, a etapa final está gerando um valor `{ACCESS_TOKEN}`.

>[!NOTE]
>
>Esses tokens expiram após 24 horas. Se você estiver usando essa integração para um aplicativo, é uma boa ideia obter o token do portador de forma programática de dentro do aplicativo.

Você tem duas opções para gerar seus tokens de acesso, dependendo do seu caso de uso:

* [Gerar tokens manualmente](#manual)
* [Gerar tokens programaticamente](#program)

#### Gerar tokens de acesso manualmente {#manual}

Abra a chave privada baixada anteriormente em um editor de texto ou navegador e copie seu conteúdo. Em seguida, volte para o Console do desenvolvedor e cole a chave privada na seção **Generate access token** na página API do reator para seu projeto antes de selecionar **Generate Token**.

![](../images/api/getting-started/paste-private-key.png)

Um novo token de acesso é gerado e um botão para copiar o token para a área de transferência é fornecido. Esse valor é usado para o cabeçalho `Authorization` necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/token-generated.png)

#### Gerar tokens de acesso programaticamente {#program}

Se estiver usando a integração do Launch para um aplicativo, você poderá gerar tokens de acesso de forma programática por meio de solicitações de API. Para fazer isso, você deve obter os seguintes valores:

* ID do cliente (`{API_KEY}`)
* Segredo do cliente (`{SECRET}`)
* Um token Web JSON (`{JWT}`)

A ID do cliente e o segredo podem ser obtidos na página principal do seu projeto, conforme visto na [etapa anterior](#one-time-setup).

![](../images/api/getting-started/auto-access-creds.png)

Para obter sua credencial JWT, navegue até **Conta de serviço (JWT)** na navegação à esquerda e selecione a guia **Gerar JWT**. Nesta página, em **Generate custom JWT**, cole o conteúdo da sua chave privada na caixa de texto fornecida e selecione **Generate Token**.

![](../images/api/getting-started/generate-jwt.png)

O JWT gerado aparece abaixo quando ele terminar o processamento, juntamente com um comando cURL de amostra que você pode usar para testar o token, se desejar. Use o botão **Copiar** para copiar o token para a área de transferência.

![](../images/api/getting-started/jwt-generated.png)

Depois de reunir suas credenciais, você pode integrar a chamada da API abaixo em seu aplicativo para gerar tokens de acesso de forma programática.

**Solicitação**

A solicitação deve enviar uma carga `multipart/form-data`, fornecendo suas credenciais de autenticação, conforme mostrado abaixo:

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**Resposta**

Uma resposta bem-sucedida retorna um novo token de acesso, bem como o número de segundos restantes até sua expiração.

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| Propriedade | Descrição |
| :-- | :-- |
| `access_token` | O valor do token de acesso recém-gerado. Esse valor é usado para o cabeçalho `Authorization` necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`. |
| `expires_in` | O tempo restante até o token expirar, em milissegundos. Depois que um token expira, um novo deve ser gerado. |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Ao seguir as etapas deste tutorial, você deve ter um valor válido para `{IMS_ORG}`, `{API_KEY}` e `{ACCESS_TOKEN}`. Agora é possível testar esses valores usando-os em uma simples solicitação de cURL para a API do reator.

Comece tentando fazer uma chamada de API para [listar todas as empresas](./endpoints/companies.md#list).

>[!NOTE]
>
>Você pode não ter empresas em sua organização, nesse caso, a resposta será o status HTTP 404 (Não encontrado). Desde que não receba um erro 403 (Proibido), suas credenciais de acesso são válidas e estão funcionando.

Depois de confirmar que suas credenciais de acesso estão funcionando, continue explorando a outra documentação de referência da API para saber mais sobre os vários recursos da API.

## Recursos adicionais

Bibliotecas JWT e SDKs: [https://jwt.io/](https://jwt.io/)

Desenvolvimento da API Postman: [https://www.postman.com/](https://www.postman.com/)
