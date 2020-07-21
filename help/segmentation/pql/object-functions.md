---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções do objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---


# Funções do objeto

[!DNL Profile Query Language] (PQL) oferta funções para tornar a interação com objetos mais simples. Para obter mais informações sobre outras funções PQL, consulte a visão geral [do idioma do Query do](./overview.md)Perfil.

## É nulo

A `isNull` função determina se uma referência de objeto não existe.

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

A `isNotNull` função determina se existe uma referência de objeto.

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

Agora que você aprendeu sobre funções de objeto, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.