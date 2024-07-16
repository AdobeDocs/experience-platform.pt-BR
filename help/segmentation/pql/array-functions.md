---
solution: Experience Platform
title: Funções de matriz, lista e definição do PQL
description: O Profile Query Language (PQL) oferece funções para facilitar a interação com matrizes, listas e strings.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 4%

---

# Funções de matriz, lista e definição

O [!DNL Profile Query Language] (PQL) oferece funções para facilitar a interação com matrizes, listas e cadeias de caracteres. Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Em

A função `in` é usada para determinar se um item é membro de uma matriz ou lista.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Exemplo**

A consulta do PQL a seguir define as pessoas com aniversários em março, junho ou setembro.

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

O query do PQL a seguir define as pessoas com aniversários que não são em março, junho ou setembro.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersecta

A função `intersects` é usada para determinar se duas matrizes ou listas têm pelo menos um membro comum.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Exemplo**

A seguinte query do PQL define as pessoas cujas cores favoritas incluem pelo menos uma das cores vermelha, azul ou verde.

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

A seguinte consulta do PQL define se a pessoa 1 e a pessoa 2 têm cores favoritas de vermelho, azul e verde.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subconjunto de

A função `subsetOf` é usada para determinar se uma matriz específica (matriz A) é um subconjunto de outra matriz (matriz B). Em outras palavras, que todos os elementos na matriz A são elementos da matriz B.

**Formato**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Exemplo**

O query do PQL a seguir define as pessoas que visitaram todas as cidades favoritas.

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

A consulta do PQL a seguir define as pessoas que comeram sushi e pizza pelo menos uma vez.

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

A seguinte query do PQL define as pessoas cuja cor favorita inclui vermelho.

```sql
person.favoriteColors.includes("red")
```

## Distinto

A função `distinct` é usada para remover valores duplicados de uma matriz ou lista.

**Formato**

```sql
{ARRAY}.distinct()
```

**Exemplo**

A consulta do PQL a seguir especifica as pessoas que fizeram pedidos em mais de uma loja.

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

A consulta do PQL a seguir agrupa todas as ordens pelas quais a ordem foi armazenada.

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
| `{EXPRESSION}` | Uma expressão pela qual filtrar. |

**Exemplo**

A consulta do PQL a seguir define todas as pessoas com 21 anos ou mais.

```sql
person.filter(age >= 21)
```

## Mapa

A função `map` é usada para criar uma nova matriz aplicando uma expressão a cada item em uma determinada matriz.

**Formato**

```sql
array.map(expression)
```

**Exemplo**

A consulta PQL a seguir cria uma nova matriz de números e eleva ao quadrado o valor dos números originais.

```sql
numbers.map(square)
```

## Primeiro `n` na matriz {#first-n}

A função `topN` é usada para retornar os primeiros `N` itens em uma matriz, quando classificados em ordem crescente com base na expressão numérica fornecida.

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

A consulta do PQL a seguir retorna as cinco principais ordens com o preço mais alto.

```sql
orders.topN(price, 5)
```

## Último `n` na matriz

A função `bottomN` é usada para retornar os últimos `N` itens em uma matriz, quando classificados em ordem crescente com base na expressão numérica fornecida.

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

A consulta do PQL a seguir retorna as cinco principais ordens com o preço mais baixo.

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

A consulta PQL a seguir retorna o primeiro dos cinco pedidos principais com o preço mais alto. Mais informações sobre a função `topN` podem ser encontradas na [primeira `n` da seção de matriz](#first-n).

```sql
orders.topN(price, 5).head()
```

## Próximas etapas

Agora que você aprendeu sobre as funções de matriz, lista e conjunto, é possível usá-las nas queries do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
