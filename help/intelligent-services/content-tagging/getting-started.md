---
keywords: Experience Platform;introdução;ia de conteúdo;ia de comércio;marcação de conteúdo;getting started;content ai;commerce ai;content tagging
solution: Experience Platform
title: Introdução à marcação de conteúdo
description: A marcação de conteúdo usa APIs Adobe I/O. Para fazer chamadas para APIs Adobe I/O e a Integração do console de E/S, primeiro você deve concluir o tutorial de autenticação.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a98639851e7245b9cbd6fe42b35b4730dd19c3f8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Introdução à marcação de conteúdo

[!DNL Content tagging] O utiliza APIs de Adobe I/O. Para fazer chamadas para APIs Adobe I/O e a Integração do console de E/S, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

No entanto, quando você chega ao **Adicionar API** etapa, a API está localizada em Experience Cloud em vez de Adobe Experience Platform, como mostrado na seguinte captura de tela:

![adicionar marcação de conteúdo](./images/add-api-updated.png)

Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Adobe I/O, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Criar um ambiente do Postman (opcional)

Depois de configurar o projeto e a API no Console do Adobe Developer, você tem a opção de baixar um arquivo de ambiente para o Postman. Em **[!UICONTROL APIs]** no painel esquerdo do seu projeto, selecione **[!UICONTROL Marcação de conteúdo]**. Uma nova guia é aberta, contendo um cartão rotulado como &quot;[!DNL Try it out]&quot;. Selecionar **Baixar para Postman** para baixar um arquivo JSON usado para configurar o ambiente postman.

![baixar para postman](./images/add-to-postman-updated.png)

Depois de baixar o arquivo, abra o Postman e selecione o **ícone de engrenagem** no canto superior direito para abrir a **gerenciar ambientes** diálogo.

![ícone de engrenagem](./images/select-gear-icon.png)

Em seguida, selecione **Importar** de dentro do **Gerenciar ambientes** diálogo.

![importar](./images/import-updated.png)

Você será redirecionado e solicitado a selecionar um arquivo de ambiente do seu computador. Selecione o arquivo JSON que você baixou anteriormente e selecione **Abertura** para carregar o ambiente.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Você será redirecionado de volta para a *Gerenciar ambientes* com um novo nome de ambiente preenchido. Selecione o nome do ambiente para exibir e editar as variáveis disponíveis no Postman. Ainda é necessário preencher manualmente a `JWT_TOKEN` e `ACCESS_TOKEN`. Esses valores devem ter sido obtidos ao concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct-updated.png)

Uma vez concluídas, suas variáveis devem ser semelhantes à captura de tela abaixo. Selecionar **Atualizar** para concluir a configuração do ambiente.

![](./images/final-environment-updated.png)

Agora é possível selecionar o ambiente no menu suspenso no canto superior direito e preencher automaticamente todos os valores salvos. Basta reeditar os valores a qualquer momento para atualizar todas as chamadas de API.

![exemplo](./images/select-environment-updated.png)

Para obter mais informações sobre como trabalhar com APIs Adobe I/O usando o Postman, consulte a publicação Média em [uso do Postman para autenticação JWT no Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Leitura de chamadas de API de amostra

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md) no guia de solução de problemas de Experience Platform.

## Próximas etapas {#next-steps}

Depois de ter todas as credenciais, você estará pronto para configurar um trabalhador personalizado para [!DNL Content tagging]. Os documentos a seguir ajudam a entender a estrutura de extensibilidade e a configuração do ambiente.

Para saber mais sobre o Framework de extensibilidade, comece lendo o [introdução à extensibilidade](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) documento. Este documento descreve os pré-requisitos e os requisitos de provisionamento.

Para saber mais sobre a configuração de um ambiente para [!DNL Content tagging], comece lendo o guia de [configurar um ambiente de desenvolvedor](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Este documento fornece instruções de configuração que permitem desenvolver para o Serviço do Asset compute.
