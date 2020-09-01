---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;API;api;
solution: Adobe Experience Platform
title: Guia do desenvolvedor do Adobe Experience Platform Segmentation Service
topic: guide
translation-type: tm+mt
source-git-commit: 0783979afa63890c77fd08f2d2ace4e141f59395
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Guia do desenvolvedor da Adobe Experience Platform [!DNL Segmentation Service] API

[!DNL Adobe Experience Platform Segmentation Service] permite que você crie segmentos e gere audiências a partir [!DNL Adobe Experience Platform] de seus [!DNL Real-time Customer Profile] dados.

A [!DNL Segmentation Service] API fornece vários pontos de extremidade que permitem gerenciar programaticamente suas operações de segmentação em [!DNL Experience Platform]. Este documento de visão geral fornece introduções de alto nível para cada um desses pontos de extremidade e links para seus guias de ponto de extremidade associados para obter detalhes. Antes de ler os guias de ponto de extremidade individuais, consulte o guia [de](./getting-started.md) introdução para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de amostra e muito mais.

Para visualização de todos os pontos de extremidade e operações CRUD disponíveis, consulte a referência [à API do Serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentação.

## Exportar trabalhos

Os trabalhos de exportação são processos assíncronos usados para persistir membros de segmentos de audiência em conjuntos de dados. Você pode usar o `/export/jobs` endpoint para recuperar todos os trabalhos de exportação, criar um novo trabalho de exportação, recuperar detalhes de um trabalho de exportação específico ou cancelar um trabalho de exportação específico.

Para obter mais informações sobre como usar esse terminal, leia o guia [de ponto de extremidade de trabalhos de](./export-jobs.md)exportação.

## Pré-visualizações e estimativas

As pré-visualizações fornecem uma lista paginada de perfis qualificados para uma definição de segmento, permitindo que você compare os resultados com o esperado. Você pode usar o `/preview` endpoint para criar um novo trabalho de pré-visualização ou procurar os resultados de um trabalho de pré-visualização específico.

As estimativas fornecem informações estatísticas para definições de segmentos, como tamanho de audiência projetado, intervalo de confiança e desvio padrão de erro. Você pode usar o `/estimate` endpoint para visualização de uma estimativa de uma definição de segmento.

Para obter mais informações sobre como usar esses pontos de extremidade, leia o guia [de pontos de extremidade de](./previews-and-estimates.md)pré-visualizações e estimativas.

## Programações

As programações são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia. Você pode usar o `/config/schedules` ponto de extremidade para recuperar uma lista de programações, criar uma nova programação, recuperar detalhes de uma programação específica, atualizar uma programação específica ou excluir uma programação específica.

Para obter mais informações sobre como usar este terminal, leia o guia [de ponto de extremidade de](./schedules.md)agendamento.

## Definições de segmento

As definições de segmentos definem quais perfis farão parte de quais segmentos de audiência. Você pode usar o `/segment/definitions` terminal para gerenciar definições de segmentos.

Para obter mais informações sobre como usar esse terminal, leia o guia [de ponto de extremidade de definições de](./segment-definitions.md)segmento.

## Trabalhos de segmento

O processo de trabalhos de segmento estabelecia definições de segmento anteriormente para gerar um segmento de audiência. Você pode usar o `/segment/jobs` terminal para gerenciar trabalhos de segmento.

Para obter mais informações sobre como usar esse terminal, leia o guia [de ponto de extremidade de trabalhos de](./segment-jobs.md)segmento.

## Pesquisa de segmento

A pesquisa por segmento é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com a pesquisa de segmentos, consulte o guia do ponto de extremidade [de pesquisa](segment-search.md)

## Próximas etapas

Para começar a usar a [!DNL Segmentation Service] API, consulte os diferentes guias de ponto de extremidade para obter etapas detalhadas sobre como fazer chamadas para os vários pontos de extremidade do serviço. Para saber mais sobre como trabalhar com segmentos usando a [!DNL Platform] interface do usuário, consulte o guia [do usuário de](../ui/overview.md)Segmentação.