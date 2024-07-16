---
solution: Experience Platform
title: Funções de filtro do PQL
description: As funções de filtro são usadas para filtrar dados em matrizes no Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---

# Filtrar funções

As funções de filtro são usadas para filtrar dados em matrizes em [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Filtro

A função `[]` (filtro) permite que filtros sejam aplicados a uma matriz e retorne um subconjunto da matriz que corresponda à condição especificada.

**Formato**

```sql
{ARRAY}[filter]
```

**Exemplo**

A consulta do PQL a seguir obtém todos os eventos que têm pelo menos um item de produto com um SKU igual a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operador para cima

O operador `^` (para cima) permite fazer referência às propriedades nos níveis superiores dos filtros.

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

A consulta PQL a seguir obtém todos os eventos que têm pelo menos um item de produto com uma SKU igual a &quot;PS&quot; **ou** com uma pessoa cujo gênero é feminino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Próximas etapas

Agora que você aprendeu sobre funções de filtro, é possível usá-las em queries do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
