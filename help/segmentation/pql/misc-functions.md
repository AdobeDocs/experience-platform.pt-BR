---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de Segmentação; pql; PQL; Idioma de Consulta de Perfil; funções diversas; misc;
solution: Experience Platform
title: Funções diversas de PQL
topic-legacy: developer guide
description: A função a seguir é uma função diversa para a Linguagem de consulta de perfil (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Funções diversas

A função a seguir é uma função diversa para [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Let

A função `let` permite que uma expressão seja armazenada como uma variável a ser usada posteriormente em uma query.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Exemplo**

A consulta PQL a seguir obtém todos os totais de produtos com a transação em USD, onde a soma é maior que $100 e menor que $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Próximas etapas

Agora que você aprendeu sobre funções diversas, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a [Visão geral da linguagem de consulta de perfil](./overview.md).
