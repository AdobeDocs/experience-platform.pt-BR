---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, Serviço de segmentação, pql, PQL, Linguagem de consulta de perfil, funções aritméticas, aritmética;
solution: Experience Platform
title: Funções Aritméticas PAL
description: As funções aritméticas são usadas para executar cálculos básicos em valores no Idioma da Consulta de Perfil (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# Funções aritméticas

As funções aritméticas são usadas para executar cálculos básicos em valores em [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Add

O `+` (adição) é usada para encontrar a soma de duas expressões de argumento.

**Formato**

```sql
{NUMBER} + {NUMBER}
```

**Exemplo**

A consulta PQL a seguir soma o preço de dois produtos diferentes.

```sql
product1.price + product2.price
```

## Multiplicar

O `*` (multiplicação) é usada para encontrar o produto de duas expressões de argumento.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Exemplo**

A consulta PQL a seguir encontra o produto do inventário e o preço de um produto para descobrir o valor bruto do produto.

```sql
product.inventory * product.price
```

## Subtrair

O `-` (subtração) é usada para encontrar a diferença de duas expressões de argumento.

**Formato**

```sql
{NUMBER} - {NUMBER}
```

**Exemplo**

A consulta PQL a seguir encontra a diferença de preço entre dois produtos diferentes.

```sql
product1.price - product2.price
```

## Dividir

O `/` (divisão) é usada para encontrar o quociente de duas expressões de argumento.

**Formato**

```sql
{NUMBER} / {NUMBER}
```

**Exemplo**

A consulta PQL a seguir encontra o quociente entre o total de produtos vendidos e o total de dinheiro ganho para ver o custo médio por item.

```sql
totalProduct.price / totalProduct.sold
```

## Remanescente

O `%` (modulo/rest) é usada para encontrar o restante após dividir as duas expressões de argumento.

**Formato**

```sql
{NUMBER} % {NUMBER}
```

**Exemplo**

A consulta PQL a seguir verifica se a idade da pessoa é divisível por cinco.

```sql
person.age % 5 = 0
```

## Próximas etapas

Agora que você aprendeu sobre funções aritméticas, pode usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a seção [Visão geral do idioma de consulta do perfil](./overview.md).
