---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções de storage, lista e definição
topic: developer guide
translation-type: tm+mt
source-git-commit: 0fc356b67af4d34e35cd9329385ec284d9336953
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 5%

---


# Funções de storage, lista e definição

[!DNL Profile Query Language] (PQL) O oferta funciona para facilitar a interação com arrays, listas e strings. Para obter mais informações sobre outras funções PQL, consulte a [[!DNL Profile Query Language] visão geral](./overview.md).

## Em

A `in` função é usada para determinar se um item é membro de uma matriz ou lista.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Exemplo**

O seguinte query PQL define pessoas com aniversários em março, junho ou setembro.

```sql
person.birthMonth in [3, 6, 9]
```

## Não está em

A `notIn` função é usada para determinar se um item não é membro de uma matriz ou lista.

>[!NOTE]
>
>A `notIn` função *também* garante que nenhum dos valores seja igual a nulo. Portanto, os resultados não são uma negação exata da `in` função.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Exemplo**

O seguinte query PQL define pessoas com aniversários que não estejam em março, junho ou setembro.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersecções

A `intersects` função é usada para determinar se duas matrizes ou listas têm pelo menos um membro comum.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Exemplo**

O query PQL a seguir define as pessoas cujas cores favoritas incluem pelo menos um de vermelho, azul ou verde.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersecção

A `intersection` função é usada para determinar os membros comuns de duas matrizes ou listas.

**Formato**

```sql
{ARRAY}.intersection({ARRAY})
```

**Exemplo**

O seguinte query PQL define se a pessoa 1 e a pessoa 2 têm cores favoritas de vermelho, azul e verde.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subconjunto de

A `subsetOf` função é usada para determinar se uma matriz específica (matriz A) é um subconjunto de outra matriz (matriz B). Em outras palavras, todos os elementos na matriz A são elementos da matriz B.

**Formato**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Exemplo**

O query PQL a seguir define as pessoas que visitaram todas as cidades favoritas.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superconjunto de

A `supersetOf` função é usada para determinar se uma matriz específica (matriz A) é um superconjunto de outra matriz (matriz B). Em outras palavras, a matriz A contém todos os elementos na matriz B.

**Formato**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Exemplo**

O query PQL a seguir define as pessoas que comeram sushi e pizza pelo menos uma vez.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Inclui

A `includes` função é usada para determinar se uma matriz ou lista contém um determinado item.

**Formato**

```sql
{ARRAY}.includes({ITEM})
```

**Exemplo**

O query PQL a seguir define as pessoas cuja cor favorita inclui o vermelho.

```sql
person.favoriteColors.includes("red")
```

## Distinto

A `distinct` função é usada para remover valores de duplicado de uma matriz ou lista.

**Formato**

```sql
{ARRAY}.distinct()
```

**Exemplo**

O seguinte query PQL especifica pessoas que fizeram pedidos em mais de uma loja.

```sql
person.orders.storeId.distinct().count() > 1
```

## Agrupar por

A `groupBy` função é usada para particionar valores de uma matriz ou lista em um grupo com base no valor da expressão.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argumento | Descrição |
| --------- | ----------- |
| `{ARRAY}` | A matriz ou lista que deve ser agrupada. |
| `{EXPRESSION}` | Uma expressão que mapeia cada item na matriz ou na lista retornada. |

**Exemplo**

O query PQL a seguir agrupa todos os pedidos nos quais o pedido foi armazenado.

```sql
orders.groupBy(storeId)
```

## Filtro

A `filter` função é usada para filtrar uma matriz ou lista com base em uma expressão.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{ARRAY}` | A matriz ou lista que deve ser filtrada. |
| `{EXPRESSION}` | Uma expressão para filtrar. |

**Exemplo**

O seguinte query PQL define todas as pessoas com 21 anos ou mais.

```sql
person.filter(age >= 21)
```

## Mapa

A `map` função é usada para criar uma nova matriz aplicando uma expressão a cada item em uma matriz específica.

**Formato**

```sql
array.map(expression)
```

**Exemplo**

O query PQL a seguir cria uma nova matriz de números e quadra o valor dos números originais.

```sql
numbers.map(square)
```

## Primeiro `n` no array {#first-n}

A `topN` função é usada para retornar os primeiros `N` itens em uma matriz, quando classificada em ordem crescente com base na expressão numérica fornecida.

**Formato**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{ARRAY}` | A matriz ou lista que deve ser classificada. |
| `{VALUE}` | A propriedade na qual classificar a matriz ou a lista. |
| `{AMOUNT}` | O número de itens a serem retornados. |

**Exemplo**

O seguinte query PQL retorna os cinco pedidos principais com o preço mais alto.

```sql
orders.topN(price, 5)
```

## Últimos `n` na matriz

A `bottomN` função é usada para retornar os últimos `N` itens em uma matriz, quando classificada em ordem crescente com base na expressão numérica fornecida.

**Formato**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argumento | Descrição |
| --------- | ----------- | 
| `{ARRAY}` | A matriz ou lista que deve ser classificada. |
| `{VALUE}` | A propriedade na qual classificar a matriz ou a lista. |
| `{AMOUNT}` | O número de itens a serem retornados. |

**Exemplo**

O seguinte query PQL retorna os cinco pedidos principais com o preço mais baixo.

```sql
orders.bottomN(price, 5)
```

## Primeiro item

A `head` função é usada para retornar o primeiro item na matriz ou na lista.

**Formato**

```sql
{ARRAY}.head()
```

**Exemplo**

O seguinte query PQL retorna o primeiro dos cinco pedidos principais com o preço mais alto. Mais informações sobre a `topN` função podem ser encontradas na [primeira `n` seção da matriz](#first-n) .

```sql
orders.topN(price, 5).head()
```

## Próximas etapas

Agora que você aprendeu sobre o array, a lista e as funções definidas, é possível usá-las nos query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
