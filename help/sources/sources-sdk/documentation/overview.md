---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
solution: Experience Platform
title: Documente sua origem
topic-legacy: overview
description: A etapa final antes que sua nova fonte possa ser ativada no Adobe Experience Platform é documentar sua nova fonte.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Documente sua origem

>[!IMPORTANT]
>
>O SDK das Fontes está atualmente na versão beta e sua organização pode ainda não ter acesso a ele. A funcionalidade descrita nesta documentação está sujeita a alterações.

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

Pode utilizar uma caneta pré-cheia. [modelo de documentação](./template.md) para ajudar a criar documentação para sua fonte. Mais abaixo, você pode encontrar instruções sobre como editar o modelo e abrir uma solicitação de pull. A documentação enviada para a nova fonte será revisada e publicada pela equipe de documentação do Adobe.

Também é possível baixar a variável [modelo de documentação aqui](../assets/template.zip).

## Criar a nova página de origem

Você pode usar a interface da Web do GitHub ou seu ambiente local para criar a documentação para sua nova fonte no Platform. Encontre instruções para ambas as opções nos links abaixo:

* [Use a interface da Web do GitHub para criar uma página de documentação de origem](./github.md)
* [Usar um editor de texto no ambiente local para criar uma página de documentação de origem](./text-editor.md)