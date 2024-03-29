---
title: Documentar sua fonte (SDK de transmissão)
description: A etapa final antes que a nova fonte possa ser ativada no Adobe Experience Platform é documentar a nova fonte.
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Documentar sua fonte (SDK de transmissão)

>[!NOTE]
>
>O SDK de transmissão de fontes de autoatendimento está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

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

Você pode usar um pré-preenchido [Modelo da documentação da API](streaming-template-api.md) ou o [Modelo de documentação da interface do usuário](streaming-template-ui.md) para ajudar a criar a documentação da sua origem. Mais abaixo, você pode encontrar instruções sobre como editar o modelo e abrir uma solicitação de pull. A documentação enviada para sua nova fonte será revisada e publicada pela equipe de documentação do Adobe.

Você também pode baixar os modelos de documentação abaixo:

* [Modelo da documentação da API](../assets/streaming/streaming-template-api.zip)
* [Modelo de documentação da interface do usuário](../assets/streaming/streaming-template-ui.zip)

## Criar sua nova página de origem

Você pode usar a interface da Web do GitHub ou seu ambiente local para criar a documentação para sua nova origem na Platform. Encontre instruções para ambas as opções nos links abaixo:

* [Usar a interface da Web do GitHub para criar uma página de documentação de origem](../documentation/github.md)
* [Use um editor de texto em seu ambiente local para criar uma página de documentação de origem](../documentation/text-editor.md)
