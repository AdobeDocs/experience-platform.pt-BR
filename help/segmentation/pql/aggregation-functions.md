---
solution: Experience Platform
title: Funções de Agregação PQL
description: As funções de agregação são usadas para agrupar vários valores em matrizes de Idioma de consulta de perfil (PQL) para formar um único valor de resumo.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 8%

---

# Funções de agregação

As funções de agregação são usadas para agrupar vários valores em [!DNL Profile Query Language] arrays (PQL) para formar um único valor de resumo. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Contagem

A variável `count` A função retorna o número de elementos dentro da matriz especificada.

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

A variável `sum` Esta função retorna a soma de todos os valores selecionados na matriz.

**Formato**

```sql
{ARRAY}.sum()
```

**Exemplo**

A consulta PQL a seguir retorna a soma de todos os preços das ordens.

```sql
orders.sum(order.price)
```

## Média

A variável `average` Esta função retorna a média aritmética de todos os valores selecionados dentro da matriz.

**Formato**

```sql
{ARRAY}.average()
```

**Exemplo**

A consulta PQL a seguir retorna o preço médio de todas as ordens.

```sql
orders.average(order.price)
```

## Mínimo

A variável `min` Esta função retorna o menor valor dentro da matriz.

**Formato**

```sql
{ARRAY}.min()
```

**Exemplo**

A consulta PQL a seguir retorna o preço mais baixo de todas as ordens.

```sql
orders.min(order.price)
```

## Máximo

A variável `max` Esta função retorna o maior valor dentro da matriz.

**Formato**

```sql
{ARRAY}.max()
```

**Exemplo**

A consulta PQL a seguir retorna o preço mais alto de todas as ordens.

```sql
orders.max(order.price)
```

## Próximas etapas

Agora que você aprendeu sobre funções de agregação, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
