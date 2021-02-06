---
keywords: Experience Platform;home;popular topics;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Idioma do Query do Perfil;funções diversas;misc;
solution: Experience Platform
title: Funções diversas de PQL
topic: developer guide
description: A função a seguir é diversa para a Linguagem do Query do Perfil (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# Funções diversas

A função a seguir é diversa para [!DNL Profile Query Language] (PQL). Para obter mais informações sobre outras funções PQL, consulte [[!DNL Profile Query Language] overview](./overview.md).

## Let

A função `let` permite que uma expressão seja armazenada como uma variável para ser usada posteriormente em um query.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Exemplo**

O seguinte query PQL obtém todos os totais de produtos com a transação em USD, onde a soma é maior que $100 e menor que $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Próximas etapas

Agora que você aprendeu sobre diversas funções, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a [visão geral da linguagem do Query do Perfil](./overview.md).
