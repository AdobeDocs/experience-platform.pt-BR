---
solution: Experience Platform
title: Funções de objeto do PQL
description: O Profile Query Language (PQL) oferece funções para simplificar a interação com objetos.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 8%

---

# Funções do objeto

O [!DNL Profile Query Language] (PQL) oferece funções para simplificar a interação com objetos. Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## É nulo

A função `isNull` determina se uma referência de objeto não existe como booleana.

**Formato**

```sql
{OBJECT}.isNull()
```

**Exemplo**

A consulta do PQL a seguir verifica se o endereço residencial da pessoa não existe.

```sql
person.homeAddress.isNull()
```

## Não é nulo

A função `isNotNull` determina se uma referência de objeto existe como booleana.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Exemplo**

A consulta do PQL a seguir verifica se o endereço residencial da pessoa existe.

```sql
person.homeAddress.isNotNull()
```

## Próximas etapas

Agora que você aprendeu sobre funções de objeto, é possível usá-las em consultas do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
