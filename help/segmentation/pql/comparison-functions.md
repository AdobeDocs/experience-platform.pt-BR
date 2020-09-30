---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;comparison functions;comparison;
solution: Experience Platform
title: Funções de comparação
topic: developer guide
description: As funções de comparação são usadas para comparar entre expressões e valores diferentes, retornando "true" ou "false" de acordo.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 10%

---


# Funções de comparação

As funções de comparação são usadas para comparar expressões e valores diferentes, retornando `true` ou `false` de acordo. Para obter mais informações sobre outras funções PQL, consulte a [[!DNL Profile Query Language] visão geral](./overview.md).

## Igual a

A função `=` (igual) verifica se um valor ou expressão é igual a outro valor ou expressão.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Exemplo**

O seguinte query PQL verifica se o país do endereço residencial está no Canadá.

```sql
homeAddress.countryISO = "CA"
```

## Diferente de

A função `!=` (não igual) verifica se um valor ou expressão **não** é igual a outro valor ou expressão.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Exemplo**

O seguinte query PQL verifica se o país do endereço residencial não está no Canadá.

```sql
homeAddress.countryISO != "CA"
```

## Greater than

A função `>` (maior que) é usada para verificar se o primeiro valor é maior que o segundo.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Exemplo**

O seguinte query PQL define pessoas cujos aniversários não caem em janeiro ou fevereiro.

```sql
person.birthMonth > 2
```

## Greater than or equal to

A função `>=` (maior que ou igual a) é usada para verificar se o primeiro valor é maior ou igual ao segundo valor.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Exemplo**

O seguinte query PQL define pessoas cujos aniversários não caem em janeiro ou fevereiro.

```sql
person.birthMonth >= 3
```

## Less than

A função de comparação `<` (menor que) é usada para verificar se o primeiro valor é menor que o segundo.

**Formato**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Exemplo**

O query PQL a seguir define as pessoas cujo aniversário é em janeiro.

```sql
person.birthMonth < 2
```

## Less than or equal to

A função de comparação `<=` (menor que ou igual a) é usada para verificar se o primeiro valor é menor que ou igual ao segundo valor.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Exemplo**

O query PQL a seguir define as pessoas cujo aniversário é em janeiro ou fevereiro.

```sql
person.birthMonth <= 2
```

## Próximas etapas

Agora que você aprendeu sobre as funções de comparação, é possível usá-las nos query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
