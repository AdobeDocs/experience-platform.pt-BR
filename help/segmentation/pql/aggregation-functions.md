---
solution: Experience Platform
title: Funções de agregação do PQL
description: As funções de agregação são usadas para agrupar vários valores em arrays Profile Query Language (PQL) para formar um único valor de resumo.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---

# Funções de agregação

As funções de agregação são usadas para agrupar vários valores em matrizes [!DNL Profile Query Language] (PQL) para formar um único valor de resumo. Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Contagem

A função `count` retorna o número de elementos dentro da matriz especificada como um número.

**Formato**

```sql
{ARRAY}.count()
```

**Exemplo**

A consulta do PQL a seguir retorna o número de pedidos na matriz.

```sql
orders.count()
```

## Somar

A função `sum` retorna a soma de todos os valores selecionados na matriz como um número.

**Formato**

```sql
{ARRAY}.sum()
```

**Exemplo**

A consulta do PQL a seguir retorna a soma de todos os preços dos pedidos.

```sql
orders.sum(order.price)
```

## Média

A função `average` retorna a média aritmética de todos os valores selecionados na matriz como um número.

**Formato**

```sql
{ARRAY}.average()
```

**Exemplo**

A consulta PQL a seguir retorna o preço médio de todos os pedidos.

```sql
orders.average(order.price)
```

## Mínimo

A função `min` retorna o menor valor dentro da matriz como um número.

**Formato**

```sql
{ARRAY}.min()
```

**Exemplo**

A consulta do PQL a seguir retorna o preço mais baixo de todas as ordens.

```sql
orders.min(order.price)
```

## Máximo

A função `max` retorna o maior valor dentro da matriz como um número.

**Formato**

```sql
{ARRAY}.max()
```

**Exemplo**

A consulta do PQL a seguir retorna o preço mais alto de todas as ordens.

```sql
orders.max(order.price)
```

## Próximas etapas

Agora que você aprendeu sobre funções de agregação, pode usá-las em queries do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
