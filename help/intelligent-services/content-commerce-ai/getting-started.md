---
keywords: Experience Platform, introdução, ai do conteúdo, ai do comércio, ai do conteúdo e ai do comércio
solution: Experience Platform
title: Introdução ao Content and Commerce AI
description: A API do conteúdo e do Commerce utiliza APIs do Adobe I/O. Para fazer chamadas para APIs do Adobe I/O e a Integração do console de E/S, primeiro complete o tutorial de autenticação.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Introdução ao Content and Commerce AI

>[!NOTE]
>
>A API do conteúdo e do comércio está em beta. A documentação está sujeita a alterações.

[!DNL Content and Commerce AI] O usa APIs do Adobe I/O. Para fazer chamadas para APIs do Adobe I/O e a integração do console de E/S, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

No entanto, quando você chega ao **Adicionar API** , a API está localizada no Experience Cloud em vez do Adobe Experience Platform, conforme mostrado na seguinte captura de tela:

![adição de Content e Commerce AI](./images/add-api.png)

A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Adobe I/O, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Criar um ambiente Postman (opcional)

Depois de configurar seu projeto e a API no Adobe Developer Console, você tem a opção de baixar um arquivo de ambiente para o Postman. Em **[!UICONTROL APIs]** no painel esquerdo do projeto, selecione **[!UICONTROL Content e Commerce AI]**. Uma nova guia é aberta, contendo um cartão rotulado como &quot;[!DNL Try it out]&quot;. Selecionar **Download para Postman** para baixar um arquivo JSON usado para configurar o ambiente do postman.

![download para postman](./images/add-to-postman.png)

Após o download do arquivo, abra o Postman e selecione o **ícone de engrenagem** no canto superior direito para abrir o **gerenciar ambientes** caixa de diálogo.

![ícone de engrenagem](./images/select-gear-icon.png)

Em seguida, selecione **Importar** no **Gerenciar ambientes** caixa de diálogo.

![importar](./images/import.png)

Você é redirecionado e é solicitado a selecionar um arquivo de ambiente do seu computador. Selecione o arquivo JSON que você baixou anteriormente e selecione **Abrir** para carregar o ambiente.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Você é redirecionado para a função *Gerenciar ambientes* com um novo nome de ambiente preenchido. Selecione o nome do ambiente para exibir e editar as variáveis disponíveis no Postman. Ainda é necessário preencher manualmente a variável `JWT_TOKEN` e `ACCESS_TOKEN`. Estes valores devem ser obtidos durante a conclusão da [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct.png)

Uma vez concluída, suas variáveis devem ser semelhantes à captura de tela abaixo. Selecionar **Atualizar** para concluir a configuração do ambiente.

![](./images/final-environment.png)

Agora é possível selecionar seu ambiente no menu suspenso no canto superior direito e preencher automaticamente os valores salvos. Basta reeditar os valores a qualquer momento para atualizar todas as chamadas de API.

![exemplo](./images/select-environment.png)

Para obter mais informações sobre como trabalhar com APIs do Adobe I/O usando Postman, consulte a publicação média em [uso do Postman para autenticação JWT no Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md) no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Depois de ter todas as suas credenciais, você estará pronto para configurar um trabalhador personalizado para [!DNL Content and Commerce AI]. Os documentos a seguir ajudam a compreender a estrutura de extensibilidade e a configuração do ambiente.

Para saber mais sobre a Estrutura de extensibilidade, comece lendo a variável [introdução à extensibilidade](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) documento. Este documento descreve os pré-requisitos e os requisitos de provisionamento.

Para saber mais sobre como configurar um ambiente para [!DNL Content and Commerce AI], comece lendo o guia de [configuração de um ambiente de desenvolvedor](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Este documento fornece instruções de configuração que permitem desenvolver o serviço do Asset compute.
