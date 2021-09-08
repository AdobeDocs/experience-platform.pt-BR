---
title: 'Usar a interface da Web do GitHub para criar uma página de documentação de destino '
seo-title: Use the GitHub web interface to create a destination documentation page
description: As instruções desta página mostram como usar a interface da Web do GitHub para criar documentação e enviar uma solicitação de pull.
seo-description: The instructions on this page show you how to use the GitHub web interface to author documentation and submit a pull request.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 2%

---

# Usar a interface da Web do GitHub para criar uma página de documentação de destino {#github-interface}

As instruções abaixo mostram como usar a interface da Web do GitHub para criar a documentação e enviar uma solicitação de pull (PR). Antes de passar pelas etapas indicadas aqui, leia [Documentar seu destino em Destinos do Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte também a documentação de suporte no guia do colaborador do Adobe:
>* [Instale as ferramentas de criação do Git e do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configurar o repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Fluxo de trabalho de contribuição do GitHub para grandes alterações](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Configurar o ambiente de criação do GitHub {#set-up-environment}

1. No navegador, navegue até `https://github.com/AdobeDocs/experience-platform.en`.
2. Para [bifurcar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) o repositório, clique em **Bifurcar** conforme mostrado na imagem abaixo.

   ![Repositório de documentação do Fork Adobe](./assets/ssd-fork-repo.png)

3. Na bifurcação do repositório, crie uma nova ramificação para o projeto, conforme mostrado abaixo. Use esta nova ramificação para o seu trabalho.

   ![Criar nova ramificação do GitHub](./assets/new-branch-github.gif)

4. Na estrutura de pastas GitHub do repositório bifurcado, navegue até `experience-platform.en/help/destinations/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a categoria `personalization`. Selecione **Adicionar arquivo > Criar novo arquivo**.

   ![Adicionar novo arquivo](./assets/github-navigate-and-create-file.gif)

5. Nomeie seu destino `YOURDESTINATION.md`, onde YOURDESTINATION é o nome do seu destino no Adobe Experience Platform. Por exemplo, se sua empresa é chamada Moviestar, você nomearia o arquivo `moviestar.md`.

## Crie a página de documentação para seu destino {#author-documentation}

1. Você criará o conteúdo da página de destino com base no [modelo de autoatendimento de documentação](./self-service-template.md). **[](assets/yourdestination-template.zip)** Baixe o template e descompacte-o para extrair o template  `.md` de arquivo.
2. Cole e edite o conteúdo do modelo com informações relevantes para seu destino em um editor de marcação online, como [dillinger.io](https://dillinger.io/). Siga as instruções no modelo para obter detalhes sobre o que você deve preencher e quais parágrafos podem ser removidos.
3. Copie o conteúdo do editor de marcação para o novo arquivo no GitHub.
4. Para capturas de tela ou imagens que você planeja usar, use a interface do GitHub para fazer upload dos arquivos para `experience-platform.en/help/destinations/assets/catalog/[...]`, onde `[...]` é a categoria desejada para seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a categoria `personalization`. Você precisa vincular às imagens da página que está criando. Consulte [instruções sobre como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Upload de imagem no GitHub](./assets/upload-image.gif)

5. Quando estiver pronto, salve o arquivo na ramificação.

![Confirmar criação do arquivo](./assets/ssd-confirm-file-creation.png)

## Envie sua documentação para revisão {#submit-review}

1. Depois de salvar o arquivo e fazer upload das imagens desejadas, você pode abrir uma solicitação de pull (PR) para mesclar sua ramificação de trabalho na ramificação principal do repositório da documentação do Adobe. Verifique se a ramificação em que você trabalhou está selecionada e selecione **Solicitação de pull**.

![Criar solicitação de pull](./assets/ssd-create-pull-request-1.png)

1. Certifique-se de que as ramificações base e comparativas estejam corretas. Adicione uma nota ao PR, descrevendo sua atualização e selecione **Criar solicitação de pull**. Isso abre uma PR para mesclar a ramificação de trabalho da bifurcação na ramificação principal do repositório do Adobe.

   >[!TIP]
   >
   >Deixe a caixa de seleção **Allow edits by maintainers** selecionada para que a equipe de documentação do Adobe possa fazer edições no PR.

   ![Criar solicitação de pull para o repositório de documentação do Adobe](./assets/ssd-create-pull-request-2.png)

1. Neste ponto, é exibida uma notificação solicitando que você assine o Contrato de licença de colaborador (CLA) do Adobe. Esta é uma etapa obrigatória. Após assinar o CLA, atualize a página do PR e envie a solicitação de pull.

1. Você pode confirmar que a solicitação de pull foi enviada inspecionando a guia **Solicitações de pull** em `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR bem-sucedido](./assets/ssd-pr-successful.png)

1. Obrigado! A equipe de documentação do Adobe entrará em contato com o PR caso alguma edição seja necessária e informará quando a documentação será publicada.

>[!TIP]
>
>Para adicionar imagens e links à sua documentação e para quaisquer outras perguntas sobre o Markdown, leia [Using Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) no guia de escrita colaborativa do Adobe.
