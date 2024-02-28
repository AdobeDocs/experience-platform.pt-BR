---
title: Guia da API do Serviço de segmentação
description: A API do Serviço de segmentação permite que os desenvolvedores gerenciem programaticamente as operações de segmentação no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# Guia da API do Serviço de segmentação

Adobe Experience Platform [!DNL Segmentation Service] O permite criar públicos-alvo por meio de definições de segmento ou outras fontes no Adobe Experience Platform a partir do [!DNL Real-Time Customer Profile] dados.

A variável [!DNL Segmentation Service] A API fornece vários endpoints que permitem gerenciar programaticamente as operações de segmentação no [!DNL Experience Platform]. Este documento de visão geral fornece apresentações de alto nível a cada um desses endpoints, além de links para os guias de endpoint associados para obter detalhes. Antes de ler os manuais de endpoint individuais, consulte os [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para exibir todos os endpoints e operações CRUD disponíveis, consulte o [Referência da API do serviço de segmentação](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Públicos-alvo

Os públicos-alvo são uma coleção de pessoas que compartilham comportamentos e/ou características semelhantes. Eles podem ser gerados usando a Platform ou de fontes externas. Você pode usar o `/audiences` endpoint para recuperar todos os públicos, criar um novo público, recuperar detalhes de um público específico, atualizar um público específico ou excluir um público específico.

Para obter mais informações sobre como usar este endpoint, leia a [manual de endpoint de públicos](./audiences.md).

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

As definições de segmento definem quais perfis farão parte de qual público-alvo. Você pode usar o `/segment/definitions` ponto de extremidade para gerenciar definições de segmento.

Para obter mais informações sobre como usar este endpoint, leia a [guia de endpoint de definições de segmento](./segment-definitions.md).

## Trabalhos do segmento

Os trabalhos de segmento processam definições de segmento estabelecidas anteriormente para gerar um público-alvo. Você pode usar o `/segment/jobs` endpoint para gerenciar trabalhos do segmento.

Para obter mais informações sobre como usar este endpoint, leia a [manual de endpoint de trabalhos de segmento](./segment-jobs.md).

## Pesquisa de segmentos

A pesquisa de segmentos é usada para pesquisar campos contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com pesquisa de segmento, consulte [guia de endpoint de pesquisa](segment-search.md)

## Próximas etapas

Para começar a usar o [!DNL Segmentation Service] , revise os diferentes manuais de endpoint para obter etapas detalhadas sobre como fazer chamadas para os vários endpoints do serviço. Para saber mais sobre como trabalhar com segmentos usando o [!DNL Platform] Interface do usuário do, consulte a [Guia do usuário de segmentação](../ui/overview.md).
