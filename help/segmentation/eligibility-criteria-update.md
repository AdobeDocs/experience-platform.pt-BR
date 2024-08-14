---
title: Atualização dos critérios de qualificação de segmentação
description: Saiba mais sobre as atualizações de critérios de qualificação de segmentação que afetam os tipos de públicos que podem ser avaliados usando a segmentação de borda e de transmissão.
hide: true
hidefromtoc: true
source-git-commit: 0bbee2100ed6fdc0f40457965e195d07de6eb2a1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Atualização dos critérios de qualificação de segmentação

A partir de 24 de setembro de 2024, serão feitas duas atualizações que afetarão a qualificação de segmentação.

1. Tipos de consulta de segmentação de borda e transmissão
2. Políticas de mesclagem de transmissão e segmentação de borda

## Tipos de consulta

Qualquer definição de segmento **nova ou editada** que corresponda aos seguintes tipos de consulta **não será mais** avaliada usando streaming ou segmentação de borda. Em vez disso, eles serão avaliados usando a segmentação em lote.

- Um único evento com uma janela de tempo superior a 24 horas
   - Ative um público com todos os perfis que visualizaram uma página da Web nos últimos 3 dias.
- Um único evento sem janela de tempo
   - Ative um público com todos os perfis que visualizaram uma página da Web.

Se for necessário avaliar uma definição de segmento usando a transmissão ou segmentação de borda que corresponda ao tipo de consulta atualizado, você poderá criar explicitamente uma consulta em lote e de transmissão e combiná-las usando o segmento de segmentos.

Por exemplo, se você precisava ativar um público-alvo com todos os perfis que visualizaram uma página da Web nos últimos 3 dias usando a segmentação por transmissão, é possível criar as seguintes consultas:

- P1 (Streaming): todos os perfis que visualizaram uma página da Web nas últimas 24 horas
- P2 (Lote): Todos os perfis que visualizaram uma página da Web nos últimos 3 dias

Em seguida, é possível combiná-los referindo-se a Q1 ou Q2.

Da mesma forma, se for necessário ativar um público-alvo com todos os perfis que visualizaram uma página da Web, você poderá criar as seguintes consultas:

- P3 (Streaming): todos os perfis que visualizaram uma página da Web nas últimas 24 horas
- Q4 (Batch): todos os perfis que visualizaram uma página da Web.

Em seguida, é possível combiná-los fazendo referência a Q3 ou Q4.

>[!IMPORTANT]
>
>Todas as definições de segmento existentes que correspondem aos tipos de consulta permanecerão avaliadas usando transmissão ou segmentação de borda até serem editadas.
>
>Além disso, todas as definições de segmento existentes que atualmente atendem aos outros critérios de avaliação de transmissão ou segmentação de borda permanecerão avaliadas com a transmissão ou segmentação de borda.

## Política de mesclagem

Todas as definições de segmento **novas ou editadas** qualificadas para streaming ou segmentação de borda **devem** estar na política de mesclagem &quot;Ativo no Edge&quot;.

Todas as definições de segmento existentes que são avaliadas usando a segmentação de transmissão ou de borda continuarão funcionando como estão.
