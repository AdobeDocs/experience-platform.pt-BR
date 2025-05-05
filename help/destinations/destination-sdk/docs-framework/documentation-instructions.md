---
title: Documentar seu destino no Adobe Experience Platform
description: Instruções detalhadas para criar uma página de documentação para seu destino no Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Documentar seu destino no Adobe Experience Platform

>[!IMPORTANT]
>
>O processo documentado aqui só é necessário para parceiros que enviam destinos (públicos) produzidos. Se você estiver criando um destino privado para uso próprio, não será necessário criar e publicar a documentação do para seu destino.

## Visão geral {#overview}

Bem-vindo ao Adobe Experience Platform, é ótimo ter você aqui!
A documentação do destino é a etapa final antes de poder ser definido online no Adobe Experience Platform.

Esta seção de documentação inclui:

* Instruções passo a passo para que você crie uma página de documentação para seu novo destino;
* Um modelo para você preencher para o seu destino;
* [Instruções gerais sobre o uso do Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=pt-BR);
* [Instruções específicas para o tipo de Markdown do Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=pt-BR#custom-markdown-extensions) (o tipo de Markdown do Adobe é muito semelhante ao Markdown comum).
* Uma [página de práticas recomendadas](./authoring-best-practices.md) para ajudá-lo a criar uma página de documentação para sua página de destino, que atenda aos padrões de qualidade da documentação do Experience Platform.

## Pré-requisitos {#prerequisites}

Para criar a documentação do seu destino de acordo com as instruções neste artigo, os seguintes itens são necessários:

* **Uma conta do GitHub**. Cadastre-se no [GitHub](https://github.com/) se ainda não tiver uma conta.
* **GitHub Desktop**. Se você optar por [criar a documentação em seu ambiente local](./work-in-local-environment.md), deverá usar o [GitHub Desktop](https://desktop.github.com/).
* Sua integração com o Adobe deve estar em uma fase de teste, com seu destino implantado em um ambiente de preparo no Adobe Experience Platform.

## Instruções de alto nível para criar a documentação para seu destino no Adobe Experience Platform {#high-level-instructions}

Em um alto nível, para criar a documentação para o seu destino, você precisa [criar uma bifurcação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=pt-BR#fork-the-repository) do repositório da documentação do Adobe Experience Platform e editar o [modelo de documentação fornecido](./self-service-template.md) em uma nova ramificação. Use o modelo fornecido pelo Adobe para criar uma nova página de destino. Abra uma solicitação de pull (PR) quando estiver pronto. As instruções para fazer isso estão mais abaixo, em [Etapas para criar sua nova página de destino](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/pt-BR/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Modelo de documentação {#documentation-template}

Para ajudá-lo a criar sua página de documentação, o Adobe preencheu previamente um [modelo de documentação](./self-service-template.md) para você. Mais abaixo, você pode encontrar instruções sobre como editar o modelo e abrir uma solicitação de pull. A equipe de documentação do Adobe revisará e publicará a documentação para o novo destino.

[Baixe o modelo aqui](../assets/docs-framework/yourdestination-template.zip) e descompacte o arquivo para extrair o arquivo `yourdestination.md`.

As instruções sobre como usar o modelo para criar sua página de documentação estão mais abaixo.

## Etapas para criar sua nova página de destino {#steps-to-create-docs-page}

Você pode usar a interface da Web do GitHub ou seu ambiente local para criar a documentação para seu novo destino no Adobe Experience Platform. Encontre instruções para ambas as opções nos links abaixo:

* [Usar a interface da Web do GitHub para criar uma página de documentação de destino](./use-github-interface-to-create-documentation.md)
* [Use um editor de texto em seu ambiente local para criar uma página de documentação de destino](./work-in-local-environment.md)

## Práticas recomendadas {#best-practices}

Revise as [práticas recomendadas de criação](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) antes e enquanto cria a página de documentação de destino. Leia também as [orientações de escrita da Documentação do Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=pt-BR) para obter mais dicas de escrita que a equipe de documentação do Adobe usa ao criar a documentação.