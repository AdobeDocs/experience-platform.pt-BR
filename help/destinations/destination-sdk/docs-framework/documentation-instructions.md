---
title: Documente seu destino no Adobe Experience Platform
description: Instruções detalhadas sobre você para criar uma página de documentação para seu destino no Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: dd4a150351b5e0c41586cf663324aeb345a896e4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# Documente seu destino no Adobe Experience Platform

>[!IMPORTANT]
>
>O processo documentado aqui é necessário apenas para parceiros que enviam destinos (públicos) produzidos. Se estiver criando um destino privado para uso próprio, não será necessário criar e publicar a documentação para o destino.

## Visão geral {#overview}

Bem-vindo ao Adobe Experience Platform, ótimo ter você aqui!
A documentação do destino é a etapa final antes de poder ser definida no Adobe Experience Platform.

Esta seção de documentação inclui:

* Instruções passo a passo para criar uma página de documentação para seu novo destino;
* Um modelo a ser preenchido para o destino;
* [Instruções gerais sobre como usar o Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Instruções específicas para o aroma de Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (o sabor Adobe Markdown é muito semelhante ao Markdown normal).
* A [página práticas recomendadas](./authoring-best-practices.md) para ajudar você a criar uma página de documentação para a página de destino, que atende aos padrões de qualidade da documentação do Experience Platform.

## Pré-requisitos {#prerequisites}

Para criar documentação para seu destino de acordo com as instruções neste artigo, os seguintes itens são necessários:

* **Uma conta do GitHub**. Inscreva-se para [GitHub](https://github.com/) se você ainda não tiver uma conta.
* **Desktop do GitHub**. Se você selecionar [crie a documentação no ambiente local](./work-in-local-environment.md), você deve usar [Desktop do GitHub](https://desktop.github.com/).
* Sua integração com o Adobe deve estar em uma fase de teste com seu destino implantado em um ambiente de preparo no Adobe Experience Platform.

## Instruções de alto nível para criar documentação para seu destino no Adobe Experience Platform {#high-level-instructions}

Em um alto nível, para criar documentação para o seu destino, é necessário [criar uma bifurcação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) do repositório da documentação do Adobe Experience Platform e edite o [modelo de documentação fornecido](./self-service-template.md) em uma nova ramificação. Use o modelo fornecido pelo Adobe para criar uma nova página de destino. Abra uma solicitação de pull (PR) quando estiver pronto. As instruções para fazer isso estão mais abaixo, em [Etapas para criar a nova página de destino](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Modelo de documentação {#documentation-template}

Para ajudar você a criar a página de documentação, o Adobe pré-preencheu um [modelo de documentação](./self-service-template.md) para você. Além disso, abaixo, você pode encontrar instruções sobre como editar o modelo e abrir uma solicitação de pull. A equipe de documentação do Adobe verificará e publicará a documentação do novo destino.

[Baixe o modelo aqui](assets/yourdestination-template.zip) e descompacte o arquivo para extrair a variável `yourdestination.md` arquivo.

As instruções sobre como usar o modelo para criar sua página de documentação estão mais abaixo.

## Etapas para criar a nova página de destino {#steps-to-create-docs-page}

Você pode usar a interface da Web do GitHub ou seu ambiente local para criar documentação para seu novo destino no Adobe Experience Platform. Encontre instruções para ambas as opções nos links abaixo:

* [Usar a interface da Web do GitHub para criar uma página de documentação de destino](./use-github-interface-to-create-documentation.md)
* [Usar um editor de texto no ambiente local para criar uma página de documentação de destino](./work-in-local-environment.md)

## Práticas recomendadas {#best-practices}

Revise o [práticas recomendadas de criação](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) antes e enquanto você cria a página de documentação de destino. Leia também a seção [orientação de escrita para a documentação do Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) para obter mais dicas de escrita que a equipe de documentação do Adobe usa ao criar a documentação.