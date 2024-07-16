---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
solution: Experience Platform
title: Visão geral de Origens de Autoatendimento (SDK em Lote)
description: Fontes de autoatendimento do Adobe Experience Platform (SDK em lote) é um conjunto de APIs de configuração que permitem integrar uma fonte baseada em API REST usando a API do serviço de fluxo para trazer seus dados para o Experience Platform.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 3%

---

# Visão geral de Fontes de autoatendimento (SDK em lote)

Fontes de Autoatendimento do Adobe Experience Platform (SDK em Lote) é uma estrutura que permite integrar uma fonte baseada em API REST ao catálogo de fontes de Experience Platform usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Fontes de autoatendimento (SDK em lote) fornecem um conjunto de APIs de configuração para criar sua própria fonte e trazer seus dados em lote para o Experience Platform.

Com Fontes de autoatendimento (SDK em lote), você pode:

* Configure e integre uma nova origem ao catálogo de Experience Platform usando a API [!DNL Flow Service].
* Defina especificações para sua origem, incluindo informações relacionadas aos tipos de autenticação compatíveis e como os dados do recurso são obtidos.
* Crie documentação voltada para o usuário para sua nova fonte.

A documentação de Fontes de autoatendimento fornece instruções para configurar, testar e liberar uma integração de fonte baseada em API REST com o Experience Platform, e fazer com que sua fonte se torne parte do catálogo de fontes em constante crescimento.

![catálogo](./assets/catalog.png)

## Noções básicas sobre fontes

O Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços de Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

Para obter mais informações sobre origens e para ver uma lista de origens diferentes atualmente com suporte no Experience Platform, consulte a [visão geral das origens](../home.md).

## Criar uma origem

Através das Fontes de Autoatendimento, você pode integrar sua própria fonte baseada em API REST e trazer seus dados para o Experience Platform com [!DNL Flow Service]. É possível integrar uma origem ao catálogo de origens de Experience Platform criando, configurando e enviando uma nova especificação de conexão por meio da API [!DNL Flow Service].

Consulte o manual sobre [criação de uma nova especificação de conexão](./api/api-overview.md) para obter informações sobre como integrar uma nova origem ao Experience Platform.

## Documentar sua origem

Depois que a origem for criada, consulte o [guia de documentação](./documentation/doc-overview.md) para obter instruções sobre como documentar a origem por meio da interface da Web do [!DNL GitHub] ou por meio do seu próprio editor de texto.

## Processo de alto nível

O processo passo a passo para configurar sua origem no Experience Platform é descrito abaixo:

* Leia o [Guia da API de Fontes de Autoatendimento (SDK em Lote)](./api/api-overview.md).
   * Leia o [guia de introdução](./api/getting-started.md).
   * Siga o tutorial em [criando uma nova especificação de conexão](./api/create.md).
   * Siga o tutorial em [atualizando sua especificação de conexão](./api/update-connection-specs.md).
   * Siga o tutorial em [adicionando sua nova ID de especificação de conexão a uma especificação de fluxo](./api/update-flow-specs.md)
   * [Enviar nova origem](./api/submit.md).
* Para entender melhor a estrutura e as propriedades de uma especificação de conexão, leia o manual sobre [opções de configuração para Fontes de Autoatendimento (SDK em Lote)](./config/config.md).
   * Leia o manual sobre [configuração das especificações de autenticação](./config/authspec.md) para compreender melhor os diferentes tipos de autenticação que você pode usar na sua origem.
   * Leia o guia em [configuração das especificações de origem](./config/sourcespec.md) para obter informações sobre os diferentes tipos de paginação, formatos de agendamento e esquemas personalizados que podem ser configurados para a origem.
   * Leia o manual sobre [configuração das especificações de exploração](./config/explorespec.md) para obter informações sobre como definir os parâmetros necessários para explorar e inspecionar objetos contidos na sua fonte.
* Para começar a documentar sua origem, leia a [visão geral sobre como criar documentação para Fontes de Autoatendimento](./documentation/doc-overview.md)
   * Você pode usar este [modelo de documentação da API de fontes](./documentation/template.md) para estruturar sua documentação de API.
   * Você pode usar este [modelo de documentação da interface do usuário](./documentation/ui-template.md) de fontes para estruturar sua documentação da interface do usuário.
   * Consulte o guia em [usando a interface da Web do GitHub](./documentation/github.md) para obter etapas sobre como criar a documentação usando o GitHub.
   * Consulte o guia em [usando um editor de texto](./documentation/text-editor.md) para obter etapas sobre como criar a documentação usando o computador local.
