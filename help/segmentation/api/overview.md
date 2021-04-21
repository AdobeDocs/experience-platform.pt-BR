---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; API; api;
title: Guia da API do serviço de segmentação
topic-legacy: guide
description: A API do Serviço de segmentação permite aos desenvolvedores gerenciar programaticamente as operações de segmentação no Adobe Experience Platform. Siga este guia para saber como executar operações principais usando a API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Guia da API do serviço de segmentação

[!DNL Adobe Experience Platform Segmentation Service] O permite criar segmentos e gerar públicos-alvo no a  [!DNL Adobe Experience Platform] partir de seus  [!DNL Real-time Customer Profile] dados.

A API [!DNL Segmentation Service] fornece vários endpoints que permitem gerenciar programaticamente suas operações de segmentação em [!DNL Experience Platform]. Este documento de visão geral fornece introduções de alto nível para cada um desses endpoints e links para seus guias de endpoint associados para obter detalhes. Antes de ler os guias de ponto de extremidade individuais, consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

Para visualizar todos os endpoints e operações CRUD disponíveis, consulte a [Referência da API do serviço de segmentação](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Exportar trabalhos

Os trabalhos de exportação são processos assíncronos usados para manter os membros do segmento do público-alvo em conjuntos de dados. Você pode usar o endpoint `/export/jobs` para recuperar todos os trabalhos de exportação, criar um novo trabalho de exportação, recuperar detalhes de um trabalho de exportação específico ou cancelar um trabalho de exportação específico.

Para obter mais informações sobre como usar esse endpoint, leia o [guia do endpoint de tarefas de exportação](./export-jobs.md).

## Visualizações e estimativas

As visualizações fornecem uma lista paginada de perfis de qualificação para uma definição de segmento, permitindo que você compare os resultados com o que espera. Você pode usar o endpoint `/preview` para criar um novo trabalho de pré-visualização ou consultar os resultados de um trabalho de pré-visualização específico.

As estimativas fornecem informações estatísticas para definições de segmentos, como tamanho de público-alvo projetado, intervalo de confiança e desvio padrão do erro. Você pode usar o terminal `/estimate` para exibir uma estimativa de definição de segmento.

Para obter mais informações sobre como usar esses endpoints, leia o [guia de pré-visualizações e estimativas de endpoints](./previews-and-estimates.md).

## Agendamentos

Os agendamentos são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia. Você pode usar o endpoint `/config/schedules` para recuperar uma lista de programações, criar uma nova programação, recuperar detalhes de uma programação específica, atualizar uma programação específica ou excluir uma programação específica.

Para obter mais informações sobre como usar esse endpoint, leia o [guia do endpoint de agendamentos](./schedules.md).

## Definições de segmento

As definições de segmento definem quais perfis farão parte de quais segmentos de público-alvo. Você pode usar o terminal `/segment/definitions` para gerenciar definições de segmento.

Para obter mais informações sobre como usar esse endpoint, leia o [guia do endpoint de definições de segmento](./segment-definitions.md).

## Trabalhos de segmento

As tarefas de segmento processam definições de segmento estabelecidas anteriormente para gerar um segmento de público-alvo. Você pode usar o terminal `/segment/jobs` para gerenciar tarefas de segmento.

Para obter mais informações sobre como usar esse endpoint, leia o [guia do endpoint de tarefas do segmento](./segment-jobs.md).

## Pesquisa de segmento

A pesquisa de segmento é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com a pesquisa de segmentos, consulte o [guia do endpoint de pesquisa](segment-search.md)

## Próximas etapas

Para começar a usar a API [!DNL Segmentation Service], consulte os diferentes guias de endpoint para obter etapas detalhadas sobre como fazer chamadas para os vários endpoints do serviço. Para saber mais sobre como trabalhar com segmentos usando a interface [!DNL Platform], consulte o [Guia do usuário de segmentação](../ui/overview.md).
