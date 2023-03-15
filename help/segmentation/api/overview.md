---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;API;api;
title: Guia da API do Serviço de segmentação
description: A API do Serviço de segmentação permite que os desenvolvedores gerenciem programaticamente as operações de segmentação no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# Guia da API do Serviço de segmentação

[!DNL Adobe Experience Platform Segmentation Service] O permite criar segmentos e gerar públicos-alvo no [!DNL Adobe Experience Platform] do seu [!DNL Real-Time Customer Profile] dados.

A variável [!DNL Segmentation Service] A API fornece vários endpoints que permitem gerenciar programaticamente as operações de segmentação no [!DNL Experience Platform]. Este documento de visão geral fornece apresentações de alto nível a cada um desses endpoints, além de links para os guias de endpoint associados para obter detalhes. Antes de ler os manuais de endpoint individuais, consulte os [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para exibir todos os endpoints e operações CRUD disponíveis, consulte o [Referência da API do serviço de segmentação](https://www.adobe.io/experience-platform-apis/references/segmentation/).

<!-- ## Audiences

Audiences are a collection of people who share similar behaviors and/or characteristics. These can be generated either by using Platform or from external sources. You can use the `/audiences` endpoint to retrieve all audiences, create a new audience, retrieve details of a specific audience, update a specific audience, or delete a specific audience.

For more information on using this endpoint, please read the [audiences endpoint guide](./audiences.md). -->

## Exportar trabalhos

Os trabalhos de exportação são processos assíncronos usados para manter membros do segmento de público-alvo em conjuntos de dados. Você pode usar o `/export/jobs` endpoint para recuperar todos os trabalhos de exportação, criar um novo trabalho de exportação, recuperar detalhes de um trabalho de exportação específico ou cancelar um trabalho de exportação específico.

Para obter mais informações sobre como usar este endpoint, leia a [guia de endpoint de trabalhos de exportação](./export-jobs.md).

## Visualizações e estimativas

As visualizações fornecem uma lista paginada de perfis qualificados para uma definição de segmento, permitindo comparar os resultados com o que você espera. Você pode usar o `/preview` endpoint para criar um novo trabalho de visualização ou pesquisar resultados de um trabalho de visualização específico.

As estimativas fornecem informações estatísticas para definições de segmento, como tamanho do público projetado, intervalo de confiança e desvio padrão de erro. Você pode usar o `/estimate` endpoint para exibir uma estimativa de uma definição de segmento.

Para obter mais informações sobre como usar esses endpoints, leia a [guia de visualizações e estimativas de endpoints](./previews-and-estimates.md).

## Agendamentos

Os cronogramas são uma ferramenta que pode ser usada para executar automaticamente trabalhos de segmentação em lote uma vez por dia. Você pode usar o `/config/schedules` endpoint para recuperar uma lista de agendamentos, criar um novo agendamento, recuperar detalhes de um agendamento específico, atualizar um agendamento específico ou excluir um agendamento específico.

Para obter mais informações sobre como usar este endpoint, leia a [guia de endpoint de agendamentos](./schedules.md).

## Definições de segmento

As definições de segmento definem quais perfis farão parte de quais segmentos de público-alvo. Você pode usar o `/segment/definitions` ponto de extremidade para gerenciar definições de segmento.

Para obter mais informações sobre como usar este endpoint, leia a [guia de endpoint de definições de segmento](./segment-definitions.md).

## Trabalhos do segmento

Os trabalhos de segmento processam definições de segmento estabelecidas anteriormente para gerar um segmento de público-alvo. Você pode usar o `/segment/jobs` endpoint para gerenciar trabalhos do segmento.

Para obter mais informações sobre como usar este endpoint, leia a [manual de endpoint de trabalhos de segmento](./segment-jobs.md).

## Pesquisa de segmentos

A pesquisa de segmentos é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com pesquisa de segmento, consulte [guia de endpoint de pesquisa](segment-search.md)

## Próximas etapas

Para começar a usar o [!DNL Segmentation Service] , revise os diferentes manuais de endpoint para obter etapas detalhadas sobre como fazer chamadas para os vários endpoints do serviço. Para saber mais sobre como trabalhar com segmentos usando o [!DNL Platform] Interface do usuário do, consulte a [Guia do usuário de segmentação](../ui/overview.md).
