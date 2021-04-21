---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; pql; PQL; Idioma da consulta de perfil; funções de agregação; agregação;
solution: Experience Platform
title: Funções de agregação PQL
topic-legacy: developer guide
description: As funções de agregação são usadas para agrupar vários valores em matrizes de Linguagem de consulta de perfil (PQL) para formar um único valor de resumo.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---

# Funções de agregação

As funções de agregação são usadas para agrupar vários valores em matrizes [!DNL Profile Query Language] (PQL) para formar um único valor de resumo. Mais informações sobre outras funções PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Contagem

A função `count` retorna o número de elementos dentro da matriz fornecida.

**Formato**

```sql
{ARRAY}.count()
```

**Exemplo**

A consulta PQL a seguir retorna o número de pedidos na matriz.

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

A consulta PQL a seguir retorna a soma de todos os preços dos pedidos.

```sql
orders.sum(order.price)
```

## Média

A função `average` retorna a média aritmética de todos os valores selecionados dentro da matriz.

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

A função `min` retorna o menor de todos os valores selecionados na matriz.

**Formato**

```sql
{ARRAY}.min()
```

**Exemplo**

A consulta PQL a seguir retorna o preço mais baixo de todos os pedidos.

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

A consulta PQL a seguir retorna o preço mais alto de todos os pedidos.

```sql
orders.max(order.price)
```

## Próximas etapas

Agora que você aprendeu sobre funções de agregação, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a [Visão geral da linguagem de consulta de perfil](./overview.md).
