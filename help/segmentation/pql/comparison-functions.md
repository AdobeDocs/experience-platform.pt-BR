---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, Serviço de segmentação, pql, PQL, Linguagem de consulta de perfil, funções de comparação, comparação;
solution: Experience Platform
title: Funções de Comparação de PQL
description: As funções de comparação são usadas para comparar diferentes expressões e valores, retornando "true" ou "false" de acordo.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# Funções de comparação

As funções de comparação são usadas para comparar expressões e valores diferentes, retornando `true` ou `false` em conformidade. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Igual a

O `=` (igual) verifica se um valor ou expressão é igual a outro valor ou expressão.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Exemplo**

A consulta PQL a seguir verifica se o país do endereço residencial está no Canadá.

```sql
homeAddress.countryISO = "CA"
```

## Diferente de

O `!=` (não é igual) verifica se um valor ou expressão é **not** igual a outro valor ou expressão.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Exemplo**

A consulta PQL a seguir verifica se o país do endereço residencial não está no Canadá.

```sql
homeAddress.countryISO != "CA"
```

## Greater than

O `>` (greater than) é usada para verificar se o primeiro valor é maior que o segundo valor.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Exemplo**

A consulta PQL a seguir define as pessoas cujos aniversários não caem em janeiro ou fevereiro.

```sql
person.birthMonth > 2
```

## Maior que ou igual a

O `>=` (maior que ou igual a) é usada para verificar se o primeiro valor é maior ou igual ao segundo valor.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Exemplo**

A consulta PQL a seguir define as pessoas cujos aniversários não caem em janeiro ou fevereiro.

```sql
person.birthMonth >= 3
```

## Menos que

O `<` (less than) é usada para verificar se o primeiro valor é menor que o segundo valor.

**Formato**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Exemplo**

A consulta PQL a seguir define as pessoas cujo aniversário é em janeiro.

```sql
person.birthMonth < 2
```

## Less than or equal to

O `<=` A função de comparação (menor que ou igual a) é usada para verificar se o primeiro valor é menor que ou igual ao segundo valor.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Exemplo**

A consulta PQL a seguir define as pessoas cujo aniversário é em janeiro ou fevereiro.

```sql
person.birthMonth <= 2
```

## Próximas etapas

Agora que você aprendeu sobre as funções de comparação, pode usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a seção [Visão geral do idioma de consulta do perfil](./overview.md).
