---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, Serviço de segmentação, pql, PQL, Linguagem de consulta de perfil, funções de filtro, filtro;
solution: Experience Platform
title: Funções de Filtro PQL
topic-legacy: developer guide
description: As funções de filtro são usadas para filtrar dados em matrizes no Idioma da Consulta de Perfil (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# Filtrar funções

As funções de filtro são usadas para filtrar dados em arrays em [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Filtro

A função `[]` (filtro) permite que os filtros sejam aplicados a uma matriz e retorne um subconjunto da matriz que corresponda à condição especificada.

**Formato**

```sql
{ARRAY}[filter]
```

**Exemplo**

A consulta PQL a seguir obtém todos os eventos que têm pelo menos um item de produto com SKU igual a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operador Up

O operador `^` (up) permite fazer referência às propriedades nos níveis superiores dos filtros.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argumento | Descrição |
| -------- | ----------- |
| `{ARRAY}` | A matriz que está sendo filtrada. |
| `{FILTER_1}` | A camada externa da filtragem. |
| `{FILTER_2}` | A camada interna do filtro |
| `^{PROPERTY}` | A propriedade que também está sendo filtrada. Devido a `^`, está verificando uma propriedade com base em filter1. |

**Exemplo**

A consulta PQL a seguir obtém todos os eventos que têm pelo menos um item de produto com um SKU igual a &quot;PS&quot; **ou** têm uma pessoa cujo gênero é feminino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Próximas etapas

Agora que você aprendeu sobre funções de filtro, pode usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a [Visão geral da linguagem de consulta de perfil](./overview.md).
