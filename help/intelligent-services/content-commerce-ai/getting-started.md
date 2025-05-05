---
keywords: Experience Platform;introdução;conteúdo;marcação de conteúdo
solution: Experience Platform
title: Introdução à marcação de conteúdo
description: A marcação de conteúdo usa APIs Adobe I/O. Para fazer chamadas para APIs Adobe I/O e a Integração do console de E/S, primeiro você deve concluir o tutorial de autenticação.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 7%

---

# Introdução à marcação de conteúdo

[!DNL Content tagging] usa APIs de Adobe I/O. Para fazer chamadas para APIs Adobe I/O e a Integração do Console de E/S, primeiro você deve concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

No entanto, quando você chega à etapa **Adicionar API**, a API está localizada em Creative Cloud em vez de Adobe Experience Platform, como mostrado na seguinte captura de tela:

![adicionando marcação de conteúdo](./images/add-api-updated.png)

Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Adobe I/O, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Criar um ambiente do Postman (opcional)

Depois de configurar o projeto e a API no Adobe Developer Console, você tem a opção de baixar um arquivo de ambiente para o Postman. Em **[!UICONTROL APIs]**, no painel esquerdo do projeto, selecione **[!UICONTROL Marcação de conteúdo]**. Uma nova guia é aberta, contendo um cartão rotulado como &quot;[!DNL Try it out]&quot;. Selecione **Baixar para Postman** para baixar um arquivo JSON usado para configurar seu ambiente postman.

![baixar para postman](./images/add-to-postman-updated.png)

Depois de baixar o arquivo, abra o Postman e selecione o **ícone de engrenagem** na parte superior direita para abrir a caixa de diálogo **gerenciar ambientes**.

![ícone de engrenagem](./images/select-gear-icon.png)

Em seguida, selecione **Importar** na caixa de diálogo **Gerenciar ambientes**.

![importar](./images/import-updated.png)

Você será redirecionado e solicitado a selecionar um arquivo de ambiente do seu computador. Selecione o arquivo JSON que você baixou anteriormente e selecione **Abrir** para carregar o ambiente.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Você será redirecionado de volta à guia *Gerenciar ambientes* com um novo nome de ambiente preenchido. Selecione o nome do ambiente para exibir e editar as variáveis disponíveis no Postman. Ainda é necessário preencher manualmente o `JWT_TOKEN` e `ACCESS_TOKEN`. Estes valores devem ter sido obtidos ao concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct-updated.png)

Uma vez concluídas, suas variáveis devem ser semelhantes à captura de tela abaixo. Selecione **Atualizar** para concluir a configuração do seu ambiente.

![](./images/final-environment-updated.png)

Agora é possível selecionar o ambiente no menu suspenso no canto superior direito e preencher automaticamente todos os valores salvos. Basta reeditar os valores a qualquer momento para atualizar todas as chamadas de API.

![exemplo](./images/select-environment-updated.png)

Para obter mais informações sobre como trabalhar com APIs de Adobe I/O usando o Postman, consulte a publicação do Medium em [como usar o Postman para autenticação JWT no Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md) no guia de solução de problemas de Experience Platform.

## Próximas etapas {#next-steps}

Depois de ter todas as suas credenciais, você estará pronto para configurar um trabalhador personalizado para [!DNL Content tagging]. Os documentos a seguir ajudam a entender a estrutura de extensibilidade e a configuração do ambiente.

Para saber mais sobre a Estrutura de extensibilidade, comece lendo o documento [introdução à extensibilidade](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=pt-BR). Este documento descreve os pré-requisitos e os requisitos de provisionamento.

Para saber mais sobre como configurar um ambiente para [!DNL Content tagging], comece lendo o guia para [configurar um ambiente de desenvolvedor](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html?lang=pt-BR). Este documento fornece instruções de configuração que permitem desenvolver para o Serviço do Asset Compute.
