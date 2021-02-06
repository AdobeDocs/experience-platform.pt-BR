---
keywords: Experience Platform;home;popular topics;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Idioma do Query do Perfil;funções do mapa;map;
solution: Experience Platform
title: Funções do Mapa PQL
topic: developer guide
description: A Linguagem do Query do perfil (PQL) oferta funções para facilitar a interação com mapas.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

---


# Funções de mapa

[!DNL Profile Query Language] (PQL) oferta funções para facilitar a interação com mapas. Para obter mais informações sobre outras funções PQL, consulte [[!DNL Profile Query Language] overview](./overview.md).

## Obtenha

A função `get` é usada para recuperar o valor de um mapa para uma determinada chave.

**Formato**

```sql
{MAP}.get({STRING})
```

**Exemplo**

O seguinte query PQL obtém o valor do mapa de identidade para a chave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Teclas

A função `keys` é usada para recuperar todas as chaves de um determinado mapa.

**Formato**

```sql
{MAP}.keys()
```

**Exemplo**

O seguinte query PQL obtém todas as chaves do mapa `identityMap`.

```sql
identityMap.keys()
```

## Valores

A função `values` é usada para recuperar todos os valores de um determinado mapa.

**Formato**

```sql
{MAP}.values()
```

**Exemplo**

O seguinte query PQL obtém todos os valores do mapa `identityMap`.

```sql
identityMap.values()
```

## Próximas etapas

Agora que você aprendeu sobre funções de mapa, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a [visão geral da linguagem do Query do Perfil](./overview.md).
