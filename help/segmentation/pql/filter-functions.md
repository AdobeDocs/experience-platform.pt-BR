---
solution: Experience Platform
title: Funções de Filtro PQL
description: As funções de filtro são usadas para filtrar dados em matrizes na Linguagem de consulta de perfil (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 4%

---

# Filtrar funções

As funções de filtro são usadas para filtrar dados em matrizes no [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Filtro

A variável `[]` (filtro) permite que filtros sejam aplicados a uma matriz e retorne um subconjunto da matriz que corresponda à condição especificada.

**Formato**

```sql
{ARRAY}[filter]
```

**Exemplo**

A consulta PQL a seguir obtém todos os eventos que têm pelo menos um item de produto com um SKU igual a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operador para cima

A variável `^` (up) permite fazer referência às propriedades em níveis superiores de filtros.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argumento | Descrição |
| -------- | ----------- |
| `{ARRAY}` | A matriz que está sendo filtrada. |
| `{FILTER_1}` | A camada externa da filtragem. |
| `{FILTER_2}` | A camada interna da filtragem |
| `^{PROPERTY}` | A propriedade que também está sendo filtrada. Devido à `^`, está verificando uma propriedade com base em filter1. |

**Exemplo**

A consulta PQL a seguir obtém todos os eventos que têm pelo menos um item de produto com uma SKU igual a &quot;PS&quot; **ou** têm uma pessoa cujo gênero é feminino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Próximas etapas

Agora que você aprendeu sobre funções de filtro, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
