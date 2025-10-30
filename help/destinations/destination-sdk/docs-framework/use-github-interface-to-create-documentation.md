---
title: Usar a interface da Web do GitHub para criar uma página de documentação de destino
description: As instruções nesta página mostram como usar a interface da Web do GitHub para criar uma página de documentação para o seu destino do Experience Platform e enviá-la para revisão.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: ff094c0c2c75e097140626d77478b8da9a7edf04
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Usar a interface da Web do GitHub para criar uma página de documentação de destino {#github-interface}

As instruções abaixo mostram como usar a interface da Web do GitHub para criar a documentação e enviar uma solicitação de pull (PR). Antes de seguir as etapas indicadas aqui, leia [Documentar seu destino nos Destinos do Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte também a documentação de suporte no guia do colaborador do Adobe:
>
>* [Instalar as ferramentas de criação do Git e do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=pt-BR)
>* [Configurar o repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=pt-BR)
>* [Fluxo de trabalho de contribuição do GitHub para grandes alterações](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=pt-BR).

## Configurar o ambiente de criação do GitHub {#set-up-environment}

1. Em seu navegador, navegue até `https://github.com/AdobeDocs/experience-platform.en`.
1. Para [bifurcar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=pt-BR#fork-the-repository) o repositório, clique em **Bifurcar** conforme mostrado abaixo. Isso cria uma cópia do repositório do Experience Platform em sua própria conta GitHub.

   ![Bifurcar repositório de documentação do Adobe](../assets/docs-framework/ssd-fork-repository.gif)

1. Na bifurcação do repositório, crie uma nova ramificação para o projeto, conforme mostrado abaixo. Use esta nova ramificação para seu trabalho.

   ![Criar nova ramificação do GitHub](../assets/docs-framework/new-branch-github.gif)

1. Na estrutura de pastas do GitHub do repositório bifurcado, navegue até `experience-platform.en/help/destinations/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se você estiver adicionando um destino de personalização ao Experience Platform, selecione a categoria `personalization`. Selecione **Adicionar arquivo > Criar novo arquivo**.

   ![Adicionar novo arquivo](../assets/docs-framework/github-navigate-and-create-file.gif)

1. Nomeie seu destino `YOURDESTINATION.md`, onde YOURDESTINATION é o nome de seu destino no Adobe Experience Platform. Por exemplo, se sua empresa se chama Moviestar, você chamaria seu arquivo de `moviestar.md`.

## Crie a página de documentação do seu destino {#author-documentation}

1. Você criará o conteúdo da página de destino com base no [modelo de autoatendimento de documentação](./self-service-template.md). **[Baixe](../assets/docs-framework/yourdestination-template.zip)** o modelo e descompacte-o para extrair o modelo de arquivo `.md`.
1. Cole e edite o conteúdo do modelo com informações relevantes para o seu destino em um editor de markdown online, como o [dillinger.io](https://dillinger.io/). Siga as instruções no modelo para obter detalhes sobre o que você deve preencher e quais parágrafos podem ser removidos.

   >[!TIP]
   >
   >Você pode fechar a janela do navegador a qualquer momento e reabri-la posteriormente. Seu trabalho é salvo automaticamente e aguardará você ao reabrir o navegador.
1. Copie o conteúdo do editor de marcação para seu novo arquivo no GitHub.
1. Para capturas de tela ou imagens que você planeja usar, use a interface do GitHub para carregar os arquivos para `experience-platform.en/help/destinations/assets/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se você estiver adicionando um destino de personalização ao Experience Platform, selecione a categoria `personalization`. É necessário vincular às imagens da página que você está criando. Consulte [instruções sobre como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=pt-BR#link-to-images).

   ![Carregar imagem no GitHub](../assets/docs-framework/upload-image.gif)

1. Quando estiver pronto, salve o arquivo na ramificação.

   ![Confirmar criação de arquivo](../assets/docs-framework/ssd-confirm-file-creation.png)

## Envie sua documentação para revisão {#submit-review}

>[!TIP]
>
>Observe que não há nada que você possa quebrar aqui. Seguindo as instruções nesta seção, você está simplesmente sugerindo uma atualização da documentação. A atualização sugerida será aprovada ou editada pela equipe de documentação da Adobe Experience Platform.

1. Depois de salvar o arquivo e carregar as imagens desejadas, você pode abrir uma solicitação de pull (PR) para mesclar a ramificação de trabalho à ramificação mestre do repositório de documentação do Adobe. Verifique se a ramificação em que você trabalhou está selecionada e selecione **Contribute > Abrir solicitação de pull**.

   ![Criar solicitação de pull](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Verifique se as ramificações base e de comparação estão corretas. Adicione uma observação à PR, descrevendo sua atualização, e selecione **Criar solicitação de pull**. Isso abre uma PR para mesclar a ramificação de trabalho da sua bifurcação com a ramificação mestre do repositório do Adobe.

   >[!TIP]
   >
   >Deixe marcada a caixa de seleção **Permitir edições pelos mantenedores** para que a equipe de documentação do Adobe possa fazer edições na PR.

   ![Criar solicitação de pull para o repositório de documentação do Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Nesse momento, é exibida uma notificação solicitando que você assine o Contrato de licença de colaborador (CLA) da Adobe. Essa é uma etapa obrigatória. Depois de assinar o CLA, atualize a página da PR e envie a solicitação de pull.

1. É possível confirmar se a solicitação de pull foi enviada ao inspecionar a guia **Solicitações de pull** em `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR bem-sucedida](../assets/docs-framework/ssd-pr-successful.png)

1. Obrigado! A equipe de documentação do Adobe entrará em contato com a PR, caso seja necessário fazer alguma edição, e para informar quando a documentação será publicada.

>[!TIP]
>
>Para adicionar imagens e links à sua documentação e a qualquer outra pergunta sobre o Markdown, leia [Usando o Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=pt-BR) no guia de escrita colaborativa da Adobe.
