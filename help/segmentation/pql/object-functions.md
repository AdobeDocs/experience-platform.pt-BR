---
solution: Experience Platform
title: Funções do objeto PQL
description: A Linguagem de consulta de perfil (PQL) oferece funções para simplificar a interação com objetos.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 6%

---

# Funções do objeto

[!DNL Profile Query Language] O (PQL) oferece funções para simplificar a interação com objetos. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## É nulo

A variável `isNull` determina se uma referência de objeto não existe.

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

A variável `isNotNull` determina se existe uma referência de objeto.

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

Agora que você aprendeu sobre funções de objeto, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
