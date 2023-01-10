---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; pql; PQL; Idioma da consulta de perfil; funções de agregação; agregação;
solution: Experience Platform
title: Funções de agregação PQL
description: As funções de agregação são usadas para agrupar vários valores em matrizes de Linguagem de consulta de perfil (PQL) para formar um único valor de resumo.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 7%

---

# Funções de agregação

As funções de agregação são usadas para agrupar vários valores em [!DNL Profile Query Language] Matrizes (PQL) para formar um único valor de resumo. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Contagem

O `count` retorna o número de elementos dentro de uma matriz específica.

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

O `sum` retorna a soma de todos os valores selecionados na matriz.

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

O `average` retorna a média aritmética de todos os valores selecionados na matriz.

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

O `min` retorna o menor de todos os valores selecionados na matriz.

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

O `max` retorna o maior de todos os valores selecionados na matriz.

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

Agora que você aprendeu sobre funções de agregação, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a seção [Visão geral do idioma de consulta do perfil](./overview.md).
