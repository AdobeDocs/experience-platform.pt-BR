---
title: Usar a interface da Web do GitHub para criar uma página de documentação de destino
description: As instruções nesta página mostram como usar a interface da Web do GitHub para criar uma página de documentação para o seu destino de Experience Platform e enviá-la para revisão.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# Usar a interface da Web do GitHub para criar uma página de documentação de destino {#github-interface}

As instruções abaixo mostram como usar a interface da Web do GitHub para criar a documentação e enviar uma solicitação de pull (PR). Antes de seguir as etapas indicadas aqui, leia [Documente seu destino nos Destinos do Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte também a documentação de suporte no guia do colaborador do Adobe:
>* [Instale as ferramentas de criação do Git e do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Configurar o repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [Fluxo de trabalho de contribuição do GitHub para grandes alterações](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Configurar o ambiente de criação do GitHub {#set-up-environment}

1. No navegador, navegue até `https://github.com/AdobeDocs/experience-platform.en`.
2. Para [bifurcação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) repositório, clique em **Bifurcar** conforme mostrado abaixo. Isso cria uma cópia do repositório Experience Platform em sua própria conta GitHub.

   ![Repositório de documentação do Fork Adobe](../assets/docs-framework/ssd-fork-repository.gif)

3. Na bifurcação do repositório, crie uma nova ramificação para o projeto, conforme mostrado abaixo. Use esta nova ramificação para seu trabalho.

   ![Criar nova ramificação do GitHub](../assets/docs-framework/new-branch-github.gif)

4. Na estrutura de pastas GitHub do repositório bifurcado, navegue até `experience-platform.en/help/destinations/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a variável `personalization` categoria. Selecionar **Adicionar arquivo > Criar novo arquivo**.

   ![Adicionar novo arquivo](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Nomeie seu destino `YOURDESTINATION.md`, onde YOURDESTINATION é o nome do seu destino no Adobe Experience Platform. Por exemplo, se sua empresa se chama Moviestar, você nomearia seu arquivo como `moviestar.md`.

## Crie a página de documentação do seu destino {#author-documentation}

1. Você criará o conteúdo da página de destino com base no [modelo de autoatendimento de documentação](./self-service-template.md). **[Baixar](../assets/docs-framework/yourdestination-template.zip)** o template e descompacte-o para extrair o `.md` modelo de arquivo.
2. Cole e edite o conteúdo do modelo com informações relevantes para o seu destino em um editor de markdown online, como [dillinger.io](https://dillinger.io/). Siga as instruções no modelo para obter detalhes sobre o que você deve preencher e quais parágrafos podem ser removidos.

   >[!TIP]
   >
   >Você pode fechar a janela do navegador a qualquer momento e reabri-la posteriormente. Seu trabalho é salvo automaticamente e aguardará você ao reabrir o navegador.
3. Copie o conteúdo do editor de marcação para seu novo arquivo no GitHub.
4. Para capturas de tela ou imagens que você planeja usar, use a interface do GitHub para fazer upload dos arquivos para o `experience-platform.en/help/destinations/assets/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a variável `personalization` categoria. É necessário vincular às imagens da página que você está criando. Consulte [instruções sobre como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).

   ![Carregar imagem no GitHub](../assets/docs-framework/upload-image.gif)

5. Quando estiver pronto, salve o arquivo na ramificação.

![Confirmar criação de arquivo](../assets/docs-framework/ssd-confirm-file-creation.png)

## Envie sua documentação para revisão {#submit-review}

>[!TIP]
>
>Observe que não há nada que você possa quebrar aqui. Seguindo as instruções nesta seção, você está simplesmente sugerindo uma atualização da documentação. A atualização sugerida será aprovada ou editada pela equipe de documentação da Adobe Experience Platform.

1. Depois de salvar o arquivo e carregar as imagens desejadas, você pode abrir uma solicitação de pull (PR) para mesclar a ramificação de trabalho à ramificação mestre do repositório da documentação do Adobe. Verifique se a ramificação em que você trabalhou está selecionada e selecione **Contribute > Abrir solicitação de pull**.

![Criar pull request](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Verifique se as ramificações base e de comparação estão corretas. Adicione uma observação à PR, descrevendo a atualização e selecione **Criar pull request**. Isso abre uma PR para mesclar a ramificação de trabalho da sua bifurcação na ramificação mestre do repositório Adobe.

   >[!TIP]
   >
   >Deixe a **Permitir edições pelos mantenedores** caixa de seleção marcada para que a equipe de documentação do Adobe possa fazer edições na PR.

   ![Criar solicitação de pull para o repositório de documentação do Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Nesse momento, é exibida uma notificação solicitando que você assine o Contrato de licença de colaborador (CLA) do Adobe. Essa é uma etapa obrigatória. Depois de assinar o CLA, atualize a página da PR e envie a solicitação de pull.

1. Você pode confirmar que a solicitação de pull foi enviada ao inspecionar o **Solicitações de pull** guia em `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR bem-sucedida](../assets/docs-framework/ssd-pr-successful.png)

1. Obrigado! A equipe de documentação do Adobe entrará em contato com o PR, caso seja necessário fazer alguma edição, e para informar quando a documentação será publicada.

>[!TIP]
>
>Para adicionar imagens e links à sua documentação e para qualquer outra pergunta sobre o Markdown, leia [Utilização do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) no guia de escrita colaborativa do Adobe.
