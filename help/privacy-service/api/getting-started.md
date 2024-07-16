---
title: Autentique e acesse a API do Privacy Service
description: Saiba como autenticar para a API de Privacy Service e como interpretar chamadas de API de exemplo na documentação.
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 15%

---

# Autentique e acesse a API do Privacy Service

Este guia fornece uma introdução aos conceitos principais que você deve conhecer antes de tentar fazer chamadas para a API do Adobe Experience Platform Privacy Service.

## Pré-requisitos {#prerequisites}

Este guia requer entendimento prático do [Privacy Service](../home.md) e como ele permite gerenciar o acesso e excluir solicitações de titulares de dados (clientes) nos aplicativos da Adobe Experience Cloud.

Para criar credenciais de acesso para a API, um administrador em sua organização deve ter configurado previamente perfis de produto para o Privacy Service no Adobe Admin Console. O perfil de produto atribuído a uma integração de API determina as permissões dessa integração ao acessar recursos de Privacy Service. Consulte o manual sobre [gerenciamento de permissões de Privacy Service](../permissions.md) para obter mais informações.

## Coletar valores para cabeçalhos necessários {#gather-values-required-headers}

Para fazer chamadas para a API Privacy Service, primeiro colete suas credenciais de acesso para serem usadas nos cabeçalhos necessários:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Estes valores são gerados usando o [Adobe Developer Console](https://developer.adobe.com/console). Seus `{ORG_ID}` e `{API_KEY}` só precisam ser gerados uma vez e podem ser reutilizados em chamadas de API futuras. No entanto, seu `{ACCESS_TOKEN}` é temporário e deve ser gerado novamente a cada 24 horas.

As etapas de geração desses valores são descritas em detalhes abaixo.

### Configuração única {#one-time-setup}

Acesse o [Adobe Developer Console](https://developer.adobe.com/console) e faça logon com seu Adobe ID. Depois, siga as etapas descritas no tutorial sobre como [criar um projeto vazio](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) na documentação do Developer Console.

Depois de criar um novo projeto, selecione **[!UICONTROL Adicionar ao projeto]** e escolha **[!UICONTROL API]** no menu suspenso.

![A opção de API sendo selecionada na lista suspensa [!UICONTROL Adicionar ao Projeto] da página de detalhes do projeto no Developer Console](../images/api/getting-started/add-api-button.png)

#### Selecione a API de Privacy Service {#select-privacy-service-api}

A tela **[!UICONTROL Adicionar uma API]** é exibida. Selecione **[!UICONTROL Experience Cloud]** para restringir a lista de APIs disponíveis e, em seguida, selecione o cartão para **[!UICONTROL APIs de Privacy Service]** antes de selecionar **[!UICONTROL Avançar]**.

![O cartão de API Privacy Service sendo selecionado da lista de APIs disponíveis](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>Selecione a opção **[!UICONTROL Exibir documentos]** para navegar em uma janela de navegador separada para a [documentação de referência da API de Privacy Service](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) completa.

Em seguida, selecione o tipo de autenticação para gerar tokens de acesso e acessar a API Privacy Service.

>[!IMPORTANT]
>
>Selecione o método **[!UICONTROL OAuth Server-to-Server]**, pois esse será o único método com suporte no futuro. O método **[!UICONTROL Conta de Serviço (JWT)]** está obsoleto. Embora as integrações que usam o método de autenticação JWT continuem a funcionar até 1º de janeiro de 2025, a Adobe recomenda que você migre as integrações existentes para o novo método servidor para servidor OAuth antes dessa data. Obtenha mais informações na seção [!BADGE Obsoleto]{type=negative}[Gerar um JSON Web Token (JWT)](/help/landing/api-authentication.md#jwt).

![Selecione o método de autenticação Oauth de servidor para servidor.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### Atribuir permissões por meio de perfis de produto {#product-profiles}

A etapa final de configuração é selecionar os perfis de produto dos quais essa integração herdará as permissões. Se você selecionar mais de um perfil, os conjuntos de permissões serão combinados para a integração.

>[!NOTE]
>
Os perfis de produto e as permissões granulares que fornecem são criados e gerenciados por administradores por meio do Adobe Admin Console. Consulte o manual sobre [permissões de Privacy Service](../permissions.md) para obter mais informações.

Quando terminar, selecione **[!UICONTROL Salvar API configurada]**.

![Um único perfil de produto sendo selecionado na lista antes de salvar a configuração](../images/api/getting-started/select-product-profiles.png)

Depois que a API for adicionada ao projeto, a página **[!UICONTROL APIs de Privacy Service]** do projeto exibirá as seguintes credenciais, necessárias em todas as chamadas para APIs de Privacy Service:

* `{API_KEY}` ([!UICONTROL ID do Cliente])
* `{ORG_ID}` ([!UICONTROL ID da Organização])

![Informações de integração após adicionar uma API no Developer Console.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### Autenticação para cada sessão {#authentication-each-session}

A credencial final necessária que você deve coletar é a `{ACCESS_TOKEN}`, que é usada no cabeçalho de Autorização. Diferentemente dos valores de `{API_KEY}` e `{ORG_ID}`, um novo token deve ser gerado a cada 24 horas para continuar usando a API.

Em geral, há dois métodos de geração de um token de acesso:

* [Gerar o token manualmente](#manual-token) para teste e desenvolvimento.
* [Automatize a geração de token](#auto-token) para integrações de API.

#### Gerar um token manualmente {#manual-token}

Para gerar manualmente um novo `{ACCESS_TOKEN}`, navegue até **[!UICONTROL Credenciais]** > **[!UICONTROL Servidor para servidor OAuth]** e selecione **[!UICONTROL Gerar token de acesso]**, conforme mostrado abaixo.

![Uma gravação de tela sobre como um token de acesso é gerado na interface do usuário do Developer Console.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

É gerado um novo token de acesso, e é fornecido um botão para copiá-lo para a área de transferência. Esse valor é usado para o cabeçalho [!DNL Authorization] necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`.

#### Geração de token automatizada {#auto-token}

Você também pode usar um ambiente e uma coleção do Postman para gerar tokens de acesso. Para obter mais informações, leia a seção sobre [como usar o Postman para autenticar e testar chamadas de API](/help/landing/api-authentication.md#use-postman) no guia de autenticação de API Experience Platform.

## Leitura de chamadas de API de amostra {#read-sample-api-calls}

Cada manual de endpoint fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/api-guide.md#sample-api) no guia de introdução para APIs da plataforma.

## Próximas etapas {#next-steps}

Agora que você entende quais cabeçalhos usar, você está pronto para começar a fazer chamadas para a API Privacy Service. Selecione um dos manuais de endpoint para começar:

* [Processos de privacidade](./privacy-jobs.md)
* [Consentimento](./consent.md)
