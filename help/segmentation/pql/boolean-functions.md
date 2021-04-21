---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; pql; PQL; Idioma de consulta de perfil; funções booleanas; booleano;
solution: Experience Platform
title: Funções booleanas PQL
topic-legacy: developer guide
description: As funções booleanas são usadas para executar a lógica booleana em elementos diferentes na linguagem de consulta de perfil (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# Funções booleanas

As funções booleanas são usadas para executar lógica booleana em elementos diferentes em [!DNL Profile Query Language] (PQL).  Mais informações sobre outras funções PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## E

A função `and` é usada para criar uma conjunção lógica.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Exemplo**

A consulta PQL a seguir retornará todas as pessoas com o país de origem como Canadá e o ano de nascimento de 1985.

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

A consulta PQL a seguir retornará todas as pessoas com o país de origem como Canadá ou o ano de nascimento de 1985.

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

A consulta PQL a seguir retornará todas as pessoas que não têm o país de origem como o Canadá.

```sql
not (homeAddress.countryISO = "CA")
```

## Se

A função `if` é usada para resolver uma expressão dependendo de se uma condição especificada é verdadeira.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | A expressão booleana que está sendo testada. |
| `{TRUE_EXPRESSION}` | A expressão cujo valor será usado se `{TEST_EXPRESSION}` for true. |
| `{FALSE_EXPRESSION}` | A expressão cujo valor será usado se `{TEST_EXPRESSION}` for false. |

**Exemplo**

A consulta PQL a seguir definirá o valor como `1` se o país de origem for o Canadá e `2` se o país de origem não for o Canadá.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Próximas etapas

Agora que você aprendeu sobre funções booleanas, pode usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a [Visão geral da linguagem de consulta de perfil](./overview.md).
