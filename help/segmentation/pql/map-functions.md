---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, Serviço de segmentação, pql, PQL, Linguagem de consulta de perfil, funções de mapa, mapa;
solution: Experience Platform
title: Funções do Mapa PQL
description: A Linguagem de consulta de perfil (PQL) oferece funções para facilitar a interação com mapas.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---

# Funções do mapa

[!DNL Profile Query Language] (PQL) oferece funções para facilitar a interação com mapas. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Obtenha

O `get` é usada para recuperar o valor de um mapa para uma determinada chave.

**Formato**

```sql
{MAP}.get({STRING})
```

**Exemplo**

A consulta PQL a seguir obtém o valor do mapa de identidade da chave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Teclas

O `keys` é usada para recuperar todas as chaves de um determinado mapa.

**Formato**

```sql
{MAP}.keys()
```

**Exemplo**

A consulta PQL a seguir obtém todas as chaves do mapa `identityMap`.

```sql
identityMap.keys()
```

## Valores

O `values` é usada para recuperar todos os valores de um determinado mapa.

**Formato**

```sql
{MAP}.values()
```

**Exemplo**

A consulta PQL a seguir obtém todos os valores do mapa `identityMap`.

```sql
identityMap.values()
```

## Próximas etapas

Agora que você aprendeu sobre as funções do mapa, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a seção [Visão geral do idioma de consulta do perfil](./overview.md).
