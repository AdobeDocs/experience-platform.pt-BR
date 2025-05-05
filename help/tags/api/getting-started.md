---
title: Autenticar e acessar a API do Reator
description: Saiba como começar a usar a API do Reactor, incluindo etapas para gerar as credenciais de acesso necessárias.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 47%

---

# Autenticar e acessar a API do Reator

Para usar a [API do Reator](https://developer.adobe.com/experience-platform-apis/references/reactor/) para criar e gerenciar extensões de Tags, cada solicitação deve incluir os seguintes cabeçalhos de autenticação:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Este guia mostra como usar o Adobe Developer Console a fim de coletar os valores de cada um desses cabeçalhos para que você possa começar a fazer chamadas à API do reator.

## Obter acesso de desenvolvedor à Adobe Experience Platform {#gain-developer-access}

A fim de gerar valores de autenticação para a API do reator, você deve ter acesso de desenvolvedor à Experience Platform. Para obter acesso de desenvolvedor, siga as etapas iniciais no [tutorial de autenticação da Experience Platform](/help/landing/api-authentication.md). Depois de concluir a etapa [Obter acesso do usuário](/help/landing/api-authentication.md#gain-user-access), retorne a este tutorial para gerar as credenciais específicas da API do Reator.

## Gerar credenciais de acesso {#generate-access-credentials}

Usando o Adobe Developer Console, você deve gerar as três credenciais de acesso descritas a seguir:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

A ID (`{ORG_ID}`) e a chave de API (`{API_KEY}`) da sua organização podem ser reutilizadas em chamadas de API futuras depois de terem sido geradas. No entanto, seu token de acesso (`{ACCESS_TOKEN}`) é temporário e deve ser gerado novamente a cada 24 horas.

As etapas de geração desses valores são descritas em detalhes abaixo.

### Configuração única {#one-time-setup}

Acesse o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Depois, siga as etapas descritas no tutorial sobre como [criar um projeto vazio](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) na documentação do Developer Console.

Depois de criar um projeto, selecione **Adicionar API** na tela **Visão geral do projeto**.

![](../images/api/getting-started/add-api-button.png)

A tela **Adicionar uma API** é exibida. Selecione **API do Experience Platform Launch** na lista de APIs disponíveis antes de selecionar **Avançar**.

![](../images/api/getting-started/add-launch-api.png)

Em seguida, selecione o tipo de autenticação para gerar tokens de acesso e acessar a API do Experience Platform.

>[!IMPORTANT]
>
>Selecione o método **[!UICONTROL OAuth Server-to-Server]**, pois esse será o único método com suporte no futuro. O método **[!UICONTROL Conta de Serviço (JWT)]** está obsoleto. Embora as integrações que usam o método de autenticação JWT continuem a funcionar até 1º de janeiro de 2025, a Adobe recomenda que você migre as integrações existentes para o novo método servidor para servidor OAuth antes dessa data. Obtenha mais informações na seção [!BADGE Obsoleto]{type=negative}[Gere um JSON Web Token (JWT)](/help/landing/api-authentication.md#jwt) no tutorial de autenticação da API do Experience Platform.

Clique em **Avançar** para continuar.

![Selecione o método de autenticação OAuth de servidor para servidor.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

A próxima tela solicita que você selecione um ou mais perfis de produto para associar à integração com a API.

>[!NOTE]
>
>Os perfis de produto são gerenciados por sua organização por meio da Adobe Admin Console e contêm conjuntos específicos de permissões para recursos granulares. Os perfis de produto e suas permissões só podem ser gerenciados por usuários com privilégios de administrador na organização. Se não tiver certeza sobre quais perfis de produto deve selecionar para a API, entre em contato com o administrador.

Selecione os perfis de produto desejados na lista e selecione **Salvar API configurada** para concluir o registro da API.

![](../images/api/getting-started/select-product-profile.png)

### Coletar credenciais {#gather-credentials}

Depois que a API for adicionada ao projeto, a página **[!UICONTROL API Experience Platform]** do projeto exibirá as seguintes credenciais, necessárias em todas as chamadas para as APIs Experience Platform:

* `{API_KEY}` ([!UICONTROL ID do Cliente])
* `{ORG_ID}` ([!UICONTROL ID da Organização])

![Informações de integração após adicionar uma API no Developer Console.](/help/tags/images/api/getting-started/api-integration-information.png)

### Gerar um token de acesso {#generate-access-token}

A próxima etapa é gerar uma credencial `{ACCESS_TOKEN}` para uso em chamadas de API do Experience Platform. Diferentemente dos valores de `{API_KEY}` e `{ORG_ID}`, um novo token deve ser gerado a cada 24 horas para continuar usando as APIs do Experience Platform.

>[!TIP]
>
>Esses tokens expiram após 24 horas. Se você está usando essa integração para um aplicativo, convém obter o token de portador de forma programática por meio do aplicativo.

Você tem duas opções para gerar os tokens de acesso, dependendo do caso de uso:

* [Gerar tokens manualmente](#manual)
* [Geração de token automatizada](#auto-token)

#### Gerar tokens de acesso manualmente {#manual}

Para gerar manualmente um novo `{ACCESS_TOKEN}`, navegue até **[!UICONTROL Credenciais]** > **[!UICONTROL Servidor para servidor OAuth]** e selecione **[!UICONTROL Gerar token de acesso]**, conforme mostrado abaixo.

![Gravação de tela de como e o token de acesso são gerados na interface do usuário do Developer Console.](/help/tags/images/api/getting-started/generate-access-token.gif)

É gerado um novo token de acesso, e é fornecido um botão para copiá-lo para a área de transferência. Este valor é usado para o cabeçalho de Autorização necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`.

#### Geração de token automatizada {#auto-token}

Você também pode usar um ambiente e uma coleção do Postman para gerar tokens de acesso. Para obter mais informações, leia a seção sobre [como usar o Postman para autenticar e testar chamadas de API](/help/landing/api-authentication.md#use-postman) no guia de autenticação da API do Experience Platform.

## Credenciais da API de teste {#test-api-credentials}

Seguindo as etapas deste tutorial, você deve ter valores válidos para `{ORG_ID}`, `{API_KEY}` e `{ACCESS_TOKEN}`. Agora é possível testar esses valores usando-os em uma solicitação de cURL simples para a API do Reactor.

Para começar, tente fazer uma chamada de API para [listar todas as empresas](./endpoints/companies.md#list).

>[!NOTE]
>
>Talvez você não tenha empresas em sua organização. Nesse caso, a resposta será o status HTTP 404 (Não encontrado). Desde que você não receba um erro 403 (Proibido), suas credenciais de acesso são válidas e estão funcionando.

Depois de confirmar que suas credenciais de acesso estão funcionando, continue explorando a outra documentação de referência da API para saber mais sobre os vários recursos da API.

## Leitura de chamadas de API de amostra {#read-sample-api-calls}

Cada manual de endpoint fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/api-guide.md#sample-api) no guia de introdução para APIs do Experience Platform.

## Próximas etapas {#next-steps}

Agora que você entende quais cabeçalhos usar, você está pronto para começar a fazer chamadas para a API do Reator. Selecione um dos manuais de endpoint para começar:

* [Documentação de referência da API do Reator](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Visão geral do guia da API do Reator](/help/tags/api/overview.md)
