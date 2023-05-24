---
title: Use um editor de texto em seu ambiente local para criar uma página de documentação de destino
description: As instruções nesta página mostram como usar um editor de texto para trabalhar em seu ambiente local a fim de criar uma página de documentação para seu destino de Experience Platform e enviá-la para revisão.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Use um editor de texto em seu ambiente local para criar uma página de documentação de destino {#local-authoring}

As instruções nesta página mostram como usar um editor de texto para trabalhar em seu ambiente local, criar documentação e enviar uma solicitação de pull (PR). Antes de seguir as etapas indicadas aqui, leia [Documente seu destino nos Destinos do Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte também a documentação de suporte no guia do colaborador do Adobe:
>* [Instale as ferramentas de criação do Git e do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configurar o repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Fluxo de trabalho de contribuição do GitHub para grandes alterações](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Conectar-se ao GitHub e configurar o ambiente de criação local {#set-up-environment}

1. No navegador, navegue até `https://github.com/AdobeDocs/experience-platform.en`
2. Para [bifurcação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) repositório, clique em **Bifurcar** conforme mostrado abaixo. Isso cria uma cópia do repositório Experience Platform em sua própria conta GitHub.

   ![Repositório de documentação do Fork Adobe](../assets/docs-framework/ssd-fork-repository.gif)

3. Clone o repositório no computador local. Selecionar **Código > HTTPS > Abrir com o GitHub Desktop**, conforme mostrado abaixo. Verifique se você tem [GitHub Desktop](https://desktop.github.com/) instalado. Para obter mais informações, leia [Criar um clone local do repositório](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) no guia do colaborador Adobe.

   ![Clonar o repositório da documentação do Adobe para o ambiente local](../assets/docs-framework/clone-local.png)

4. Na estrutura de arquivo local, navegue até `experience-platform.en/help/destinations/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a variável `personalization` pasta.

## Crie a página de documentação do seu destino {#author-documentation}

1. Sua página de documentação se baseia no [modelo de destino de autoatendimento](../docs-framework/self-service-template.md). Baixe o [modelo de destino](../assets/docs-framework/yourdestination-template.zip). Descompacte e extraia o arquivo `yourdestination-template.md` para o diretório mencionado na etapa 4 acima.  Renomear o arquivo `YOURDESTINATION.md`, onde YOURDESTINATION é o nome do seu destino no Adobe Experience Platform. Por exemplo, se sua empresa se chama Moviestar, você nomearia seu arquivo como `moviestar.md`.
2. Abra o novo arquivo na [editor de texto preferido](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). O Adobe recomenda usar [Código do Visual Studio](https://code.visualstudio.com/) e instale a extensão Adobe Markdown Authoring. Para instalar a extensão, abra o Visual Studio Code, selecione o **[!DNL Extensions]** no lado esquerdo da tela e procure `adobe markdown authoring`. Selecione a extensão e clique em **[!DNL Install]**.
   ![Instalar a extensão de criação do Adobe Markdown](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Edite o template com informações relevantes para o seu destino. Siga as instruções no modelo.
4. Para obter capturas de tela ou imagens que você planeja adicionar à documentação, acesse `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a variável `personalization` pasta. Crie uma nova pasta para o destino e salve as imagens aqui. Você deve vinculá-los a partir da página que está criando. Consulte [instruções sobre como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Quando estiver pronto, salve o arquivo em que está trabalhando.

## Envie sua documentação para revisão {#submit-review}

>[!TIP]
>
>Observe que não há nada que você possa quebrar aqui. Seguindo as instruções nesta seção, você está simplesmente sugerindo uma atualização da documentação. A atualização sugerida será aprovada ou editada pela equipe de documentação da Adobe Experience Platform.

1. No GitHub Desktop, crie uma ramificação de trabalho para suas atualizações e selecione **Publicar ramificação** para publicar a ramificação no GitHub.

![Nova ramificação local](../assets/docs-framework/new-branch-local.gif)

1. No GitHub Desktop, [confirmar](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) seu trabalho, conforme mostrado abaixo.

   ![Confirmar local](../assets/docs-framework/commit-local.png)

1. No GitHub Desktop, [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) seu trabalho para o [remoto](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) conforme mostrado abaixo.

   ![Enviar sua confirmação](../assets/docs-framework/push-local-to-remote.png)

1. Na interface da Web do GitHub, abra uma solicitação de pull (PR) para mesclar a ramificação de trabalho à ramificação principal do repositório de documentação do Adobe. Verifique se a ramificação em que você trabalhou está selecionada e selecione **Contribute > Abrir solicitação de pull**.

   ![Criar pull request](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Verifique se as ramificações base e de comparação estão corretas. Adicione uma observação à PR, descrevendo a atualização e selecione **Criar pull request**. Isso abre uma PR para mesclar a ramificação de trabalho da sua bifurcação na ramificação principal do repositório Adobe.
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
>Para adicionar imagens e links à sua documentação e para qualquer outra pergunta sobre o Markdown, leia [Utilização do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) no guia de escrita colaborativa do Adobe.
