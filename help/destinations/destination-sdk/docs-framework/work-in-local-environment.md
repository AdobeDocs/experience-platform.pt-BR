---
title: Usar um editor de texto no ambiente local para criar uma página de documentação de destino
seo-title: Use a text editor in your local environment to create a destination documentation page
description: As instruções desta página mostram como usar um editor de texto para trabalhar no ambiente local para criar documentação e enviar uma solicitação de pull.
seo-description: The instructions on this page show you how to use a text editor to work in your local environment to author documentation and submit a pull request.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e1e7d2f70c032d02f96b3999e4fca736070c6ca9
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 3%

---

# Usar um editor de texto no ambiente local para criar uma página de documentação de destino {#local-authoring}

As instruções desta página mostram como usar um editor de texto para trabalhar no ambiente local para criar documentação e enviar uma solicitação de pull (PR). Antes de passar pelas etapas indicadas aqui, leia [Documentar seu destino em Destinos do Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte também a documentação de suporte no guia do colaborador do Adobe:
>* [Instale as ferramentas de criação do Git e do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configurar o repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Fluxo de trabalho de contribuição do GitHub para grandes alterações](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Conecte-se ao GitHub e configure seu ambiente de criação local {#set-up-environment}

1. No navegador, navegue até `https://github.com/AdobeDocs/experience-platform.en`
2. Para [bifurcar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) o repositório, clique em **Bifurcar** como mostrado na captura de tela.

   ![Repositório de documentação do Fork Adobe](./assets/ssd-fork-repo.png)

3. Clone o repositório no computador local. Selecione **Code > HTTPS > Open with GitHub Desktop**, conforme mostrado abaixo. Verifique se o [GitHub Desktop](https://desktop.github.com/) está instalado. Para obter mais referência, leia [Create a local clone of the repository](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) no guia do colaborador do Adobe.

   ![Clone o repositório de documentação do Adobe para o ambiente local](./assets/clone-local.png)

4. Na estrutura de arquivo local, navegue até `experience-platform.en/help/destinations/catalog/[...]`, onde `[...]` é a categoria desejada para o destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a pasta `personalization`.

## Crie a página de documentação para seu destino {#author-documentation}

1. A página de documentação se baseia no [modelo de destino de autoatendimento](./self-service-template.md). Baixe o [modelo de destino](assets/yourdestination-template.zip). Descompacte-o e extraia o arquivo `yourdestination-template.md` para o diretório mencionado na etapa 4 acima.  Renomeie o arquivo `YOURDESTINATION.md`, onde YOURDESTINATION é o nome do seu destino no Adobe Experience Platform. Por exemplo, se sua empresa é chamada Moviestar, você nomearia o arquivo `moviestar.md`.
2. Abra o novo arquivo no [editor de texto de escolha](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). O Adobe recomenda usar [Visual Studio Code](https://code.visualstudio.com/) e instalar a extensão de criação do Adobe Markdown. Para instalar a extensão, abra o Código do Visual Studio, selecione a guia **[!DNL Extensions]** à esquerda da tela e procure por `adobe markdown authoring`. Selecione a extensão e clique em **[!DNL Install]**.
   ![Instalar a extensão de criação do Adobe Markdown](./assets/install-adobe-markdown-extension.gif)
3. Edite o modelo com informações relevantes para o seu destino. Siga as instruções no template.
4. Para quaisquer capturas de tela ou imagens que planeje adicionar à sua documentação, vá para `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, onde `[...]` é a categoria desejada para o seu destino. Por exemplo, se estiver adicionando um destino de personalização ao Experience Platform, selecione a pasta `personalization`. Crie uma nova pasta para o seu destino e salve suas imagens aqui. Você deve vincular a eles a partir da página que está criando. Consulte [instruções sobre como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Quando estiver pronto, salve o arquivo em que você está trabalhando.

## Envie sua documentação para revisão {#submit-review}

1. No GitHub Desktop, crie uma ramificação de trabalho para suas atualizações e selecione **Publicar ramificação** para publicar a ramificação no GitHub.

![Nova ramificação local](./assets/new-branch-local.gif)

1. No GitHub Desktop, [commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) seu trabalho, conforme mostrado abaixo.

   ![Confirmar local](./assets/commit-local.png)

1. No GitHub Desktop, [empurre](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) seu trabalho para a ramificação [remota](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote), conforme mostrado abaixo.

   ![Empurrar sua confirmação](./assets/push-local-to-remote.png)

1. Na interface da Web do GitHub, abra uma solicitação de pull (PR) para mesclar sua ramificação de trabalho na ramificação principal do repositório da documentação do Adobe. Verifique se a ramificação em que você trabalhou está selecionada e selecione **Solicitação de pull**.

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
