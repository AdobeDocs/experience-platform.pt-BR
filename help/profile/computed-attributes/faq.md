---
title: Perguntas frequentes sobre atributos computados
description: Descubra respostas para perguntas frequentes sobre o uso de atributos computados.
badge: "Beta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Perguntas frequentes

>[!IMPORTANT]
>
>Atributos computados estão atualmente em **beta** e está **não** disponível para todos os usuários.

No Adobe Experience Platform, os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização. Veja a seguir uma lista das perguntas frequentes sobre atributos computados.

## Quais conjuntos de dados contribuem para os cálculos de atributos calculados?

Os atributos computados consideram conjuntos de dados de Evento de experiência habilitados para Perfil do cliente em tempo real para calcular atributos computados.

## Quais campos do Experience Data Model (XDM) podem ser usados para criar atributos calculados?

Todos os campos XDM no esquema de união do Evento de experiência podem ser usados para criar atributos calculados.

## O que representa o &quot;último horário de avaliação&quot;?

O último horário de avaliação significa que os eventos **anterior** para esse carimbo de data e hora foram considerados na última atualização bem-sucedida do atributo calculado.

## Posso escolher a frequência de atualização? Como isso é decidido?

A frequência de atualização é determinada automaticamente com base no período de pesquisa do seu atributo calculado. Para obter mais informações sobre esse assunto, leia a [seção período de pesquisa](./overview.md#lookback-periods) da visão geral dos atributos calculados.

## Como os cálculos são afetados pelas expirações de dados do Evento de experiência?

Os cálculos de atributos calculados são baseados no período de pesquisa definido e nos Eventos de experiência que estão dentro desse período. Como resultado, esses cálculos são **não** afetados pelas expirações de dados do Evento de experiência. No entanto, para garantir a precisão dos atributos calculados, o período de pesquisa deve permanecer **no prazo de** os limites das expirações de dados.

## Posso criar um atributo calculado com base em outro atributo calculado?

Como os atributos calculados são criados usando campos de Evento de experiência e residem em um campo de Perfil, não há como usar diretamente um atributo calculado para criar outro atributo calculado.

## Existem limites para o número de atributos computados que eu posso criar?

O número máximo atual de **publicado** atributos computados é 25.

## Há alguma implicação downstream na desativação de um atributo calculado?

Antes de desabilitar o atributo calculado, você **deve** remova-os dos sistemas downstream (como segmentação, jornadas ou destinos), pois pode haver complicações que surgirão se não forem removidos.

## O que acontece quando eu desabilitar um atributo calculado? {#inactive-status}

Quando um atributo calculado é desativado ou tornado inativo, ele não é mais atualizado. Como resultado, este atributo calculado **não é possível** ser usado na pesquisa de perfil ou em outros usos downstream.

## Como os atributos computados ajudam a impulsionar o engajamento?

Os atributos computados impulsionam o enriquecimento do perfil ao agregar os atributos do evento em um nível de perfil mesclado. Por exemplo, você pode personalizar emails de marketing com o produto visualizado mais recentemente.
