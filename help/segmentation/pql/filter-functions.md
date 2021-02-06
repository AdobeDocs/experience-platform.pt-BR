---
keywords: Experience Platform;home;popular topics;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Idioma do Query do Perfil;funções de filtro;filter;
solution: Experience Platform
title: Funções do filtro PQL
topic: developer guide
description: As funções de filtragem são usadas para filtrar dados em matrizes na Linguagem de Query do Perfil (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---


# Funções de filtro

As funções de filtro são usadas para filtrar dados em arrays em [!DNL Profile Query Language] (PQL). Para obter mais informações sobre outras funções PQL, consulte [[!DNL Profile Query Language] overview](./overview.md).

## Filtro

A função `[]` (filtro) permite que filtros sejam aplicados a uma matriz e retorne um subconjunto da matriz que corresponda à condição especificada.

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

O operador `^` (up) permite que você se refira às propriedades nos níveis superiores dos filtros.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argumento | Descrição |
| -------- | ----------- |
| `{ARRAY}` | A matriz que está sendo filtrada. |
| `{FILTER_1}` | A camada externa da filtragem. |
| `{FILTER_2}` | A camada interna da filtragem |
| `^{PROPERTY}` | A propriedade que também está sendo filtrada. Devido a `^`, ele está verificando uma propriedade com base em filter1. |

**Exemplo**

O seguinte query PQL obtém todos os eventos que têm pelo menos um item de produto com um SKU igual a &quot;PS&quot; **ou** que têm uma pessoa cujo gênero é feminino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Próximas etapas

Agora que você aprendeu sobre funções de filtro, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a [visão geral da linguagem do Query do Perfil](./overview.md).
