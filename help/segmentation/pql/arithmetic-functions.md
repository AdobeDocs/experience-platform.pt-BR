---
solution: Experience Platform
title: Funções aritméticas PAL
description: Funções aritméticas são usadas para realizar cálculos básicos em valores no Profile Query Language (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---

# Funções aritméticas

Funções aritméticas são usadas para realizar cálculos básicos em valores em [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Add

A função `+` (adição) é usada para localizar a soma de duas expressões de argumento como um número.

**Formato**

```sql
{NUMBER} + {NUMBER}
```

**Exemplo**

A consulta do PQL a seguir soma o preço de dois produtos diferentes.

```sql
product1.price + product2.price
```

## Multiplicar

A função `*` (multiplicação) é usada para localizar o produto de duas expressões de argumento como um número.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Exemplo**

A consulta PQL a seguir localiza o produto do estoque e o preço de um produto para localizar o valor bruto do produto.

```sql
product.inventory * product.price
```

## Subtrair

A função `-` (subtração) é usada para localizar a diferença de duas expressões de argumento como um número.

**Formato**

```sql
{NUMBER} - {NUMBER}
```

**Exemplo**

A consulta do PQL a seguir encontra a diferença de preço entre dois produtos diferentes.

```sql
product1.price - product2.price
```

## Divisão

A função `/` (divisão) é usada para localizar o quociente de duas expressões de argumento como um número.

**Formato**

```sql
{NUMBER} / {NUMBER}
```

**Exemplo**

A consulta PQL a seguir encontra o quociente entre o total de produtos vendidos e o dinheiro total ganho para ver o custo médio por item.

```sql
totalProduct.price / totalProduct.sold
```

## Restante

A função `%` (módulo/restante) é usada para localizar o restante após dividir as duas expressões de argumento como um número.

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

Agora que você aprendeu sobre funções aritméticas, é possível usá-las em queries do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
