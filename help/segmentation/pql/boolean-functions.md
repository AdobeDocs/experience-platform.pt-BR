---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções booleanas
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# Funções booleanas

As funções booleanas são usadas para executar lógica booleana em diferentes elementos no [!DNL Profile Query Language] (PQL).  Para obter mais informações sobre outras funções PQL, consulte a [[!DNL Profile Query Language] visão geral](./overview.md).

## E

A `and` função é usada para criar uma conjunção lógica.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Exemplo**

O query PQL a seguir retornará todas as pessoas com o país de origem como Canadá e o ano de nascimento de 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Ou

A `or` função é usada para criar uma disjunção lógica.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Exemplo**

O query PQL a seguir retornará todas as pessoas com o país de origem como Canadá ou o ano de nascimento de 1985.

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

O query PQL a seguir retornará todas as pessoas que não têm seu país de origem como Canadá.

```sql
not (homeAddress.countryISO = "CA")
```

## Se

A `if` função é usada para resolver uma expressão, dependendo se uma condição especificada é verdadeira.

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

O query PQL a seguir definirá o valor como `1` se o país de origem fosse o Canadá e `2` se o país de origem não fosse o Canadá.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Próximas etapas

Agora que você aprendeu sobre funções booleanas, pode usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
