---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;aggregation functions;aggregation;
solution: Experience Platform
title: Funções de agregação
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 8%

---


# Funções de agregação

As funções de agregação são usadas para agrupar vários valores em matrizes [!DNL Profile Query Language] (PQL) para formar um único valor de resumo. Para obter mais informações sobre outras funções PQL, consulte a [[!DNL Profile Query Language] visão geral](./overview.md).

## Contagem

A `count` função retorna o número de elementos dentro de uma matriz específica.

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

A `sum` função retorna a soma de todos os valores selecionados dentro da matriz.

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

A `average` função retorna a média aritmética de todos os valores selecionados dentro da matriz.

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

A `min` função retorna o menor de todos os valores selecionados dentro da matriz.

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

A `max` função retorna o maior de todos os valores selecionados dentro da matriz.

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

Agora que você aprendeu sobre funções de agregação, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
