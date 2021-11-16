---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
solution: Experience Platform
title: Visão geral do SDK de fontes (Beta)
topic-legacy: overview
description: O SDK das Fontes da Adobe Experience Platform é um conjunto de APIs de configuração que permitem integrar uma fonte baseada na API REST usando a API do Serviço de fluxo para trazer seus dados para o Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: d98cf404fd1a4d150f202154aba87b0089418957
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Visão geral do SDK de fontes (Beta)

>[!IMPORTANT]
>
>O SDK das Fontes está atualmente na versão beta e sua organização pode ainda não ter acesso a ele. A funcionalidade descrita nesta documentação está sujeita a alterações.

O SDK das Fontes Adobe Experience Platform é um conjunto de APIs de configuração que permitem integrar uma fonte baseada em API REST usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) para trazer seus dados para o Experience Platform.

Com o SDK de fontes, é possível:

* Configure uma nova fonte para o catálogo da plataforma, complete com as funcionalidades de criação, leitura, atualização e exclusão usando o [!DNL Flow Service] API.
* Defina as especificações para a fonte, incluindo informações relacionadas aos tipos de autenticação suportados e como os dados de recursos são buscados.
* Crie uma documentação voltada para o usuário para sua nova fonte.

A documentação do SDK de Fontes fornece instruções para usar o SDK de Fontes do Adobe Experience Platform para configurar, testar e lançar uma integração de fonte baseada em API REST com a Platform, e fazer com que sua fonte se torne parte do crescente catálogo de fontes.

![catálogo](./assets/catalog.png)

## Como entender as fontes

A Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

Para obter mais informações sobre fontes e ver uma lista de fontes diferentes atualmente compatíveis com a Plataforma, consulte a seção [visão geral das fontes](../home.md).

## Criar uma fonte

Por meio do SDK de Fontes, você pode integrar sua própria fonte baseada em API REST e trazer seus dados para a plataforma com o [!DNL Flow Service]. O SDK de Fontes permite integrar uma nova fonte com a Plataforma, criando e enviando uma nova especificação de conexão por meio do [!DNL Flow Service] API.

Consulte o guia sobre [criação de uma nova especificação de conexão](./api/api-overview.md) para obter informações sobre como integrar uma nova fonte à plataforma.

## Documente sua origem

Depois que a fonte for criada, consulte a [guia de documentação](./documentation/doc-overview.md) para obter instruções sobre como documentar sua fonte pelo [!DNL GitHub] interface da Web ou por meio de seu próprio editor de texto.

## Processo de alto nível

O processo passo a passo para configurar sua fonte no Experience Platform é descrito abaixo:

* Leia o [Guia da API do SDK de fontes](./api/api-overview.md);
   * Leia o [guia de introdução](./api/getting-started.md);
   * Siga o tutorial em [criação de uma nova especificação de conexão](./api/create.md);
   * Siga o tutorial em [atualização da especificação de conexão](./api/update-connection-specs.md);
   * Siga o tutorial em [adicionar a nova ID de especificação de conexão a uma especificação de fluxo](./api/update-flow-specs.md)
   * [Enviar sua nova fonte](./api/submit.md).
* Para entender melhor a estrutura e as propriedades de uma especificação de conexão, consulte o guia sobre [opções de configuração para o SDK do SDK do SDK do Sources](./config/config.md);
   * Consulte o guia sobre [configuração das especificações de autenticação](./config/authspec.md);
   * Consulte o guia sobre [configurar suas especificações de origem](./config/sourcespec.md);
   * Consulte o guia sobre [configurar suas especificações do explorador](./config/explorespec.md);
* Para começar a documentar sua fonte, consulte o [visão geral sobre como criar documentação para o SDK do SDK do SDK do Sources](./documentation/doc-overview.md)
   * Você pode usar [modelo de documentação das fontes](./documentation/template.md) para estruturar sua documentação;
   * Consulte o guia sobre [uso da interface da Web do GitHub](./documentation/github.md) para obter etapas sobre como criar documentação usando o GitHub;
   * Consulte o guia sobre [uso de um editor de texto](./documentation/text-editor.md) para obter etapas sobre como criar a documentação usando o computador local.

