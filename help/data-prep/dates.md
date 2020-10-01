---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;date;date functions;dates;
solution: Experience Platform
title: Funções de data
topic: overview
description: Este documento apresenta as funções de data usadas com a Preparação de dados.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 17%

---


# Funções de data

A Preparação de dados suporta funções de data, tanto como strings quanto como objetos datetime.

## Conversões da função de data

Quando os campos de string de dados recebidos são mapeados para campos de data em schemas usando o Modelo de dados de experiência (XDM), o formato de data deve ser mencionado explicitamente. Se não for mencionado explicitamente, o Data Prep tentará converter os dados de entrada ao equipará-los aos seguintes formatos. Quando um formato correspondente for encontrado, ele deixará de avaliar quaisquer formatos subsequentes.

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
> A Preparação de dados tentará converter sequências de caracteres em datas o melhor possível. No entanto, essas conversões podem levar a resultados indesejáveis. Por exemplo, o valor da string &quot;12112020&quot; corresponde ao padrão &quot;MMddyyyy&quot;, mas o usuário pode ter pretendido que a data seja lida com o padrão &quot;ddaaaa&quot;. Como resultado, os usuários devem mencionar explicitamente o formato de data para strings.

## Sequências de caracteres de formato de data/hora

A tabela a seguir mostra quais letras de padrão estão definidas para strings de formato. Observe que as letras fazem distinção entre maiúsculas e minúsculas.

| Símbolo | Significado | Apresentação | Exemplo |
| ------ | ------- | ------------ | ------- |
| G | A era | Texto | AD; Anno Domini; A |
| Y | Ano, com base na Semana ISO | Número | 1996; 96 |
| y | O ano | Número | 2004; 04 |
| M/L | Mês do ano | Número/Texto | 7; 07; jul; Julho; J |
| w | Semana do ano | Número | 27 |
| W | Semana do mês | Número | 3 |
| D | Dia do ano | Número | 189 |
| d | Dia do mês | Número | 10 |
| F | Dia da semana em um mês | Número | 2 |
| E | Nome do dia da semana | Texto | Terça-feira; Tonalidade |
| u | Dia da semana, como um número. 1 representa segunda-feira, ..., 7 representa domingo | Número | 1 |
| a | Marcador AM/PM | Texto | PM |
| H | Hora do dia (0-23) | Número | 0 |
| k | Hora do dia (1-24) | Número | 24 |
| K | Hora em AM/PM (0-11) | Número | 0 |
| h | Hora em AM/PM (1-12) | Número | 12 |
| m | Minuto na hora | Número | 38 |
| s | Segundo no minuto | Número | 44 |
| S | Milissegundo | Número | 245 |
| z | Fuso horário | Fuso horário geral | Hora Padrão do Pacífico; PST; GMT-08:00 |
| Z | Fuso horário | Fuso horário RFC 822 | -0800 |
| X | Fuso horário | Fuso horário ISO 8601 | -08; -0800; -08:00 |
| V | ID de fuso horário | Texto | América/Los_Angeles |
| O | Deslocamento do fuso horário | Texto | GMT+8 |
| Q/q | Trimestre do ano | Número/Texto | 3; 03; Q3; terceiro trimestre |

**Exemplo**

A expressão `date(orderDate, 'yyyy-MM-dd')` converterá orderDate, se seu valor for &quot;31 de dezembro de 2020&quot;, em um horário de data com o valor &quot;2020-12-31&quot;.