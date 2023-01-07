---
title: Introdução à API do Privacy Service
description: Saiba como autenticar na API do Privacy Service e interpretar chamadas de API de exemplo na documentação.
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 10%

---

# Introdução à API do Privacy Service

Este guia fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Adobe Experience Platform Privacy Service.

## Pré-requisitos

Este guia requer um entendimento prático de [Privacy Service](../home.md) e como ele permite gerenciar solicitações de acesso e exclusão de seus titulares de dados (clientes) em todos os aplicativos Adobe Experience Cloud.

Para criar credenciais de acesso para a API, um administrador em sua organização deve ter configurado previamente os perfis de produto para o Privacy Service no Adobe Admin Console. O perfil de produto atribuído a uma integração de API determina quais permissões a integração tem ao acessar recursos do Privacy Service. Consulte o guia sobre [gerenciamento de permissões do Privacy Service](../permissions.md) para obter mais informações.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para a API do Privacy Service, primeiro você deve coletar suas credenciais de acesso para serem usadas nos cabeçalhos necessários:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Esses valores são gerados usando [Console do Adobe Developer](https://developer.adobe.com/console). Seu `{ORG_ID}` e `{API_KEY}` só precisam ser geradas uma vez e podem ser reutilizadas em chamadas de API futuras. No entanto, a variável `{ACCESS_TOKEN}` é temporária e deve ser regenerada a cada 24 horas.

As etapas de geração desses valores são descritas em detalhes abaixo.

### Configuração única

Acesse o [Adobe Developer Console](https://developer.adobe.com/console) e faça logon com seu Adobe ID. Depois, siga as etapas descritas no tutorial sobre como [criar um projeto vazio](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) na documentação do Developer Console.

Depois de criar um novo projeto, selecione **[!UICONTROL Adicionar ao projeto]** e escolha **[!UICONTROL API]** no menu suspenso.

![A opção API que está sendo selecionada na [!UICONTROL Adicionar ao projeto] lista suspensa da página de detalhes do projeto no Console do desenvolvedor](../images/api/getting-started/add-api-button.png)

#### Selecione uma API e gere um par de chaves {#keypair}

A tela **[!UICONTROL Adicionar uma API]** é exibida. Selecionar **[!UICONTROL Experience Cloud]** para restringir a lista de APIs disponíveis, selecione o cartão para **[!UICONTROL API Privacy Service]** antes de selecionar **[!UICONTROL Próximo]**.

![O cartão Privacy Service API que está sendo selecionado na lista de APIs disponíveis](../images/api/getting-started/add-privacy-service-api.png)

O **[!UICONTROL Configurar API]** será exibida. Selecione a opção para **[!UICONTROL Gerar um par de chaves]**, em seguida selecione **[!UICONTROL Gerar par de chaves]**.

![O [!UICONTROL Gerar um par de chaves] opção selecionada na [!UICONTROL Configurar API] tela](../images/api/getting-started/generate-key-pair.png)

O par de chaves é gerado automaticamente e um arquivo ZIP contendo uma chave privada e um certificado público é baixado pelo navegador (para ser usado em uma etapa posterior). Clique em **[!UICONTROL Avançar]** para continuar.

![O par de chaves gerado mostrado na interface do usuário, cujos valores são baixados automaticamente pelo navegador](../images/api/getting-started/key-pair-generated.png)

#### Atribuir permissões por meio de perfis de produto {#product-profiles}

A etapa final da configuração é selecionar os perfis de produto dos quais essa integração herdará as permissões. Se você selecionar mais de um perfil, seus conjuntos de permissões serão combinados para a integração.

>[!NOTE]
>
>Os perfis de produto e as permissões granulares fornecidas são criados e gerenciados pelos administradores por meio do Adobe Admin Console. Consulte o guia sobre [Permissões para Privacy Service](../permissions.md) para obter mais informações.

Quando terminar, selecione **[!UICONTROL Salvar API configurada]**.

![Um único perfil de produto sendo selecionado na lista antes de salvar a configuração](../images/api/getting-started/select-product-profiles.png)

Depois que a API for adicionada ao projeto, a página do projeto será exibida novamente no **Visão geral da API do Privacy Service** página. A partir daqui, role para baixo até o **[!UICONTROL Conta de serviço (JWT)]** seção , que fornece as seguintes credenciais de acesso que são necessárias em todas as chamadas para a API do Privacy Service:

* **[!UICONTROL ID DO CLIENTE]**: A ID do cliente é a `{API_KEY}` que deve ser previsto no `x-api-key` cabeçalho.
* **[!UICONTROL ID DA ORGANIZAÇÃO]**: a ID da organização é o valor `{ORG_ID}` que deve ser usado no cabeçalho `x-gw-ims-org-id`.

![Os valores da ID do cliente e da ID da organização , conforme aparecem na página de visão geral do projeto depois que a API é configurada](../images/api/getting-started/jwt-credentials.png)

### Autenticação para cada sessão

A credencial final necessária que você deve coletar é a `{ACCESS_TOKEN}`, que é usada no cabeçalho da Autorização. Diferente dos valores de `{API_KEY}` e `{ORG_ID}`, um novo token deve ser gerado a cada 24 horas para continuar usando a API.

Em geral, há dois métodos de geração de um token de acesso:

* [Gerar o token manualmente](#manual-token) para testes e desenvolvimento.
* [Automatizar a geração de tokens](#auto-token) para integrações de API.

#### Gerar um token manualmente {#manual-token}

Para gerar manualmente um novo `{ACCESS_TOKEN}`, abra a chave privada baixada anteriormente e cole seu conteúdo na caixa de texto ao lado de **[!UICONTROL Gerar token de acesso]** antes de selecionar **[!UICONTROL Gerar token]**.

![O token de acesso gerado anteriormente sendo colado na página de visão geral do projeto, com a variável [!UICONTROL Gerar token] botão que será selecionado depois de](../images/api/getting-started/paste-private-key.png)

É gerado um novo token de acesso, e é fornecido um botão para copiá-lo para a área de transferência. Esse valor é usado para o cabeçalho de Autorização necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`.

![O token de acesso gerado que está sendo copiado da interface do usuário](../images/api/getting-started/generated-access-token.png)

#### Automatizar a geração de tokens {#auto-token}

Você pode gerar novos tokens de acesso para processos automatizados enviando um JSON Web Token (JWT) por meio de uma solicitação POST para o Adobe Identity Management Service (IMS). Consulte o documento do Console do desenvolvedor em [Autenticação JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) para obter etapas detalhadas.

## Lendo exemplos de chamadas de API

Cada guia de endpoint fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/api-guide.md#sample-api) no guia de introdução para APIs da plataforma.

## Próximas etapas

Agora que você sabe quais cabeçalhos usar, está pronto para começar a fazer chamadas para a API do Privacy Service. Selecione um dos guias de ponto de extremidade para começar:

* [Trabalhos de privacidade](./privacy-jobs.md)
* [Consentimento](./consent.md)
