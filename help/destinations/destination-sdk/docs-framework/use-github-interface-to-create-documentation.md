---
title: Usar a interface da Web do GitHub para criar uma página de documentação de destino
description: As instruções desta página mostram como usar a interface da Web do GitHub para criar uma página de documentação para o destino do Experience Platform e enviá-la para revisão.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 1%

---

# Usar a interface da Web do GitHub para criar uma página de documentação de destino {#github-interface}

As instruções abaixo mostram como usar a interface da Web do GitHub para criar a documentação e enviar uma solicitação de pull (PR). Antes de seguir as etapas indicadas aqui, leia [Documente seu destino em Destinos do Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte também a documentação de suporte no guia do colaborador do Adobe:
>* [Instale as ferramentas de criação do Git e do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configurar o repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Fluxo de trabalho de contribuição do GitHub para grandes alterações](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Configurar o ambiente de criação do GitHub {#set-up-environment}

1. No navegador, navegue até `https://github.com/AdobeDocs/experience-platform.en`.
2. Para [garfo](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) no repositório, clique em **Bifurcação** conforme mostrado abaixo. Isso cria uma cópia do repositório do Experience Platform em sua própria conta GitHub.

   ![Repositório de documentação do Fork Adobe](../assets/docs-framework/ssd-fork-repository.gif)

3. Na bifurcação do repositório, crie uma nova ramificação para o projeto, conforme mostrado abaixo. Use esta nova ramificação para o seu trabalho.

   ![Criar nova ramificação do GitHub](../assets/docs-framework/new-branch-github.gif)

4. Na estrutura de pastas do GitHub do repositório bifurcado, navegue até `experience-platform.en/help/destinations/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a variável `personalization` categoria . Selecionar **Adicionar arquivo > Criar novo arquivo**.

   ![Adicionar novo arquivo](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Dê um nome ao destino `YOURDESTINATION.md`, onde YOURDESTINATION é o nome do seu destino no Adobe Experience Platform. Por exemplo, se sua empresa é chamada Moviestar, você nomearia seu arquivo `moviestar.md`.

## Crie a página de documentação para seu destino {#author-documentation}

1. Você criará o conteúdo da página de destino com base no [modelo de autoatendimento da documentação](./self-service-template.md). **[Baixar](../assets/docs-framework/yourdestination-template.zip)** o modelo e descompacte-o para extrair o `.md` modelo de arquivo.
2. Cole e edite o conteúdo do modelo com informações relevantes para seu destino em um editor de marcação online, como [dillinger.io](https://dillinger.io/). Siga as instruções no modelo para obter detalhes sobre o que você deve preencher e quais parágrafos podem ser removidos.

   >[!TIP]
   >
   >Você pode fechar a janela do navegador a qualquer momento e reabrir mais tarde. Seu trabalho é salvo automaticamente e estará aguardando você ao reabrir o navegador.
3. Copie o conteúdo do editor de marcação para o novo arquivo no GitHub.
4. Para capturas de tela ou imagens que você planeja usar, use a interface do GitHub para fazer upload dos arquivos para `experience-platform.en/help/destinations/assets/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a variável `personalization` categoria . Você precisa vincular às imagens da página que está criando. Consulte [instruções sobre como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Upload de imagem no GitHub](../assets/docs-framework/upload-image.gif)

5. Quando estiver pronto, salve o arquivo na ramificação.

![Confirmar criação do arquivo](../assets/docs-framework/ssd-confirm-file-creation.png)

## Envie sua documentação para revisão {#submit-review}

>[!TIP]
>
>Observe que não há nada que você possa quebrar aqui. Ao seguir as instruções desta seção, você está apenas sugerindo uma atualização de documentação. Sua atualização sugerida será aprovada ou editada pela equipe de documentação da Adobe Experience Platform.

1. Depois de salvar o arquivo e fazer upload das imagens desejadas, você pode abrir uma solicitação de pull (PR) para mesclar sua ramificação de trabalho na ramificação principal do repositório da documentação do Adobe. Verifique se a ramificação em que você trabalhou está selecionada e selecione **Contribute > Abrir solicitação de pull**.

![Criar solicitação de pull](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Certifique-se de que as ramificações base e comparativas estejam corretas. Adicione uma nota ao PR, descrevendo sua atualização e selecione **Criar solicitação de pull**. Isso abre uma PR para mesclar a ramificação de trabalho da bifurcação na ramificação principal do repositório do Adobe.

   >[!TIP]
   >
   >Deixe o **Permitir edições por mantenedores** caixa de seleção selecionada para que a equipe de documentação do Adobe possa fazer edições no PR.

   ![Criar solicitação de pull para o repositório de documentação do Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Neste ponto, é exibida uma notificação solicitando que você assine o Contrato de licença de colaborador (CLA) do Adobe. Esta é uma etapa obrigatória. Após assinar o CLA, atualize a página do PR e envie a solicitação de pull.

1. Você pode confirmar que a solicitação de pull foi enviada inspecionando o **Solicitações de pull** em `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR bem-sucedido](../assets/docs-framework/ssd-pr-successful.png)

1. Obrigado! A equipe de documentação do Adobe entrará em contato com o PR caso alguma edição seja necessária e informará quando a documentação será publicada.

>[!TIP]
>
>Para adicionar imagens e links à sua documentação e para quaisquer outras perguntas sobre o Markdown, leia [Como usar o Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) no guia de escrita colaborativa do Adobe.
