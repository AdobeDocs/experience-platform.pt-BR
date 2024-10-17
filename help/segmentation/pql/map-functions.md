---
solution: Experience Platform
title: Funções do PQL Map
description: O Profile Query Language (PQL) oferece funções para facilitar a interação com mapas.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---

# Funções do mapa

O [!DNL Profile Query Language] (PQL) oferece funções para facilitar a interação com mapas. Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Obter

A função `get` é usada para recuperar o valor de um mapa para uma determinada chave como um objeto.

**Formato**

```sql
{MAP}.get({STRING})
```

**Exemplo**

A consulta PQL a seguir obtém o valor do mapa de identidade para a chave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Chaves

A função `keys` é usada para recuperar todas as chaves de um determinado mapa como uma matriz ou lista.

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

A função `values` é usada para recuperar todos os valores de um determinado mapa como uma matriz ou lista.

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

Agora que você aprendeu sobre funções de mapa, é possível usá-las em consultas do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
