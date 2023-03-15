---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
solution: Experience Platform
title: Usar um editor de texto em seu ambiente local para criar uma página de documentação de códigos-fonte
description: Este documento fornece etapas sobre como usar seu ambiente local para criar documentação para sua fonte e enviar uma solicitação de pull (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# Use um editor de texto em seu ambiente local para criar uma página de documentação de origens

Este documento fornece etapas sobre como usar seu ambiente local para criar documentação para sua fonte e enviar uma solicitação de pull (PR).

>[!TIP]
>
>Os seguintes documentos do guia de contribuição do Adobe podem ser usados para apoiar ainda mais o processo de documentação: <ul><li>[Instale as ferramentas de criação do Git e do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Configurar o repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[Fluxo de trabalho de contribuição do GitHub para grandes alterações](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Pré-requisitos

O tutorial a seguir requer que o GitHub Desktop esteja instalado em sua máquina local. Se você não tiver o GitHub Desktop, é possível baixar o aplicativo [aqui](https://desktop.github.com/).

## Conectar-se ao GitHub e configurar o ambiente de criação local

A primeira etapa na configuração do ambiente de criação local é navegar até o [Repositório GitHub do Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Na página principal do repositório GitHub da Platform, selecione **Bifurcar**.

![bifurcação](../assets/fork.png)

Para clonar o repositório no computador local, selecione **Código**. No menu suspenso exibido, selecione **HTTPS** e selecione **Abrir com o GitHub Desktop**.

>[!TIP]
>
>Para obter mais informações, consulte o tutorial em [configuração do repositório Git localmente para a documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

Em seguida, aguarde alguns instantes para que o GitHub Desktop clone o `experience-platform.en` repositório.

![clonagem](../assets/cloning.png)

Quando o processo de clonagem for concluído, vá para o GitHub Desktop para criar uma nova ramificação. Selecionar **Principal** no início da navegação e selecione **Nova ramificação**

![nova ramificação](../assets/new-branch.png)

No painel pop-over exibido, digite um nome descritivo para a ramificação e selecione **Criar ramificação**.

![create-branch-vs](../assets/create-branch-vs.png)

Em seguida, selecione **Publicar ramificação**.

![publicar-ramificação](../assets/publish-branch.png)

## Crie a página de documentação da sua fonte

Com o repositório clonado no computador local e uma nova ramificação criada, agora é possível começar a criar a página de documentação para sua nova fonte por meio da [editor de texto de sua escolha](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors).

O Adobe recomenda usar [Código do Visual Studio](https://code.visualstudio.com/) e que você instale a extensão Adobe Markdown Authoring. Para instalar a extensão, inicie o Visual Studio Code e selecione o **Extensões** do menu de navegação esquerdo.

![ extensão](../assets/extension.png)

Em seguida, insira `Adobe Markdown Authoring` na barra de pesquisa e selecione **Instalar** na página exibida.

![instalar](../assets/install.png)

Com o computador local pronto, baixe o [modelo de documentação de origens](../assets/api-template.zip) e extrair o arquivo para `experience-platform.en/help/sources/tutorials/api/create/...` com [`...`] representando a categoria de sua escolha. Por exemplo, se você estiver criando uma origem de banco de dados, selecione a pasta do banco de dados.

Por fim, siga as instruções descritas no modelo e edite-o com as informações relevantes relacionadas à sua fonte.

![edit-template](../assets/edit-template.png)

## Envie sua documentação para revisão

Para criar uma solicitação de pull (PR) e enviar sua documentação para revisão, primeiro salve seu trabalho no [!DNL Visual Studio Code] (ou o editor de texto escolhido). Em seguida, usando o GitHub Desktop, insira uma mensagem de confirmação e selecione **Confirmar criação-origem-documentação**.

![commit-vs](../assets/commit-vs.png)

Em seguida, selecione **Origem de push** para carregar seu trabalho na ramificação remota.

![push-origin](../assets/push-origin.png)

Para criar uma solicitação de pull, selecione **Criar solicitação de pull**.

![create-pr-vs](../assets/create-pr-vs.png)

Certifique-se de que as ramificações base e de comparação estejam corretas. Adicione uma observação à PR, descrevendo a atualização e selecione **Criar pull request**. Isso abre uma PR para mesclar a ramificação de trabalho do seu trabalho na ramificação principal do repositório Adobe.

>[!TIP]
>
>Deixe a **Permitir edições pelos mantenedores** caixa de seleção marcada para garantir que a equipe de documentação do Adobe possa fazer edições na PR.

![create-pr](../assets/create-pr.png)

É possível confirmar se a solicitação de pull foi enviada ao inspecionar a guia pull requests em https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
