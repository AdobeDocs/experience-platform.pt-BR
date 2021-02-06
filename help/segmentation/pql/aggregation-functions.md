---
keywords: Experience Platform;home;popular topics;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Idioma do Query do Perfil;funções de agregação;agregar;
solution: Experience Platform
title: Funções de agregação de PQL
topic: developer guide
description: 'As funções de agregação são usadas para agrupar vários valores em matrizes de linguagem de Query de Perfil (PQL) para formar um único valor de resumo. '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---


# Funções de agregação

As funções de agregação são usadas para agrupar vários valores em arrays [!DNL Profile Query Language] (PQL) para formar um único valor de resumo. Para obter mais informações sobre outras funções PQL, consulte [[!DNL Profile Query Language] overview](./overview.md).

## Contagem

A função `count` retorna o número de elementos dentro da matriz especificada.

**Formato**

```sql
{ARRAY}.count()
```

**Exemplo**

O query PQL a seguir retorna o número de pedidos no storage.

```sql
orders.count()
```

## Sum

A função `sum` retorna a soma de todos os valores selecionados dentro da matriz.

**Formato**

```sql
{ARRAY}.sum()
```

**Exemplo**

O query PQL a seguir retorna a soma de todos os preços dos pedidos.

```sql
orders.sum(order.price)
```

## Average

A função `average` retorna a média aritmética de todos os valores selecionados dentro da matriz.

**Formato**

```sql
{ARRAY}.average()
```

**Exemplo**

O query PQL a seguir retorna o preço médio de todos os pedidos.

```sql
orders.average(order.price)
```

## Mínimo

A função `min` retorna o menor de todos os valores selecionados dentro da matriz.

**Formato**

```sql
{ARRAY}.min()
```

**Exemplo**

O query PQL a seguir retorna o preço mais baixo de todos os pedidos.

```sql
orders.min(order.price)
```

## Máximo

A função `max` retorna o maior de todos os valores selecionados dentro da matriz.

**Formato**

```sql
{ARRAY}.max()
```

**Exemplo**

O query PQL a seguir retorna o preço mais alto de todos os pedidos.

```sql
orders.max(order.price)
```

## Próximas etapas

Agora que você aprendeu sobre funções de agregação, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a [visão geral da linguagem do Query do Perfil](./overview.md).
