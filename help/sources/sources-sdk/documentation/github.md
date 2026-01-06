---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
solution: Experience Platform
title: Use a interface da Web do GitHub para criar uma página de documentação de origens
description: Este documento fornece etapas sobre como usar a interface da Web do GitHub para criar a documentação e enviar uma solicitação de pull (PR).
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: acf1d4b9b2de6e0f674aca1f44b2504f3792327d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Usar a interface da Web do GitHub para criar uma página de documentação de origem

Este documento fornece etapas sobre como usar a interface da Web do GitHub para criar a documentação e enviar uma solicitação de pull (PR).

>[!TIP]
>
>Os seguintes documentos do guia de contribuição da Adobe podem ser usados para apoiar ainda mais seu processo de documentação: <ul><li>[Instalar as ferramentas de criação do Git e do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Configurar o repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[Fluxo de trabalho de contribuição do GitHub para grandes alterações](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Configurar o ambiente do GitHub

A primeira etapa na configuração do ambiente do GitHub é navegar até o [repositório do GitHub da Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![repositório-plataforma](../assets/platform-repo.png)

Em seguida, selecione **Bifurcação**.

![bifurcação](../assets/fork.png)

Quando a bifurcação estiver concluída, selecione **principal** e digite um nome para a nova ramificação no menu suspenso que aparece. Forneça um nome descritivo para a ramificação, pois ele será usado para conter seu trabalho, e selecione **criar ramificação**.

![criar-ramificação](../assets/create-branch.png)

Na estrutura de pastas GitHub do seu repositório bifurcado, navegue até [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) e selecione a categoria apropriada para a sua origem na lista. Por exemplo, se você estiver criando a documentação para uma nova origem do CRM, selecione **crm**.

>[!TIP]
>
>Se você estiver criando a documentação para a interface, navegue até [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) e selecione a categoria apropriada para sua origem. Para adicionar suas imagens, navegue até [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) e adicione suas capturas de tela à pasta `sdk`.

![crm](../assets/crm.png)

Uma pasta de fontes CRM existentes é exibida. Para adicionar a documentação de uma nova origem, selecione **Adicionar arquivo** e selecione **Criar novo arquivo** no menu suspenso exibido.

![criar-novo-arquivo](../assets/create-new-file.png)

Nomeie seu arquivo de origem `YOURSOURCE.md`, onde YOURSOURCE é o nome de sua origem no Experience Platform. Por exemplo, se sua empresa é o ACME CRM, seu nome de arquivo deve ser `acme-crm.md`.

![interface-git](../assets/git-interface.png)

## Crie a página de documentação da sua fonte

Para começar a documentar sua nova fonte, cole o conteúdo do [modelo de documentação de fontes](./template.md) no editor da Web do GitHub. Você também pode baixar o modelo [aqui](../assets/api-template.zip).

Com o modelo copiado para a interface do editor da Web do GitHub, siga as instruções descritas no modelo e edite os valores que contêm informações relevantes para a fonte.

![colar-modelo](../assets/paste-template.png)

Quando terminar, confirme o arquivo na ramificação.

![confirmar](../assets/commit.png)

## Envie sua documentação para revisão

Depois que o arquivo for confirmado, você poderá abrir uma solicitação de pull (PR) para mesclar a ramificação de trabalho com a ramificação principal do repositório de documentação do Adobe. Verifique se a ramificação em que você está trabalhando está selecionada e selecione **Solicitação de comparação e extração**.

![compare-pr](../assets/compare-pr.png)

Certifique-se de que as ramificações base e de comparação estejam corretas. Adicione uma observação à PR, descrevendo sua atualização e selecione **Criar solicitação de pull**. Isso abre uma PR para mesclar a ramificação de trabalho do seu trabalho na ramificação principal do repositório do Adobe.

>[!TIP]
>
>Deixe marcada a caixa de seleção **Permitir edições pelos mantenedores** para garantir que a equipe de documentação do Adobe possa fazer edições na PR.

![create-pr](../assets/create-pr.png)

Nesse momento, é exibida uma notificação solicitando que você assine o Contrato de licença de colaborador (CLA) da Adobe. Essa é uma etapa obrigatória. Depois de assinar o CLA, atualize a página da PR e envie a solicitação de pull.

É possível confirmar se a solicitação de pull foi enviada ao inspecionar a guia pull requests em https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
