---
title: Documente sua fonte (SDK de streaming)
description: A etapa final antes que sua nova fonte possa ser ativada no Adobe Experience Platform é documentar sua nova fonte.
hide: true
hidefromtoc: true
source-git-commit: a9879530a8911d77dfc4cde3824834e03fa5e0a9
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Documente sua fonte (SDK de streaming)

A etapa final antes que sua nova fonte possa ser definida no Adobe Experience Platform é documentar sua nova fonte.

Este guia de documentação inclui:

* Um tutorial que pode ser seguido para criar uma página de documentação para sua nova fonte;
* Um modelo de documentação a ser preenchido para a nova fonte;
* [Instruções sobre como usar o Markdown para escrever a documentação técnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Instruções sobre a compreensão do sabor do Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions).

## Pré-requisitos

Os itens a seguir são necessários antes de começar a documentar sua nova fonte:

* **Uma conta de usuário válida do GitHub**: Se você não tiver uma conta GitHub existente, crie uma por meio do [Página de inscrição do GitHub](https://github.com/);
* **Acesso ao GitHub Desktop**: Você deve usar o [Aplicativo de desktop do GitHub](https://desktop.github.com/) para criar a documentação de origem no ambiente local;
* Sua integração com o Adobe deve estar em uma fase de teste com sua origem implantada em um ambiente de preparo temporário na Platform.

## Instruções de alto nível para criar documentação para sua origem na plataforma

Em um alto nível, para criar a documentação para a sua origem, é necessário criar uma bifurcação do repositório da documentação da Plataforma e editar o modelo de documentação fornecido em uma nova ramificação. Use o modelo fornecido pelo Adobe para criar uma nova página de origem e abrir uma solicitação de pull (PR) quando estiver pronto. As instruções para fazer isso estão mais abaixo, nas etapas para criar sua nova página de origem.

## Modelo de documentação

Pode utilizar uma caneta pré-cheia. [Modelo de documentação da API](streaming-template-api.md) ou [Modelo de documentação da interface do usuário](streaming-template-ui.md) para ajudar a criar documentação para sua fonte. Mais abaixo, você pode encontrar instruções sobre como editar o modelo e abrir uma solicitação de pull. A documentação enviada para a nova fonte será revisada e publicada pela equipe de documentação do Adobe.

Você também pode baixar os modelos de documentação abaixo:

* [Modelo de documentação da API](../assets/streaming/streaming-template-api.zip)
* [Modelo de documentação da interface do usuário](../assets/streaming/streaming-template-ui.zip)

## Criar a nova página de origem

Você pode usar a interface da Web do GitHub ou seu ambiente local para criar a documentação para sua nova fonte no Platform. Encontre instruções para ambas as opções nos links abaixo:

* [Use a interface da Web do GitHub para criar uma página de documentação de origem](../documentation/github.md)
* [Usar um editor de texto no ambiente local para criar uma página de documentação de origem](../documentation/text-editor.md)