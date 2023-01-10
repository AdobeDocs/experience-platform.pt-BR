---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, Serviço de segmentação, pql, PQL, Linguagem de consulta de perfil, funções de objeto, objeto;
solution: Experience Platform
title: Funções de objeto PQL
description: A Linguagem de consulta de perfil (PQL) oferece funções para simplificar a interação com objetos.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---

# Funções do objeto

[!DNL Profile Query Language] (PQL) oferece funções para simplificar a interação com objetos. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## É nulo

O `isNull` determina se uma referência de objeto não existe.

**Formato**

```sql
{OBJECT}.isNull()
```

**Exemplo**

A consulta PQL a seguir verifica se o endereço residencial da pessoa não existe.

```sql
person.homeAddress.isNull()
```

## Não é nulo

O `isNotNull` determina se existe uma referência de objeto.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Exemplo**

A consulta PQL a seguir verifica se o endereço residencial da pessoa existe.

```sql
person.homeAddress.isNotNull()
```

## Próximas etapas

Agora que você aprendeu sobre as funções do objeto, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a seção [Visão geral do idioma de consulta do perfil](./overview.md).
