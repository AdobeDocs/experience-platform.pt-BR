---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform
title: Introdução ao AI de conteúdo e comércio]
topic: Getting started
description: A API de E/S de conteúdo e comércio utiliza APIs de E/S de Adobe. Para fazer chamadas para APIs de E/S de Adobe e a Integração do console de E/S, você deve primeiro concluir o tutorial de autenticação.
translation-type: tm+mt
source-git-commit: 9ee888b02b4a402200ca4fcaed4a59c0a7eb94cd
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---


# Getting started with [!DNL Content and Commerce AI]

>[!NOTE]
>
>A API de conteúdo e comércio está em beta. A documentação está sujeita a alterações.

[!DNL Content and Commerce AI] utiliza APIs de E/S de Adobe. Para fazer chamadas para as APIs de E/S do Adobe e a integração do console de E/S, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação.

No entanto, quando você chega à etapa **Adicionar API** , a API está localizada em Experience Cloud em vez de Adobe Experience Platform, como mostrado na seguinte captura de tela:

![adição de AI de conteúdo e comércio](./images/add-api.png)

A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API de E/S do Adobe, como mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Criar um ambiente Postman (opcional)

Depois de configurar seu projeto e a API no Console do desenvolvedor do Adobe, você tem a opção de baixar um arquivo de ambiente para o Postman. Em **[!UICONTROL APIs]** no painel esquerdo do seu projeto, selecione **[!UICONTROL Conteúdo e Comércio AI]**. Uma nova guia é aberta, contendo um cartão rotulado &quot;[!DNL Try it out]&quot;. Selecione **Baixar para o Postman** para baixar um arquivo JSON usado para configurar o ambiente do postman.

![download para o carteiro](./images/add-to-postman.png)

Depois de baixar o arquivo, abra o Postman e selecione o ícone **de** engrenagem na parte superior direita para abrir a caixa de diálogo **Gerenciar ambientes** .

![ícone de engrenagem](./images/select-gear-icon.png)

Em seguida, selecione **Importar** na caixa de diálogo **Gerenciar ambientes** .

![importação](./images/import.png)

Você é redirecionado e é solicitado a selecionar um arquivo de ambiente do computador. Selecione o arquivo JSON que você baixou anteriormente e selecione **Abrir** para carregar o ambiente.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Você é redirecionado para a guia *Gerenciar ambientes* com um novo nome de ambiente preenchido. Selecione o nome do ambiente a ser visualização e edite as variáveis disponíveis no Postman. Você ainda precisa preencher manualmente os campos `JWT_TOKEN` e `ACCESS_TOKEN`. Esses valores devem ter sido obtidos ao concluir o tutorial [de](../../tutorials/authentication.md)autenticação.

![](./images/re-direct.png)

Após a conclusão, suas variáveis devem se parecer com a captura de tela abaixo. Selecione **Atualizar** para concluir a configuração do ambiente.

![](./images/final-environment.png)

Agora você pode selecionar seu ambiente no menu suspenso no canto superior direito e preencher automaticamente quaisquer valores salvos. Basta reeditar os valores a qualquer momento para atualizar todas as suas chamadas de API.

![exemplo](./images/select-environment.png)

Para obter mais informações sobre como trabalhar com APIs de E/S de Adobe usando o Postman, consulte a publicação Média sobre como [usar o Postman para autenticação JWT em E/S](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)de Adobe.

## Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md) de API de exemplo no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Depois de ter todas as suas credenciais, você estará pronto para configurar um funcionário personalizado para [!DNL Content and Commerce AI]. Os documentos a seguir ajudam a entender a estrutura de extensibilidade e a configuração do ambiente.

Para saber mais sobre a Estrutura de extensibilidade, leia a [introdução ao documento de extensibilidade](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) . Este documento descreve os pré-requisitos e os requisitos de provisionamento.

Para saber mais sobre como configurar um ambiente para [!DNL Content and Commerce AI], consulte o guia para [configurar um ambiente](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html)para desenvolvedores. Este documento fornece instruções de configuração que permitem que você se desenvolva para o Asset Compute Service.