---
keywords: Experience Platform; home; tópicos populares; mapear csv; mapear arquivo csv; mapear arquivo csv para xdm; mapear csv para xdm; guia da interface do usuário; mapeador; mapeamento; preparação de dados; preparação de dados;
solution: Experience Platform
title: Manuseio de formatos de dados com Preparação de dados
topic: visão geral
description: Este documento fornece uma visão geral de como diferentes tipos de dados são tratados na Preparação de dados.
translation-type: tm+mt
source-git-commit: 41656d204f7227388ee1a0a7cad01f737fb96c4f
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 13%

---


# Manuseio de formatos de dados com Preparação de dados

A Preparação de dados pode lidar de forma robusta com diferentes formatos de dados assimilados no Adobe Experience Platform. Este documento descreve como os diferentes formatos de dados são tratados com a Preparação de Dados.

## Booleanos {#booleans}

Se o tipo de origem for uma string e o tipo de destino for um booleano, a Preparação de Dados poderá analisar automaticamente o valor e converter o valor de origem em um booleano.

Os valores `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true` e `TRUE` são analisados automaticamente para serem `true`.

Os valores `n`, `N`, `no`, `NO`, `off`, `OFF`, `false` e `FALSE` são analisados automaticamente para serem `false`.

## Datas {#dates}

A Preparação de dados suporta funções de data, tanto como strings quanto como objetos datetime.

### Formato da função de data

A função de data converte strings e objetos datetime em um objeto ZoningDateTime formatado em ISO 8601.

**Formato**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATE}` | Obrigatório. A string que representa a data. |
| `{FORMAT}` | Opcional. A string que representa o formato da data. Mais informações sobre a formatação da string podem ser encontradas na seção [date/time format string](#format). |
| `{DEFAULT_DATE}` | Opcional. A data padrão a ser retornada se a data fornecida for nula. |

Por exemplo, a expressão `date(orderDate, "yyyy-MM-dd")` converterá um valor `orderDate` de &quot;31 de dezembro de 2020&quot; em um valor de data e hora de &quot;2020-12-31&quot;.

### Conversões de função de data

Quando campos de string de dados de entrada são mapeados para campos de data em esquemas usando o Experience Data Model (XDM), o formato de data deve ser mencionado explicitamente. Se não for mencionado explicitamente, a Preparação de dados tentará converter os dados de entrada ao combiná-los aos seguintes formatos. Depois que um formato correspondente for encontrado, ele interromperá a avaliação de todos os formatos subsequentes.

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
> A Preparação de dados tentará converter as cadeias de caracteres em datas da melhor maneira possível. No entanto, essas conversões podem levar a resultados indesejáveis. Por exemplo, o valor da string &quot;12112020&quot; corresponde ao padrão &quot;Dia&quot;, mas o usuário pode ter pretendido que a data seja lida com o padrão &quot;ddaaaa&quot;. Como resultado, os usuários devem mencionar explicitamente o formato de data das cadeias de caracteres.

### Sequências de caracteres de formato de data/hora {#format}

A tabela a seguir mostra quais letras de padrão são definidas para cadeias de caracteres de formato. Observe que as letras fazem distinção entre maiúsculas e minúsculas.

| Símbolo | Significado | Apresentação | Exemplo |
| ------ | ------- | ------------ | ------- |
| G | A era | Texto | AD; Anno Domini; A |
| Y | Ano, com base na Semana ISO | Número | 1996; 96 |
| y | O ano | Número | 2004; 04 |
| M/L | Mês do ano | Número/Texto | 7; 07; julho; Julho; J |
| w | Semana no ano | Número | 27 |
| W | Semana do mês | Número | 3 |
| D | Dia do ano | Número | 189 |
| d | Dia do mês | Número | 10 |
| F | Dia da semana em um mês | Número | 2 |
| E | Nome do dia da semana | Texto | terça-feira; Tonalidade |
| u | Dia da semana, como um número. 1 representa segunda-feira, ..., 7 representa domingo | Número | 1 |
| a | Marcador AM/PM | Texto | PM |
| H | Hora no dia (0-23) | Número | 0 |
| k | Hora no dia (1-24) | Número | 24º |
|  mil | Hora em AM/PM (0-11) | Número | 0 |
| h | Hora em AM/PM (1-12) | Número | 12 |
| m | Minuto na hora | Número | 38º |
| s | Segundo no minuto | Número | 44 |
| S | Milissegundo | Número | 245 |
| z | Fuso horário | Fuso horário geral | Hora Padrão do Pacífico; PST; GMT-08:00 |
| Z | Fuso horário | Fuso horário RFC 822 | -0800 |
| X | Fuso horário | Fuso horário ISO 8601 | -08; -0800; 08:00 |
| V | ID de fuso horário | Texto | América/Los_Angeles |
| O | Deslocamento do fuso horário | Texto | GMT+8 |
| Q/q | Trimestre do ano | Número/Texto | 3; 03; Q3; 3º trimestre |
