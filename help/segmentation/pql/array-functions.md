---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, Serviço de segmentação, pql, PQL, Linguagem de consulta de perfil, funções de matriz, matriz;
solution: Experience Platform
title: Array, List e defina funções PQL
topic-legacy: developer guide
description: A Linguagem de consulta de perfil (PQL) oferece funções para facilitar a interação com arrays, listas e strings.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# Array, list e defina funções

[!DNL Profile Query Language] (PQL) oferece funções para facilitar a interação com arrays, listas e strings. Mais informações sobre outras funções PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Em

A função `in` é usada para determinar se um item é membro de uma matriz ou lista.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Exemplo**

A consulta PQL a seguir define as pessoas com aniversários em março, junho ou setembro.

```sql
person.birthMonth in [3, 6, 9]
```

## Não está em

A função `notIn` é usada para determinar se um item não é membro de uma matriz ou lista.

>[!NOTE]
>
>A função `notIn` *também* garante que nenhum dos valores seja igual a nulo. Portanto, os resultados não são uma negação exata da função `in`.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Exemplo**

A consulta PQL a seguir define pessoas com aniversários que não estejam em março, junho ou setembro.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersetos

A função `intersects` é usada para determinar se duas matrizes ou listas têm pelo menos um membro comum.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Exemplo**

A consulta PQL a seguir define as pessoas cujas cores favoritas incluem pelo menos um vermelho, azul ou verde.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Interseção

A função `intersection` é usada para determinar os membros comuns de duas matrizes ou listas.

**Formato**

```sql
{ARRAY}.intersection({ARRAY})
```

**Exemplo**

A consulta PQL a seguir define se a pessoa 1 e a pessoa 2 têm cores favoritas de vermelho, azul e verde.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subconjunto de

A função `subsetOf` é usada para determinar se uma matriz específica (matriz A) é um subconjunto de outra matriz (matriz B). Em outras palavras, todos os elementos na matriz A são elementos da matriz B.

**Formato**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Exemplo**

A consulta PQL a seguir define as pessoas que visitaram todas as cidades favoritas.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superconjunto de

A função `supersetOf` é usada para determinar se uma matriz específica (matriz A) é um superconjunto de outra matriz (matriz B). Em outras palavras, essa matriz A contém todos os elementos na matriz B.

**Formato**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Exemplo**

A consulta PQL a seguir define as pessoas que comeram sushi e pizza pelo menos uma vez.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Inclui

A função `includes` é usada para determinar se uma matriz ou lista contém um determinado item.

**Formato**

```sql
{ARRAY}.includes({ITEM})
```

**Exemplo**

A consulta PQL a seguir define as pessoas cuja cor favorita inclui o vermelho.

```sql
person.favoriteColors.includes("red")
```

## Distinct

A função `distinct` é usada para remover valores duplicados de uma matriz ou lista.

**Formato**

```sql
{ARRAY}.distinct()
```

**Exemplo**

A consulta PQL a seguir especifica pessoas que fizeram pedidos em mais de um armazenamento.

```sql
person.orders.storeId.distinct().count() > 1
```

## Agrupar por

A função `groupBy` é usada para particionar valores de uma matriz ou lista em um grupo com base no valor da expressão.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argumento | Descrição |
| --------- | ----------- |
| `{ARRAY}` | A matriz ou lista que deve ser agrupada. |
| `{EXPRESSION}` | Uma expressão que mapeia cada item na matriz ou lista retornada. |

**Exemplo**

A consulta PQL a seguir agrupa todos os pedidos pelos quais o pedido foi colocado no armazenamento.

```sql
orders.groupBy(storeId)
```

## Filtro

A função `filter` é usada para filtrar uma matriz ou lista com base em uma expressão.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{ARRAY}` | A matriz ou lista que deve ser filtrada. |
| `{EXPRESSION}` | Uma expressão para filtrar por. |

**Exemplo**

A consulta PQL a seguir define todas as pessoas com 21 anos ou mais.

```sql
person.filter(age >= 21)
```

## Mapa

A função `map` é usada para criar uma nova matriz aplicando uma expressão a cada item em uma matriz específica.

**Formato**

```sql
array.map(expression)
```

**Exemplo**

A consulta PQL a seguir cria uma nova matriz de números e quadrados do valor dos números originais.

```sql
numbers.map(square)
```

## Primeiro `n` na matriz {#first-n}

A função `topN` é usada para retornar os primeiros `N` itens em uma matriz, quando classificada em ordem crescente com base na expressão numérica fornecida.

**Formato**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{ARRAY}` | A matriz ou lista que deve ser classificada. |
| `{VALUE}` | A propriedade na qual classificar a matriz ou lista. |
| `{AMOUNT}` | O número de itens a serem retornados. |

**Exemplo**

A consulta PQL a seguir retorna os cinco principais pedidos com o preço mais alto.

```sql
orders.topN(price, 5)
```

## Último `n` na matriz

A função `bottomN` é usada para retornar os últimos `N` itens em uma matriz, quando classificada em ordem crescente com base na expressão numérica fornecida.

**Formato**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argumento | Descrição |
| --------- | ----------- | 
| `{ARRAY}` | A matriz ou lista que deve ser classificada. |
| `{VALUE}` | A propriedade na qual classificar a matriz ou lista. |
| `{AMOUNT}` | O número de itens a serem retornados. |

**Exemplo**

A consulta PQL a seguir retorna os cinco principais pedidos com o preço mais baixo.

```sql
orders.bottomN(price, 5)
```

## Primeiro item

A função `head` é usada para retornar o primeiro item na matriz ou lista.

**Formato**

```sql
{ARRAY}.head()
```

**Exemplo**

A consulta PQL a seguir retorna o primeiro dos cinco principais pedidos com o preço mais alto. Mais informações sobre a função `topN` podem ser encontradas na seção [first `n` no array](#first-n).

```sql
orders.topN(price, 5).head()
```

## Próximas etapas

Agora que você aprendeu sobre funções de array, lista e conjunto, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a [Visão geral da linguagem de consulta de perfil](./overview.md).
