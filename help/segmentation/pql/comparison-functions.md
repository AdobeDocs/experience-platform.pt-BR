---
solution: Experience Platform
title: Funções de comparação do PQL
description: As funções de comparação são usadas para comparar diferentes expressões e valores, retornando "true" ou "false" de acordo.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: a4385d8872b71ded7e9121d445e10f1ffbd83cfe
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 7%

---

# Funções de comparação

As funções de comparação são usadas para comparar diferentes expressões e valores, retornando `true` ou `false` adequadamente. Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Igual a

A função `=` (igual a) verifica se um valor ou expressão é igual a outro valor ou expressão.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Exemplo**

A consulta do PQL a seguir verifica se o país do endereço residencial está no Canadá.

```sql
homeAddress.countryISO = "CA"
```

## Diferente de

A função `!=` (diferente de) verifica se um valor ou expressão é **não** igual a outro valor ou expressão.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Exemplo**

A consulta do PQL a seguir verifica se o país do endereço residencial não está no Canadá.

```sql
homeAddress.countryISO != "CA"
```

## Maior que

A função `>` (maior que) é usada para verificar se o primeiro valor é maior que o segundo valor.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Exemplo**

O query do PQL a seguir define as pessoas cujos aniversários não acontecem em janeiro ou fevereiro.

```sql
person.birthMonth > 2
```

## Maior que ou igual a

A função `>=` (maior que ou igual a) é usada para verificar se o primeiro valor é maior que ou igual ao segundo valor.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Exemplo**

O query do PQL a seguir define as pessoas cujos aniversários não acontecem em janeiro ou fevereiro.

```sql
person.birthMonth >= 3
```

## Menor que

A função de comparação `<` (menor que) é usada para verificar se o primeiro valor é menor que o segundo valor.

**Formato**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Exemplo**

O query do PQL a seguir define as pessoas cujo aniversário é em janeiro.

```sql
person.birthMonth < 2
```

## Menor que ou igual a

A função de comparação `<=` (menor que ou igual a) é usada para verificar se o primeiro valor é menor que ou igual ao segundo valor.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Exemplo**

O query do PQL a seguir define as pessoas cujo aniversário é em janeiro ou fevereiro.

```sql
person.birthMonth <= 2
```

## Próximas etapas

Agora que você aprendeu sobre funções de comparação, é possível usá-las em consultas do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
