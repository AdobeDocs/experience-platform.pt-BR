---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; API; api;
title: Guia da API do serviço de segmentação
topic-legacy: guide
description: A API do Serviço de segmentação permite aos desenvolvedores gerenciar programaticamente as operações de segmentação no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 6133c3127aaf10243d5472540c29125155c99d7b
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# Guia da API do serviço de segmentação

[!DNL Adobe Experience Platform Segmentation Service] permite criar segmentos e gerar públicos-alvo no [!DNL Adobe Experience Platform] do [!DNL Real-time Customer Profile] dados.

O [!DNL Segmentation Service] A API fornece vários endpoints que permitem gerenciar programaticamente suas operações de segmentação em [!DNL Experience Platform]. Este documento de visão geral fornece introduções de alto nível para cada um desses endpoints e links para seus guias de endpoint associados para obter detalhes. Antes de ler os guias de ponto de extremidade individuais, consulte [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para visualizar todos os endpoints disponíveis e operações CRUD, consulte [Referência da API do serviço de segmentação](https://www.adobe.io/experience-platform-apis/references/segmentation/).

<!-- ## Audiences

Audiences are a collection of people who share similar behaviors and/or characteristics. These can be generated either by using Platform or from external sources. You can use the `/audiences` endpoint to retrieve all audiences, create a new audience, retrieve details of a specific audience, update a specific audience, or delete a specific audience.

For more information on using this endpoint, please read the [audiences endpoint guide](./audiences.md). -->

## Exportar trabalhos

Os trabalhos de exportação são processos assíncronos usados para manter os membros do segmento do público-alvo em conjuntos de dados. Você pode usar o `/export/jobs` endpoint para recuperar todos os trabalhos de exportação, criar um novo trabalho de exportação, recuperar detalhes de um trabalho de exportação específico ou cancelar um trabalho de exportação específico.

Para obter mais informações sobre o uso deste ponto de extremidade, leia a [guia do endpoint de tarefas de exportação](./export-jobs.md).

## Visualizações e estimativas

As visualizações fornecem uma lista paginada de perfis de qualificação para uma definição de segmento, permitindo que você compare os resultados com o que espera. Você pode usar o `/preview` endpoint para criar um novo trabalho de visualização ou pesquisar resultados de um trabalho de visualização específico.

As estimativas fornecem informações estatísticas para definições de segmentos, como tamanho de público-alvo projetado, intervalo de confiança e desvio padrão do erro. Você pode usar o `/estimate` endpoint para exibir uma estimativa de definição de segmento.

Para obter mais informações sobre como usar esses endpoints, leia a [guia de visualizações e estimativas de endpoints](./previews-and-estimates.md).

## Agendamentos

Os agendamentos são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia. Você pode usar o `/config/schedules` endpoint para recuperar uma lista de programações, criar uma nova programação, recuperar detalhes de uma programação específica, atualizar uma programação específica ou excluir uma programação específica.

Para obter mais informações sobre o uso deste ponto de extremidade, leia a [guia de endpoint de agendamentos](./schedules.md).

## Definições de segmento

As definições de segmento definem quais perfis farão parte de quais segmentos de público-alvo. Você pode usar o `/segment/definitions` endpoint para gerenciar definições de segmento.

Para obter mais informações sobre o uso deste ponto de extremidade, leia a [guia do endpoint de definições de segmento](./segment-definitions.md).

## Trabalhos de segmento

As tarefas de segmento processam definições de segmento estabelecidas anteriormente para gerar um segmento de público-alvo. Você pode usar o `/segment/jobs` endpoint para gerenciar tarefas de segmento.

Para obter mais informações sobre o uso deste ponto de extremidade, leia a [guia do endpoint de tarefas do segmento](./segment-jobs.md).

## Pesquisa de segmento

A pesquisa de segmento é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com a pesquisa de segmentos, consulte o [guia do endpoint de pesquisa](segment-search.md)

## Próximas etapas

Para começar a usar o [!DNL Segmentation Service] Consulte a API e os diferentes guias de endpoint para obter etapas detalhadas sobre como fazer chamadas para os vários endpoints do serviço. Para saber mais sobre como trabalhar com segmentos usando a variável [!DNL Platform] interface do usuário, consulte a [Guia do usuário de segmentação](../ui/overview.md).
