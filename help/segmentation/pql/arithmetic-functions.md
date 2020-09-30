---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;arithmetic functions;arithmetic;
solution: Experience Platform
title: Funções aritméticas
topic: developer guide
description: As funções aritméticas são usadas para executar cálculos básicos em valores em Linguagem do Query do Perfil (PQL).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---


# Funções aritméticas

As funções aritméticas são usadas para executar cálculos básicos em valores em [!DNL Profile Query Language] (PQL). Para obter mais informações sobre outras funções PQL, consulte a [[!DNL Profile Query Language] visão geral](./overview.md).

## Add

A função `+` (adição) é usada para localizar a soma de duas expressões de argumento.

**Formato**

```sql
{NUMBER} + {NUMBER}
```

**Exemplo**

O query PQL a seguir resume o preço de dois produtos diferentes.

```sql
product1.price + product2.price
```

## Multiplicar

A função `*` (multiplicação) é usada para encontrar o produto de duas expressões de argumento.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Exemplo**

O seguinte query PQL localiza o produto do inventário e o preço de um produto para localizar o valor bruto do produto.

```sql
product.inventory * product.price
```

## Subtrair

A função `-` (subtração) é usada para encontrar a diferença de duas expressões de argumento.

**Formato**

```sql
{NUMBER} - {NUMBER}
```

**Exemplo**

O query PQL a seguir encontra a diferença de preço entre dois produtos diferentes.

```sql
product1.price - product2.price
```

## Dividir

A função `/` (divisão) é usada para encontrar o quociente de duas expressões de argumento.

**Formato**

```sql
{NUMBER} / {NUMBER}
```

**Exemplo**

O query PQL a seguir encontra o quociente entre o total de produtos vendidos e o total de dinheiro ganho para ver o custo médio por item.

```sql
totalProduct.price / totalProduct.sold
```

## Restante

A função `%` (modulo/restante) é usada para localizar o restante após dividir as duas expressões de argumento.

**Formato**

```sql
{NUMBER} % {NUMBER}
```

**Exemplo**

O query PQL a seguir verifica se a idade da pessoa é divisível por cinco.

```sql
person.age % 5 = 0
```

## Próximas etapas

Agora que você aprendeu sobre funções aritméticas, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
