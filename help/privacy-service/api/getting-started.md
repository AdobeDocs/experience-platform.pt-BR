---
title: Introdução à API Privacy Service
description: Saiba como autenticar para a API de Privacy Service e como interpretar chamadas de API de exemplo na documentação.
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 10%

---

# Introdução à API Privacy Service

Este guia fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Adobe Experience Platform Privacy Service.

## Pré-requisitos

Este guia requer uma compreensão funcional de [Privacy Service](../home.md) e como ele permite gerenciar o acesso e excluir solicitações de titulares de dados (clientes) nos aplicativos da Adobe Experience Cloud.

Para criar credenciais de acesso para a API, um administrador em sua organização deve ter configurado previamente perfis de produto para o Privacy Service no Adobe Admin Console. O perfil de produto atribuído a uma integração de API determina as permissões dessa integração ao acessar recursos de Privacy Service. Consulte o guia sobre [gerenciamento de permissões de Privacy Service](../permissions.md) para obter mais informações.

## Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para a API Privacy Service, primeiro colete suas credenciais de acesso para serem usadas nos cabeçalhos necessários:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Esses valores são gerados usando [Console do Adobe Developer](https://developer.adobe.com/console). Seu `{ORG_ID}` e `{API_KEY}` só precisam ser geradas uma vez e podem ser reutilizadas em chamadas de API futuras. No entanto, seu `{ACCESS_TOKEN}` é temporário e deve ser gerado novamente a cada 24 horas.

As etapas de geração desses valores são descritas em detalhes abaixo.

### Configuração única

Acesse o [Adobe Developer Console](https://developer.adobe.com/console) e faça logon com seu Adobe ID. Depois, siga as etapas descritas no tutorial sobre como [criar um projeto vazio](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) na documentação do Developer Console.

Depois de criar um novo projeto, selecione **[!UICONTROL Adicionar ao projeto]** e escolha **[!UICONTROL API]** no menu suspenso.

![A opção da API que está sendo selecionada no [!UICONTROL Adicionar ao projeto] na página de detalhes do projeto no Console do desenvolvedor](../images/api/getting-started/add-api-button.png)

#### Selecionar uma API e gerar um par de chaves {#keypair}

A tela **[!UICONTROL Adicionar uma API]** é exibida. Selecionar **[!UICONTROL Experience Cloud]** para restringir a lista de APIs disponíveis, selecione o cartão para **[!UICONTROL API PRIVACY SERVICE]** antes de selecionar **[!UICONTROL Próxima]**.

![O cartão da API Privacy Service sendo selecionado na lista de APIs disponíveis](../images/api/getting-started/add-privacy-service-api.png)

A variável **[!UICONTROL Configurar API]** é exibida. Selecione a opção para **[!UICONTROL Gerar um par de chaves]** e selecione **[!UICONTROL Gerar par de chaves]**.

![A variável [!UICONTROL Gerar um par de chaves] opção selecionada na variável [!UICONTROL Configurar API] tela](../images/api/getting-started/generate-key-pair.png)

O par de chaves é gerado automaticamente e um arquivo ZIP contendo uma chave privada e um certificado público é baixado pelo navegador (para ser usado em uma etapa posterior). Clique em **[!UICONTROL Avançar]** para continuar.

![O par de chaves gerado mostrado na interface do usuário, cujos valores são baixados automaticamente pelo navegador](../images/api/getting-started/key-pair-generated.png)

#### Atribuir permissões por meio de perfis de produto {#product-profiles}

A etapa final de configuração é selecionar os perfis de produto dos quais essa integração herdará as permissões. Se você selecionar mais de um perfil, os conjuntos de permissões serão combinados para a integração.

>[!NOTE]
>
>Os perfis de produto e as permissões granulares que fornecem são criados e gerenciados por administradores por meio do Adobe Admin Console. Consulte o guia sobre [permissões de Privacy Service](../permissions.md) para obter mais informações.

Quando terminar, selecione **[!UICONTROL Salvar API configurada]**.

![Um único perfil de produto sendo selecionado na lista antes de salvar a configuração](../images/api/getting-started/select-product-profiles.png)

Depois que a API for adicionada ao projeto, a página do projeto reaparecerá no **Visão geral da API Privacy Service** página. A partir daqui, role para baixo até a **[!UICONTROL Conta de serviço (JWT)]** , que fornece as seguintes credenciais de acesso necessárias em todas as chamadas à API Privacy Service:

* **[!UICONTROL ID DO CLIENTE]**: a ID do cliente é a obrigatória `{API_KEY}` que deve ser fornecido no `x-api-key` cabeçalho.
* **[!UICONTROL ID DA ORGANIZAÇÃO]**: a ID da organização é o valor `{ORG_ID}` que deve ser usado no cabeçalho `x-gw-ims-org-id`.

![Os valores ID do cliente e ID da organização aparecem na página de visão geral do projeto depois que a API é configurada](../images/api/getting-started/jwt-credentials.png)

### Autenticação para cada sessão

A credencial final necessária que você deve coletar é sua `{ACCESS_TOKEN}`, que é usado no cabeçalho Autorização. Ao contrário dos valores de `{API_KEY}` e `{ORG_ID}`, um novo token deve ser gerado a cada 24 horas para continuar usando a API.

Em geral, há dois métodos de geração de um token de acesso:

* [Gerar o token manualmente](#manual-token) para testes e desenvolvimento.
* [Geração de token automatizada](#auto-token) para integrações de API.

#### Gerar um token manualmente {#manual-token}

Para gerar manualmente um novo `{ACCESS_TOKEN}`, abra a chave privada baixada anteriormente e cole o conteúdo na caixa de texto ao lado de **[!UICONTROL Gerar token de acesso]** antes de selecionar **[!UICONTROL Gerar token]**.

![O token de acesso gerado anteriormente que está sendo colado na página de visão geral do projeto, com a tag [!UICONTROL Gerar token] botão sendo selecionado após](../images/api/getting-started/paste-private-key.png)

É gerado um novo token de acesso, e é fornecido um botão para copiá-lo para a área de transferência. Esse valor é usado para o cabeçalho de Autorização necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`.

![O token de acesso gerado que está sendo copiado da interface do](../images/api/getting-started/generated-access-token.png)

#### Geração de token automatizada {#auto-token}

Você pode gerar novos tokens de acesso para processos automatizados enviando um JSON Web Token (JWT) por meio de uma solicitação POST para o Adobe Identity Management Service (IMS). Consulte o documento do Console do desenvolvedor em [Autenticação JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) para obter etapas detalhadas.

## Leitura de chamadas de API de amostra

Cada manual de endpoint fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/api-guide.md#sample-api) no guia de introdução às APIs da Platform.

## Próximas etapas

Agora que você entende quais cabeçalhos usar, você está pronto para começar a fazer chamadas para a API Privacy Service. Selecione um dos manuais de endpoint para começar:

* [Trabalhos de privacidade](./privacy-jobs.md)
* [Consentimento](./consent.md)
