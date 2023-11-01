---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
solution: Experience Platform
title: Documente sua fonte
description: A etapa final antes que a nova fonte possa ser ativada no Adobe Experience Platform é documentar a nova fonte.
exl-id: 80daadb1-127f-4f42-8bc9-fb89a7898462
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Documentar sua origem

A etapa final antes que a nova fonte possa ser definida como ativa no Adobe Experience Platform é documentar a nova fonte.

Este guia de documentação inclui:

* Um tutorial que você pode seguir para criar uma página de documentação para sua nova fonte;
* Um modelo de documentação que você deve preencher para sua nova fonte;
* [Instruções sobre como usar o Markdown para escrever a documentação técnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Instruções sobre como entender o sabor do Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions).

## Pré-requisitos

Os seguintes itens são necessários antes de você começar a documentar sua nova origem:

* **Uma conta de usuário GitHub válida**: se você não tiver uma conta GitHub existente, crie uma por meio do [Página de inscrição do GitHub](https://github.com/);
* **Acesso ao GitHub Desktop**: Você deve usar o [Aplicativo GitHub Desktop](https://desktop.github.com/) para criar sua documentação de origem em seu ambiente local;
* Sua integração com o Adobe deve estar em uma fase de teste com sua fonte implantada em um ambiente de preparo na plataforma.

## Instruções de alto nível para criar a documentação para sua origem na Platform

Em um alto nível, para criar a documentação para sua origem, você precisa criar uma bifurcação do repositório de documentação da Platform e editar o modelo de documentação fornecido em uma nova ramificação. Use o modelo fornecido pelo Adobe para criar uma nova página de origem e abrir uma solicitação de pull (PR) quando estiver pronto. As instruções para fazer isso estão mais abaixo, nas etapas para criar sua nova página de origem.

## Modelo de documentação

Você pode usar um pré-preenchido [modelo de documentação](./template.md) para ajudar a criar a documentação da sua origem. Mais abaixo, você pode encontrar instruções sobre como editar o modelo e abrir uma solicitação de pull. A documentação enviada para sua nova fonte será revisada e publicada pela equipe de documentação do Adobe.

Você também pode baixar os modelos de documentação abaixo:

* [Modelo da documentação da API](../assets/api-template.zip)
* [Modelo de documentação da interface do usuário](../assets/ui-template.zip)

## Criar sua nova página de origem

Você pode usar a interface da Web do GitHub ou seu ambiente local para criar a documentação para sua nova origem na Platform. Encontre instruções para ambas as opções nos links abaixo:

* [Usar a interface da Web do GitHub para criar uma página de documentação de origem](./github.md)
* [Use um editor de texto em seu ambiente local para criar uma página de documentação de origem](./text-editor.md)
