---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Profile Query Language;diversas funções;misc;
solution: Experience Platform
title: Funções Diversas PQL
description: A função a seguir é uma função diversa da Linguagem de consulta de perfil (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Funções diversas

A seguinte função é uma função diversa para [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Let

A variável `let` permite que uma expressão seja armazenada como uma variável a ser usada posteriormente em uma query.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Exemplo**

A consulta PQL a seguir obtém todas as somas dos totais do produto com a transação em USD, onde a soma é maior que US$ 100 e menor que US$ 1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Próximas etapas

Agora que você aprendeu sobre funções diversas, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
