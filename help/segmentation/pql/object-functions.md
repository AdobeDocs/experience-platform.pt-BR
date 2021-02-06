---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Perfil Query Language;object functions;object;
solution: Experience Platform
title: Funções de objeto PQL
topic: developer guide
description: A Linguagem de Query do perfil (PQL) oferta funções para simplificar a interação com objetos.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---


# Funções do objeto

[!DNL Profile Query Language] (PQL) oferta funções para tornar a interação com objetos mais simples. Para obter mais informações sobre outras funções PQL, consulte [[!DNL Profile Query Language] overview](./overview.md).

## É nulo

A função `isNull` determina se uma referência de objeto não existe.

**Formato**

```sql
{OBJECT}.isNull()
```

**Exemplo**

O query PQL a seguir verifica se o endereço residencial da pessoa não existe.

```sql
person.homeAddress.isNull()
```

## Não é nulo

A função `isNotNull` determina se existe uma referência de objeto.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Exemplo**

O query PQL a seguir verifica se o endereço residencial da pessoa existe.

```sql
person.homeAddress.isNotNull()
```

## Próximas etapas

Agora que você aprendeu sobre funções de objeto, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a [visão geral da linguagem do Query do Perfil](./overview.md).