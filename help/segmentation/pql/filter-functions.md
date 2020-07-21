---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções de filtro
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 4%

---


# Funções de filtro

As funções de filtro são usadas para filtrar dados em arrays no [!DNL Profile Query Language] (PQL). Para obter mais informações sobre outras funções PQL, consulte a visão geral [do idioma do Query do](./overview.md)Perfil.

## Filtro

A função `[]` (filtro) permite que filtros sejam aplicados a uma matriz e retornem um subconjunto da matriz que corresponda à condição especificada.

**Formato**

```sql
{ARRAY}[filter]
```

**Exemplo**

O seguinte query PQL obtém todos os eventos que têm pelo menos um item de produto com um SKU igual a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operador up

O operador `^` (up) permite que você se refira a propriedades em níveis superiores de filtros.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argumento | Descrição |
| -------- | ----------- |
| `{ARRAY}` | A matriz que está sendo filtrada. |
| `{FILTER_1}` | A camada externa da filtragem. |
| `{FILTER_2}` | A camada interna da filtragem |
| `^{PROPERTY}` | A propriedade que também está sendo filtrada. Devido ao `^`, ele está verificando uma propriedade com base no filter1. |

**Exemplo**

O seguinte query PQL obtém todos os eventos que têm pelo menos um item de produto com um SKU igual a &quot;PS&quot; **ou que** têm uma pessoa cujo gênero é feminino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Próximas etapas

Agora que você aprendeu sobre funções de filtro, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
