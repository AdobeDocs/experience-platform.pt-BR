---
title: Guia da API do Serviço de segmentação
description: A API do Serviço de segmentação permite que os desenvolvedores gerenciem programaticamente as operações de segmentação no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 3%

---

# Guia da API do Serviço de segmentação

O Adobe Experience Platform [!DNL Segmentation Service] permite criar públicos-alvo por meio de definições de segmento ou outras fontes no Adobe Experience Platform a partir dos dados do [!DNL Real-Time Customer Profile].

A API do [!DNL Segmentation Service] fornece vários endpoints que permitem gerenciar programaticamente suas operações de segmentação no [!DNL Experience Platform]. Este documento de visão geral fornece apresentações de alto nível a cada um desses endpoints, além de links para os guias de endpoint associados para obter detalhes. Antes de ler os manuais de endpoint individuais, consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre os cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

Para exibir todos os pontos de extremidade e operações CRUD disponíveis, consulte a [Referência da API do serviço de segmentação](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Públicos-alvo

Os públicos-alvo são uma coleção de pessoas que compartilham comportamentos e/ou características semelhantes. Eles podem ser gerados com o uso do Experience Platform ou de fontes externas. Você pode usar o ponto de extremidade `/audiences` para recuperar todos os públicos, criar um novo público, recuperar detalhes de um público específico, atualizar um público específico ou excluir um público específico.

Para obter mais informações sobre como usar este ponto de extremidade, leia o [manual do ponto de extremidade de públicos-alvo](./audiences.md).

## Exportar trabalhos

Os trabalhos de exportação são processos assíncronos usados para manter membros do segmento de público-alvo em conjuntos de dados. Você pode usar o ponto de extremidade `/export/jobs` para recuperar todos os trabalhos de exportação, criar um novo trabalho de exportação, recuperar detalhes de um trabalho de exportação específico ou cancelar um trabalho de exportação específico.

Para obter mais informações sobre como usar este ponto de extremidade, leia o [manual do ponto de extremidade de trabalhos de exportação](./export-jobs.md).

## Visualizações e estimativas

As visualizações fornecem uma lista paginada de perfis qualificados para uma definição de segmento, permitindo comparar os resultados com o que você espera. Você pode usar o ponto de extremidade `/preview` para criar um novo trabalho de visualização ou pesquisar resultados de um trabalho de visualização específico.

As estimativas fornecem informações estatísticas para definições de segmento, como tamanho do público projetado, intervalo de confiança e desvio padrão de erro. Você pode usar o ponto de extremidade `/estimate` para exibir uma estimativa de uma definição de segmento.

Para obter mais informações sobre como usar esses endpoints, leia o [guia de visualizações e estimativas de endpoints](./previews-and-estimates.md).

## Programações

Os cronogramas são uma ferramenta que pode ser usada para executar automaticamente trabalhos de segmentação em lote uma vez por dia. Você pode usar o ponto de extremidade `/config/schedules` para recuperar uma lista de agendamentos, criar um novo agendamento, recuperar detalhes de um agendamento específico, atualizar um agendamento específico ou excluir um agendamento específico.

Para obter mais informações sobre como usar este ponto de extremidade, leia o [manual do ponto de extremidade de agendamentos](./schedules.md).

## Definições de segmento

As definições de segmento definem quais perfis farão parte de qual público-alvo. Você pode usar o ponto de extremidade `/segment/definitions` para gerenciar definições de segmento.

Para obter mais informações sobre como usar este ponto de extremidade, leia o [manual do ponto de extremidade de definições de segmento](./segment-definitions.md).

## Trabalhos do segmento

Os trabalhos de segmento processam definições de segmento estabelecidas anteriormente para gerar um público-alvo. Você pode usar o ponto de extremidade `/segment/jobs` para gerenciar trabalhos de segmento.

Para obter mais informações sobre como usar este ponto de extremidade, leia o [manual do ponto de extremidade de trabalhos do segmento](./segment-jobs.md).

## Pesquisa de segmentos

A pesquisa de segmentos é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com pesquisa de segmentos, consulte o [manual do ponto de extremidade de pesquisa](segment-search.md)

## Próximas etapas

Para começar a usar a API [!DNL Segmentation Service], revise os diferentes manuais de ponto de extremidade para obter etapas detalhadas sobre como fazer chamadas para os vários pontos de extremidade do serviço. Para saber mais sobre como trabalhar com segmentos usando a interface do usuário do [!DNL Experience Platform], consulte o [Guia do usuário de segmentação](../ui/overview.md).
