---
solution: Experience Platform
title: Funções de Mapa PQL
description: A Linguagem de consulta de perfil (PQL) oferece funções para facilitar a interação com mapas.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 7%

---

# Funções do mapa

[!DNL Profile Query Language] O (PQL) oferece funções para facilitar a interação com mapas. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Obtenha

A variável `get` é usada para recuperar o valor de um mapa para uma determinada chave.

**Formato**

```sql
{MAP}.get({STRING})
```

**Exemplo**

A consulta PQL a seguir obtém o valor do mapa de identidade da chave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Chaves

A variável `keys` é usada para recuperar todas as chaves de um determinado mapa.

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

A variável `values` é usada para recuperar todos os valores de um determinado mapa.

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

Agora que você aprendeu sobre funções de mapa, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
