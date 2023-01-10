---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
solution: Experience Platform
title: Visão geral das fontes de autoatendimento (SDK em lote)
description: Fontes de autoatendimento Adobe Experience Platform (SDK em lote) é um conjunto de APIs de configuração que permitem integrar uma fonte baseada em REST API usando a API de Serviço de fluxo para trazer seus dados para o Experience Platform.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Visão geral das Fontes de autoatendimento (SDK em lote)

Fontes de autoatendimento Adobe Experience Platform (SDK em lote) é uma estrutura que permite integrar uma fonte baseada em API REST ao catálogo de fontes de Experience Platform usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). As Fontes de autoatendimento (SDK em lote) fornecem um conjunto de APIs de configuração para criar sua própria fonte e trazer seus dados em lote para o Experience Platform.

Com as Fontes de autoatendimento (SDK em lote), é possível:

* Configure e integre uma nova fonte ao catálogo de Experience Platform usando o [!DNL Flow Service] API.
* Defina as especificações para a fonte, incluindo informações relacionadas aos tipos de autenticação suportados e como os dados de recursos são buscados.
* Crie uma documentação voltada para o usuário para sua nova fonte.

A documentação de Fontes de autoatendimento fornece instruções para configurar, testar e lançar uma integração de fonte baseada em API REST com o Experience Platform, e fazer com que sua fonte faça parte do crescente catálogo de fontes.

![catálogo](./assets/catalog.png)

## Como entender as fontes

O Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permite estruturar, rotular e aprimorar esses dados usando os serviços do Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

Para obter mais informações sobre fontes e ver uma lista de fontes diferentes atualmente suportadas no Experience Platform, consulte o [visão geral das fontes](../home.md).

## Criar uma fonte

Por meio de fontes de autoatendimento, você pode integrar sua própria fonte baseada em REST API e trazer seus dados para o Experience Platform com [!DNL Flow Service]. Você pode integrar uma fonte ao catálogo de fontes do Experience Platform criando, configurando e enviando uma nova especificação de conexão por meio do [!DNL Flow Service] API.

Consulte o guia sobre [criação de uma nova especificação de conexão](./api/api-overview.md) para obter informações sobre como integrar uma nova fonte ao Experience Platform.

## Documente sua origem

Depois que a fonte for criada, consulte a [guia de documentação](./documentation/doc-overview.md) para obter instruções sobre como documentar sua fonte pelo [!DNL GitHub] interface da Web ou por meio de seu próprio editor de texto.

## Processo de alto nível

O processo passo a passo para configurar sua fonte no Experience Platform é descrito abaixo:

* Leia o [Guia da API de Fontes de autoatendimento (SDK em lote)](./api/api-overview.md).
   * Leia o [guia de introdução](./api/getting-started.md).
   * Siga o tutorial em [criação de uma nova especificação de conexão](./api/create.md).
   * Siga o tutorial em [atualização da especificação de conexão](./api/update-connection-specs.md).
   * Siga o tutorial em [adicionar a nova ID de especificação de conexão a uma especificação de fluxo](./api/update-flow-specs.md)
   * [Enviar sua nova fonte](./api/submit.md).
* Para entender melhor a estrutura e as propriedades de uma especificação de conexão, leia o guia sobre [opções de configuração para Fontes de autoatendimento (SDK em lote)](./config/config.md).
   * Leia o guia em [configuração das especificações de autenticação](./config/authspec.md) para obter uma melhor compreensão dos diferentes tipos de autenticação que você pode usar para sua fonte.
   * Leia o guia em [configurar suas especificações de origem](./config/sourcespec.md) para obter informações sobre os diferentes tipos de paginação, formatos de agendamento e esquemas personalizados que podem ser configurados para sua origem.
   * Leia o guia em [configurar suas especificações do explorador](./config/explorespec.md) para obter informações sobre como definir os parâmetros necessários para explorar e inspecionar objetos contidos em sua origem.
* Para começar a documentar sua fonte, leia o [visão geral sobre como criar documentação para fontes de autoatendimento](./documentation/doc-overview.md)
   * Você pode usar [modelo de documentação da API de fontes](./documentation/template.md) para estruturar a documentação da API.
   * Você pode usar [modelo de documentação da interface do usuário de fontes](./documentation/ui-template.md) para estruturar sua documentação da interface do usuário.
   * Consulte o guia sobre [uso da interface da Web do GitHub](./documentation/github.md) para obter as etapas sobre como criar a documentação usando o GitHub.
   * Consulte o guia sobre [uso de um editor de texto](./documentation/text-editor.md) para obter etapas sobre como criar a documentação usando o computador local.
