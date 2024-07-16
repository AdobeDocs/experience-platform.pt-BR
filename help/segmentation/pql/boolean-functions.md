---
solution: Experience Platform
title: Funções booleanas do PQL
description: Funções booleanas são usadas para executar lógica booleana em diferentes elementos no Profile Query Language (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 4%

---

# Funções booleanas

Funções booleanas são usadas para executar lógica booleana em diferentes elementos em [!DNL Profile Query Language] (PQL).  Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## E

A função `and` é usada para criar uma conjunção lógica.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Exemplo**

A consulta do PQL a seguir retornará todas as pessoas com o país de origem como Canadá e o ano de nascimento de 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Ou

A função `or` é usada para criar uma disjunção lógica.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Exemplo**

A consulta do PQL a seguir retornará todas as pessoas com o país de origem como Canadá ou ano de nascimento de 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Não

A função `not` (ou `!`) é usada para criar uma negação lógica.

**Formato**

```sql
not ({QUERY})
!({QUERY})
```

**Exemplo**

A seguinte query do PQL retornará todas as pessoas que não têm seu país de origem como Canadá.

```sql
not (homeAddress.countryISO = "CA")
```

## Se

A função `if` é usada para resolver uma expressão dependendo se uma condição especificada é verdadeira.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | A expressão booleana que está sendo testada. |
| `{TRUE_EXPRESSION}` | A expressão cujo valor será usado se `{TEST_EXPRESSION}` for verdadeiro. |
| `{FALSE_EXPRESSION}` | A expressão cujo valor será usado se `{TEST_EXPRESSION}` for falso. |

**Exemplo**

A consulta PQL a seguir definirá o valor como `1` se o país de origem for o Canadá e `2` se o país de origem não for o Canadá.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Próximas etapas

Agora que você aprendeu sobre funções booleanas, é possível usá-las em consultas do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
