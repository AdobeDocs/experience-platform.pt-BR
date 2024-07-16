---
solution: Experience Platform
title: Funções diversas do PQL
description: A função a seguir é uma função diversa do Profile Query Language (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# Funções diversas

A seguinte função é uma função diversa de [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Let

A função `let` permite que uma expressão seja armazenada como uma variável a ser usada posteriormente em uma consulta.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Exemplo**

A consulta do PQL a seguir obtém todas as somas dos totais de produtos com a transação em USD, onde a soma é maior que US$ 100 e menor que US$ 1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Próximas etapas

Agora que você aprendeu sobre funções diversas, é possível usá-las em queries do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
