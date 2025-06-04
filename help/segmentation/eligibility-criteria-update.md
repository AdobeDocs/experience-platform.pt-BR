---
title: Atualização dos critérios de qualificação de segmentação
description: Saiba mais sobre as atualizações de critérios de qualificação de segmentação que afetam os tipos de públicos que podem ser avaliados usando a segmentação de borda e de transmissão.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: 2af73be351cb818862006adc8d0f1a33f95d93cf
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 3%

---

# Atualização dos critérios de qualificação de segmentação

>[!IMPORTANT]
>
>Todas as definições de segmento existentes que são avaliadas usando a segmentação de transmissão ou de borda continuarão funcionando como estão, a menos que sejam editadas ou atualizadas.

A partir de 20 de maio de 2025, serão feitas três atualizações que afetam a qualificação de segmentação.

1. Conjunto de regras elegível
2. Elegibilidade da janela de tempo
3. Inclusão de dados em lote em públicos de transmissão
4. Políticas de mesclagem ativas

## Conjunto de regras {#ruleset}

Qualquer definição de segmento **nova ou editada** que corresponda aos conjuntos de regras a seguir **não será mais avaliada** usando streaming ou segmentação de borda. Em vez disso, eles serão avaliados usando a segmentação em lote.

- Um único evento com uma janela de tempo superior a 24 horas
   - Ative um público com todos os perfis que visualizaram uma página da Web nos últimos 3 dias.
- Um único evento sem janela de tempo
   - Ative um público com todos os perfis que visualizaram uma página da Web.

## Janela de tempo {#time-window}

Para avaliar um público com segmentação por transmissão, ele **deve** ser restrito em uma janela de tempo de 24 horas.

## Inclusão de dados em lote em públicos de transmissão {#include-batch-data}

Antes dessa atualização, você poderia criar uma definição de público-alvo de transmissão que combinasse fontes de dados de lote e de transmissão. No entanto, com a atualização mais recente, a criação de um público-alvo com fontes de dados em lote e de transmissão será avaliada usando a segmentação em lote.

Se for necessário avaliar uma definição de segmento usando a segmentação de borda ou transmissão que corresponda ao conjunto de regras atualizado, será necessário criar explicitamente um lote e um conjunto de regras de transmissão e combiná-los usando o segmento de segmentos. Este conjunto de regras em lotes **deve** ser baseado em um esquema de perfil.

Por exemplo, digamos que você tenha dois públicos-alvo, com um público-alvo hospedando dados do esquema de perfil e o outro hospedando dados do esquema de evento de experiência:

| Público-alvo | Esquema | Tipo de Source | Definição de consulta | ID do público-alvo |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Residentes da Califórnia | Perfil | Lote | O endereço residencial é no estado da Califórnia | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Check-outs recentes | Evento de experiência | Transmissão | Tem pelo menos um check-out nas últimas 24 horas | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Se você quiser usar o componente de lote no público-alvo de transmissão, será necessário fazer uma referência ao público-alvo em lote usando o segmento de segmentos.

Assim, um conjunto de regras de exemplo que combinasse os dois públicos-alvo seria semelhante a:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

O público-alvo resultante *será avaliado* usando a segmentação por transmissão, pois ela aproveita a associação do público-alvo em lote referindo-se ao componente de público-alvo em lote.

No entanto, se você quiser combinar dois públicos-alvo com dados de evento, **não poderá** apenas combinar os dois eventos. Você precisará criar ambos os públicos e, em seguida, criar outro público que use o `inSegment` para se referir a esses dois públicos.

Por exemplo, digamos que você tenha dois públicos-alvo, com ambos os públicos-alvo abrigando dados do esquema do evento de experiência:

| Público-alvo | Esquema | Tipo de Source | Definição de consulta | ID do público-alvo |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Desistências recentes | Evento de experiência | Lote | Tem pelo menos um evento de abandono nas últimas 24 horas | `7deb246a-49b4-4687-95f9-6316df049948` |
| Check-outs recentes | Evento de experiência | Transmissão | Tem pelo menos um check-out nas últimas 24 horas | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Nessa situação, seria necessário criar um terceiro público-alvo da seguinte maneira:

```
inSegment("7deb246a-49b4-4687-95f9-6316df049948") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Todas as definições de segmento existentes que correspondem aos conjuntos de regras permanecerão avaliadas usando a segmentação de transmissão ou de borda até serem editadas.
>
>Além disso, todas as definições de segmento existentes que atualmente atendem aos outros critérios de avaliação de transmissão ou segmentação de borda permanecerão avaliadas com a transmissão ou segmentação de borda.

## Política de mesclagem {#merge-policy}

Todas as definições de segmento **novas ou editadas** qualificadas para streaming ou segmentação de borda **devem** estar na política de mesclagem &quot;Ativo no Edge&quot;.

Se não houver uma política de mesclagem ativa definida, você precisará [configurar sua política de mesclagem](../profile/merge-policies/ui-guide.md#configure) e configurá-la para estar ativa na borda.
