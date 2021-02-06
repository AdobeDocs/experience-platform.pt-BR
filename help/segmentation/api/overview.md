---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation Service;API;api;
title: Guia da API do Serviço de Segmentação
topic: guide
description: A API do Serviço de segmentação permite que os desenvolvedores gerenciem de forma programática as operações de segmentação no Adobe Experience Platform. Siga este guia para saber como executar operações principais usando a API.
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Guia da API do serviço de segmentação

[!DNL Adobe Experience Platform Segmentation Service] permite que você crie segmentos e gere audiências  [!DNL Adobe Experience Platform] a partir de seus  [!DNL Real-time Customer Profile] dados.

A API [!DNL Segmentation Service] fornece vários pontos de extremidade que permitem gerenciar programaticamente suas operações de segmentação em [!DNL Experience Platform]. Este documento de visão geral fornece introduções de alto nível para cada um desses pontos de extremidade e links para seus guias de ponto de extremidade associados para obter detalhes. Antes de ler as guias de ponto de extremidade individuais, consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de amostra e muito mais.

Para visualização de todos os pontos de extremidade e operações CRUD disponíveis, consulte [Referência da API do Serviço de Segmentação](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Exportar trabalhos

Os trabalhos de exportação são processos assíncronos usados para persistir membros de segmentos de audiência em conjuntos de dados. Você pode usar o terminal `/export/jobs` para recuperar todos os trabalhos de exportação, criar um novo trabalho de exportação, recuperar detalhes de um trabalho de exportação específico ou cancelar um trabalho de exportação específico.

Para obter mais informações sobre como usar esse terminal, leia o [guia de ponto de extremidade de jobs de exportação](./export-jobs.md).

## Pré-visualizações e estimativas

As pré-visualizações fornecem uma lista paginada de perfis qualificados para uma definição de segmento, permitindo que você compare os resultados com o esperado. Você pode usar o terminal `/preview` para criar um novo trabalho de pré-visualização ou procurar resultados de um trabalho de pré-visualização específico.

As estimativas fornecem informações estatísticas para definições de segmentos, como tamanho de audiência projetado, intervalo de confiança e desvio padrão de erro. Você pode usar o terminal `/estimate` para visualização de uma estimativa de definição de segmento.

Para obter mais informações sobre como usar esses pontos de extremidade, leia o guia [pré-visualizações e estimativas de pontos de extremidade](./previews-and-estimates.md).

## Programações

As programações são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia. Você pode usar o terminal `/config/schedules` para recuperar uma lista de programações, criar uma nova programação, recuperar detalhes de uma programação específica, atualizar uma programação específica ou excluir uma programação específica.

Para obter mais informações sobre como usar esse terminal, leia o [guia de endpoint de agendamento](./schedules.md).

## Definições de segmento

As definições de segmentos definem quais perfis farão parte de quais segmentos de audiência. Você pode usar o terminal `/segment/definitions` para gerenciar definições de segmentos.

Para obter mais informações sobre como usar esse terminal, leia o guia de ponto final [definições de segmento](./segment-definitions.md).

## Trabalhos de segmento

O processo de trabalhos de segmento estabelecia definições de segmento anteriormente para gerar um segmento de audiência. Você pode usar o terminal `/segment/jobs` para gerenciar trabalhos de segmento.

Para obter mais informações sobre como usar esse terminal, leia o [guia de ponto de extremidade de trabalhos de segmento](./segment-jobs.md).

## Pesquisa de segmento

A pesquisa por segmento é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com a pesquisa de segmentos, consulte o [guia de ponto de extremidade de pesquisa](segment-search.md)

## Próximas etapas

Para começar a usar a API [!DNL Segmentation Service], consulte os diferentes guias de ponto de extremidade para obter etapas detalhadas sobre como fazer chamadas para os vários pontos de extremidade do serviço. Para saber mais sobre como trabalhar com segmentos usando a interface do usuário [!DNL Platform], consulte o [Guia do usuário de segmentação](../ui/overview.md).