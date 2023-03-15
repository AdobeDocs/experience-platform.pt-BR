---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Profile Query Language;date and time functions;datetime functions;datetime;date;time;
solution: Experience Platform
title: Funções de data e hora PQL
description: As funções de data e hora são usadas para executar operações de data e hora em valores no Idioma de consulta de perfil (PQL).
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 4%

---

# Funções de data e hora

As funções de data e hora são usadas para executar operações de data e hora em valores dentro do [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Mês atual

A variável `currentMonth` A função retorna o mês atual como um número inteiro.

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

A variável `getMonth` A função retorna o mês como um número inteiro, com base em um determinado carimbo de data e hora.

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

A variável `currentYear` A função retorna o ano atual como um número inteiro.

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

A variável `getYear` A função retorna o ano como um número inteiro, com base em um determinado carimbo de data e hora.

**Formato**

```sql
{TIMESTAMP}.getYear()
```

**Exemplo**

A consulta PQL a seguir verifica se o ano de nascimento da pessoa ocorre em 1991, 1992, 1993, 1994 ou 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Dia do mês atual

A variável `currentDayOfMonth` A função retorna o dia atual do mês como um número inteiro.

**Formato**

```sql
currentDayOfMonth()
```

**Exemplo**

A consulta PQL a seguir verifica se o dia de nascimento da pessoa corresponde ao dia atual do mês.

```sql
person.birthDay = currentDayOfMonth()
```

## Obter dia do mês

A variável `getDayOfMonth` A função retorna o dia, como um número inteiro, com base em um determinado carimbo de data e hora.

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

A variável `occurs` A função compara a função de carimbo de data e hora fornecida com um período de tempo fixo.

**Formato**

A variável `occurs` pode ser gravada usando qualquer um dos seguintes formatos:

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
| `{DIRECTION}` | Uma preposição que descreve quando comparar a data com. Pode ser qualquer uma das seguintes palavras: `before`, `after`, `from`. |
| `{TIME}` | Pode ser um caractere de data e hora literal (`today`, `now`, `yesterday`, `tomorrow`), uma unidade de tempo relativa (uma de `this`, `last`ou `next` seguido por uma unidade de tempo) ou um atributo de carimbo de data e hora. |

>[!NOTE]
>
>Uso da palavra `on` é opcional. Isso melhora a legibilidade de algumas combinações, como `timestamp occurs on date(2019,12,31)`.

**Exemplo**

A consulta PQL a seguir verifica se o item foi vendido na semana passada.

```sql
product.saleDate occurs last week
```

A consulta PQL a seguir verifica se um item foi vendido entre 8 de janeiro de 2015 e 1º de julho de 2017.

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

`today` é uma palavra reservada que representa o carimbo de data e hora do início do dia da execução do PQL.

**Exemplo**

A consulta PQL a seguir verifica se o aniversário de uma pessoa foi há três dias.

```sql
person.birthday occurs = 3 days before today
```

## Próximas etapas

Agora que você aprendeu sobre funções de data e hora, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
