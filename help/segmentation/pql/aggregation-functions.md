---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções de agregação
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 8%

---


# Funções de agregação

As funções de agregação são usadas para agrupar vários valores em matrizes [!DNL Profile Query Language] (PQL) para formar um único valor de resumo. Para obter mais informações sobre outras funções PQL, consulte a visão geral [do idioma do Query do](./overview.md)Perfil.

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
