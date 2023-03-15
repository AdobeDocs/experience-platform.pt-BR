---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Profile Query Language;array functions;array;
solution: Experience Platform
title: Funções Array, List e Set PQL
description: A Profile Query Language (PQL) oferece funções para facilitar a interação com matrizes, listas e strings.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# Funções de matriz, lista e definição

[!DNL Profile Query Language] O (PQL) oferece funções para facilitar a interação com matrizes, listas e strings. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Em

A variável `in` é usada para determinar se um item é membro de uma matriz ou lista.

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

A variável `notIn` é usada para determinar se um item não é membro de uma matriz ou lista.

>[!NOTE]
>
>A variável `notIn` função *também* garante que nenhum dos valores seja igual a nulo. Portanto, os resultados não são uma negação exata do `in` função.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Exemplo**

A consulta PQL a seguir define as pessoas com aniversários que não estão em março, junho ou setembro.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Interseta

A variável `intersects` é usada para determinar se duas matrizes ou listas têm pelo menos um membro comum.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Exemplo**

A consulta PQL a seguir define as pessoas cujas cores favoritas incluem pelo menos uma das cores vermelha, azul ou verde.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersecção

A variável `intersection` é usada para determinar os membros comuns de duas matrizes ou listas.

**Formato**

```sql
{ARRAY}.intersection({ARRAY})
```

**Exemplo**

A seguinte consulta PQL define se a pessoa 1 e a pessoa 2 têm cores favoritas de vermelho, azul e verde.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subconjunto de

A variável `subsetOf` é usada para determinar se uma matriz específica (matriz A) é um subconjunto de outra matriz (matriz B). Em outras palavras, que todos os elementos na matriz A são elementos da matriz B.

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

A variável `supersetOf` é usada para determinar se uma matriz específica (matriz A) é um superconjunto de outra matriz (matriz B). Em outras palavras, essa matriz A contém todos os elementos na matriz B.

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

A variável `includes` é usada para determinar se uma matriz ou lista contém um determinado item.

**Formato**

```sql
{ARRAY}.includes({ITEM})
```

**Exemplo**

A consulta PQL a seguir define as pessoas cujas cores favoritas incluem vermelho.

```sql
person.favoriteColors.includes("red")
```

## Distinto

A variável `distinct` é usada para remover valores duplicados de uma matriz ou lista.

**Formato**

```sql
{ARRAY}.distinct()
```

**Exemplo**

A consulta PQL a seguir especifica as pessoas que fizeram pedidos em mais de uma loja.

```sql
person.orders.storeId.distinct().count() > 1
```

## Agrupar por

A variável `groupBy` é usada para particionar valores de uma matriz ou lista em um grupo com base no valor da expressão.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argumento | Descrição |
| --------- | ----------- |
| `{ARRAY}` | A matriz ou lista que deve ser agrupada. |
| `{EXPRESSION}` | Uma expressão que mapeia cada item na matriz ou lista retornada. |

**Exemplo**

A consulta PQL a seguir agrupa todas as ordens pelas quais a ordem foi armazenada.

```sql
orders.groupBy(storeId)
```

## Filtro

A variável `filter` é usada para filtrar uma matriz ou lista com base em uma expressão.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{ARRAY}` | A matriz ou lista que deve ser filtrada. |
| `{EXPRESSION}` | Uma expressão pela qual filtrar. |

**Exemplo**

A consulta PQL a seguir define todas as pessoas com 21 anos ou mais.

```sql
person.filter(age >= 21)
```

## Mapa

A variável `map` Esta função é usada para criar uma nova matriz aplicando uma expressão a cada item em uma determinada matriz.

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

A variável `topN` é usada para retornar a primeira `N` itens em uma matriz, quando classificados em ordem crescente com base na expressão numérica fornecida.

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

A consulta PQL a seguir retorna as cinco principais ordens com o preço mais alto.

```sql
orders.topN(price, 5)
```

## Último `n` na matriz

A variável `bottomN` é usada para retornar a última `N` itens em uma matriz, quando classificados em ordem crescente com base na expressão numérica fornecida.

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

A consulta PQL a seguir retorna as cinco principais ordens com o preço mais baixo.

```sql
orders.bottomN(price, 5)
```

## Primeiro item

A variável `head` é usada para retornar o primeiro item na matriz ou lista.

**Formato**

```sql
{ARRAY}.head()
```

**Exemplo**

A consulta PQL a seguir retorna a primeira das cinco principais ordens com o preço mais alto. Mais informações sobre o `topN` pode ser encontrada na variável [primeiro `n` na matriz](#first-n) seção.

```sql
orders.topN(price, 5).head()
```

## Próximas etapas

Agora que você aprendeu sobre as funções de matriz, lista e conjunto, é possível usá-las nas consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
