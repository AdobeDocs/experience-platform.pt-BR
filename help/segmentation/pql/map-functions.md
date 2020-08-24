---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções de mapa
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 6%

---


# Funções de mapa

[!DNL Profile Query Language] (PQL) oferta funções para facilitar a interação com mapas. Para obter mais informações sobre outras funções PQL, consulte a [[!DNL Profile Query Language] visão geral](./overview.md).

## Obtenha

A `get` função é usada para recuperar o valor de um mapa para uma determinada chave.

**Formato**

```sql
{MAP}.get({STRING})
```

**Exemplo**

O query PQL a seguir obtém o valor do mapa de identidade da chave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Teclas

A `keys` função é usada para recuperar todas as chaves de um determinado mapa.

**Formato**

```sql
{MAP}.keys()
```

**Exemplo**

O query PQL a seguir obtém todas as chaves do mapa `identityMap`.

```sql
identityMap.keys()
```

## Valores

A `values` função é usada para recuperar todos os valores de um determinado mapa.

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

Agora que você aprendeu sobre funções de mapa, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
