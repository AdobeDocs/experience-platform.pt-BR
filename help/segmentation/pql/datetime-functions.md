---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções de data e hora
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 4%

---


# Funções de data e hora

As funções de data e hora são usadas para executar operações de data e hora em valores dentro do [!DNL Profile Query Language] (PQL). Para obter mais informações sobre outras funções PQL, consulte a visão geral [do idioma do Query do](./overview.md)Perfil.

## Mês atual

A `currentMonth` função retorna o mês atual como um número inteiro.

**Formato**

```sql
currentMonth()
```

**Exemplo**

O query PQL a seguir verifica se o mês de nascimento da pessoa é o mês atual.

```sql
person.birthMonth = currentMonth()
```

## Obter mês

A `getMonth` função retorna o mês, como um número inteiro, com base em um determinado carimbo de data e hora.

**Formato**

```sql
{TIMESTAMP}.getMonth()
```

**Exemplo**

O query PQL a seguir verifica se o mês de nascimento da pessoa é em junho.

```sql
person.birthdate.getMonth() = 6
```

## Ano atual

A `currentYear` função retorna o ano atual como um número inteiro.

**Formato**

```sql
currentYear()
```

**Exemplo**

O query PQL a seguir verifica se o produto foi vendido no ano atual.

```sql
product.saleYear = currentYear()
```

## Obter ano

A `getYear` função retorna o ano, como um número inteiro, com base em um determinado carimbo de data e hora.

**Formato**

```sql
{TIMESTAMP}.getYear()
```

**Exemplo**

O query PQL a seguir verifica se o ano de nascimento da pessoa ocorre em 1991, 1992, 1993, 1994 ou 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Dia atual do mês

A `currentDayOfMonth` função retorna o dia atual do mês como um número inteiro.

**Formato**

```sql
currentDayOfMonth()
```

**Exemplo**

O query PQL a seguir verifica se o dia de nascimento da pessoa corresponde ao dia atual do mês.

```sql
person.birthDay = currentDayOfMonth()
```

## Obter o dia do mês

A `getDayOfMonth` função retorna o dia, como um número inteiro, com base em um determinado carimbo de data e hora.

**Formato**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Exemplo**

O query PQL a seguir verifica se o item foi vendido nos primeiros 15 dias do mês.

```sql
product.sale.getDayOfMonth() <= 15
```

## Ocorre

A `occurs` função compara a função de carimbo de data e hora fornecida com um período fixo.

**Formato**

A `occurs` função pode ser escrita usando qualquer um dos seguintes formatos:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argumento | Descrição |
| --------- | ----------- |
| `{COMPARISON}` | Um operador de comparação. Pode ser qualquer um dos seguintes operadores: `>`, `>=`, `<`, `<=`, `=`, `!=`. Mais informações sobre as funções de comparação podem ser encontradas no documento [de funções de](./comparison-functions.md)comparação. |
| `{INTEGER}` | Um número inteiro não negativo. |
| `{TIME_UNIT}` | Uma unidade de tempo. Pode ser qualquer uma das seguintes palavras: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries``millennium``millennia`, . |
| `{DIRECTION}` | Uma preposição que descreve quando comparar a data com. Pode ser qualquer uma das seguintes palavras: `before`, `after`, `from`. |
| `{TIME}` | Pode ser um literal de carimbo de data e hora (`today`, `now`, `yesterday`, `tomorrow`), uma unidade de hora relativa (uma de `this`, `last`ou `next` seguida por uma unidade de hora) ou um atributo de carimbo de data e hora. |

>[!NOTE]
>
>O uso da palavra `on` é opcional. Ela está lá para melhorar a legibilidade de algumas combinações, como `timestamp occurs on date(2019,12,31)`.

**Exemplo**

O seguinte query PQL verifica se o item foi vendido na semana passada.

```sql
product.saleDate occurs last week
```

O seguinte query PQL verifica se um item foi vendido entre 8 de janeiro de 2015 e 1 de julho de 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Agora

`now` é uma palavra reservada que representa o carimbo de data e hora da execução de PQL.

**Exemplo**

O query PQL a seguir verifica se um item foi vendido exatamente três horas antes.

```sql
product.saleDate occurs = 3 hours before now
```

## Hoje

`today` é uma palavra reservada que representa o carimbo de data e hora do start do dia de execução do PQL.

**Exemplo**

O query PQL a seguir verifica se o aniversário de uma pessoa foi há três dias.

```sql
person.birthday occurs = 3 days before today
```

## Próximas etapas

Agora que você aprendeu sobre funções de data e hora, é possível usá-las nos query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
