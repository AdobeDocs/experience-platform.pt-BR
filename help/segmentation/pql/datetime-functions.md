---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de Segmentação; pql; PQL; Idioma de Consulta de Perfil; funções de data e hora; funções de data e hora; datetime; data; hora;
solution: Experience Platform
title: Funções de Data e Hora do PQL
topic-legacy: developer guide
description: As funções de data e hora são usadas para executar operações de data e hora em valores dentro do PQL (Profile Query Language).
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 4%

---

# Funções de data e hora

As funções de data e hora são usadas para executar operações de data e hora em valores dentro de [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Mês atual

A função `currentMonth` retorna o mês atual como um número inteiro.

**Formato**

```sql
currentMonth()
```

**Exemplo**

A consulta PQL a seguir verifica se o mês de nascimento da pessoa é o mês atual.

```sql
person.birthMonth = currentMonth()
```

## Obter mês

A função `getMonth` retorna o mês, como um número inteiro, com base em um determinado carimbo de data e hora.

**Formato**

```sql
{TIMESTAMP}.getMonth()
```

**Exemplo**

A consulta PQL a seguir verifica se o mês de nascimento da pessoa é em junho.

```sql
person.birthdate.getMonth() = 6
```

## Ano atual

A função `currentYear` retorna o ano atual como um número inteiro.

**Formato**

```sql
currentYear()
```

**Exemplo**

A consulta PQL a seguir verifica se o produto foi vendido no ano atual.

```sql
product.saleYear = currentYear()
```

## Obter ano

A função `getYear` retorna o ano, como um número inteiro, com base em um determinado carimbo de data e hora.

**Formato**

```sql
{TIMESTAMP}.getYear()
```

**Exemplo**

A consulta PQL a seguir verifica se o ano de nascimento da pessoa é 1991, 1992, 1993, 1994 ou 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Dia atual do mês

A função `currentDayOfMonth` retorna o dia atual do mês como um número inteiro.

**Formato**

```sql
currentDayOfMonth()
```

**Exemplo**

A consulta PQL a seguir verifica se o dia de nascimento da pessoa corresponde ao dia atual do mês.

```sql
person.birthDay = currentDayOfMonth()
```

## Obter o dia do mês

A função `getDayOfMonth` retorna o dia, como um número inteiro, com base em um determinado carimbo de data e hora.

**Formato**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Exemplo**

A consulta PQL a seguir verifica se o item foi vendido nos primeiros 15 dias do mês.

```sql
product.sale.getDayOfMonth() <= 15
```

## Ocorre

A função `occurs` compara a função de carimbo de data e hora fornecida com um período fixo.

**Formato**

A função `occurs` pode ser gravada usando qualquer um dos formatos a seguir:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argumento | Descrição |
| --------- | ----------- |
| `{COMPARISON}` | Um operador de comparação. Pode ser qualquer um dos seguintes operadores: `>`, `>=`, `<`, `<=`, `=`, `!=`. Mais informações sobre as funções de comparação podem ser encontradas no [documento de funções de comparação](./comparison-functions.md). |
| `{INTEGER}` | Um inteiro não negativo. |
| `{TIME_UNIT}` | Uma unidade de tempo. Pode ser qualquer uma das seguintes palavras: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | Uma apresentação descrevendo quando comparar a data com. Pode ser qualquer uma das seguintes palavras: `before`, `after`, `from`. |
| `{TIME}` | Pode ser um literal de carimbo de data e hora (`today`, `now`, `yesterday`, `tomorrow`), uma unidade de hora relativa (um de `this`, `last` ou `next` seguido por uma unidade de hora) ou um atributo de carimbo de data e hora. |

>[!NOTE]
>
>O uso da palavra `on` é opcional. Ele está lá para melhorar a legibilidade de algumas combinações, como `timestamp occurs on date(2019,12,31)`.

**Exemplo**

A consulta PQL a seguir verifica se o item foi vendido na semana passada.

```sql
product.saleDate occurs last week
```

A consulta PQL a seguir verifica se um item foi vendido entre 8 de janeiro de 2015 e 1 de julho de 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Agora

`now` é uma palavra reservada que representa o carimbo de data e hora da execução de PQL.

**Exemplo**

A consulta PQL a seguir verifica se um item foi vendido exatamente três horas antes.

```sql
product.saleDate occurs = 3 hours before now
```

## Hoje

`today` é uma palavra reservada que representa o carimbo de data e hora do início do dia de execução do PQL.

**Exemplo**

A consulta PQL a seguir verifica se o aniversário de uma pessoa foi de três dias atrás.

```sql
person.birthday occurs = 3 days before today
```

## Próximas etapas

Agora que você aprendeu sobre as funções de data e hora, é possível usá-las em queries PQL. Para obter mais informações sobre outras funções PQL, leia a [Visão geral da linguagem de consulta de perfil](./overview.md).
