---
keywords: Experience Platform;página inicial;tópicos populares;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia de interface do usuário;mapeador;mapeamento;preparação de dados;preparação de dados;
solution: Experience Platform
title: Manuseio de formatos de dados com o Preparo de dados
description: Este documento fornece uma visão geral de como diferentes tipos de dados são tratados no Preparo de dados.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# Manuseio de formatos de dados com o Preparo de dados

O Preparo de dados pode lidar com diferentes formatos de dados assimilados na Adobe Experience Platform. Este documento descreve como diferentes formatos de dados são tratados com o Preparo de dados.

## Booleanos {#booleans}

Se o tipo de origem for uma string e o tipo de destino for um booleano, o Preparo de dados poderá analisar automaticamente o valor e converter o valor de origem em um booleano.

Os valores `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true`, e `TRUE` são automaticamente analisadas para serem `true`.

Os valores `n`, `N`, `no`, `NO`, `off`, `OFF`, `false`, e `FALSE` são automaticamente analisadas para serem `false`.

## Datas {#dates}

O Preparo de dados é compatível com funções de data, como cadeias de caracteres e como objetos de data e hora.

### Formato de função de data

A função de data converte strings e objetos datetime em um objeto ZonedDateTime com formato ISO 8601.

**Formato**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATE}` | Obrigatório. A cadeia de caracteres que representa a data. |
| `{FORMAT}` | Opcional. A cadeia de caracteres que representa o formato da data de origem. Mais informações sobre a formatação de cadeias de caracteres podem ser encontradas no [seção de cadeia de caracteres de formato de data/hora](#format). |
| `{DEFAULT_DATE}` | Opcional. A data padrão a ser retornada se a data fornecida for nula. |

Por exemplo, a expressão `date(orderDate, "yyyy-MM-dd")` converterá um `orderDate` valor de &quot;31 de dezembro de 2020&quot; em um valor datetime de &quot;31-12-2020&quot;.

### Conversões da função de data

Quando os campos de sequência de caracteres dos dados recebidos são mapeados para campos de data em esquemas que usam o Experience Data Model (XDM), o formato de data deve ser explicitamente mencionado. Se não for mencionado explicitamente, o Preparo de dados tentará converter os dados de entrada correspondendo-os aos seguintes formatos. Depois que um formato correspondente for encontrado, ele deixará de avaliar quaisquer formatos subsequentes.

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> O Preparo de dados tentará converter cadeias de caracteres em datas o melhor possível. No entanto, essas conversões podem levar a resultados indesejáveis. Por exemplo, o valor da string &quot;12112020&quot; corresponde ao padrão &quot;DDaaaa&quot;, mas o usuário pode ter pretendido que a data fosse lida com o padrão &quot;DDaaaa&quot;. Como resultado, os usuários devem mencionar explicitamente o formato de data para as cadeias de caracteres.

### Cadeias de caracteres de formato de data/hora {#format}

A tabela a seguir mostra quais letras do padrão são definidas para cadeias de caracteres de formato. Observe que as letras diferenciam maiúsculas de minúsculas.

| Símbolo | Significado | Apresentação | Exemplo |
| ------ | ------- | ------------ | ------- |
| G | A era | Texto | AD; Anno Domini; A |
| Y | Ano, com base na Semana ISO | Número | 1996; 96 |
| y | O ano | Número | 2004; 04 |
| M/L | Mês do ano | Número/Texto | 7; 07; Jul; Julho; J |
| w | Semana do ano | Número | 27 |
| W | Semana do mês | Número | 3 |
| D | Dia do ano | Número | 189 |
| d | Dia do mês | Número | 10 |
| F | Dia da semana em um mês | Número | 2 |
| E | Nome do dia da semana | Texto | Terça-feira; Ter |
| u | Dia da semana, em número. 1 representa segunda-feira, ..., 7 representa domingo | Número | 1 |
| a | Marcador AM/PM | Texto | PM |
| H | Hora do dia (0-23) | Número | 0 |
| k | Hora do dia (1-24) | Número | 24 |
|  mil | Hora em AM/PM (0-11) | Número | 0 |
| h | Hora em AM/PM (1-12) | Número | 12 |
| m | Minuto na hora | Número | 38 |
| s | Segundo no minuto | Número | 44 |
| S | Milissegundo | Número | 245 |
| z | Fuso horário | Fuso horário geral | Horário Padrão do Pacífico; PST; GMT-08:00 |
| Z | Fuso horário | Fuso horário RFC 822 | -0800 |
| X | Fuso horário | Fuso horário ISO 8601 | -08; -0800; -08:00 |
| V | ID do fuso horário | Texto | América/Los_Angeles |
| O | Deslocamento de fuso horário | Texto | GMT+8 |
| Q/q | Trimestre do ano | Número/Texto | 3; 03; T3; 3º trimestre |

## Mapas {#maps}

No momento, os mapas não são compatíveis com o [!DNL Data Prep].
