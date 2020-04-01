---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções diversas
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480

---


# Funções diversas

A função a seguir é diversa para a Linguagem do Query do Perfil (PQL). Para obter mais informações sobre outras funções PQL, consulte a visão geral [do idioma do Query do](./overview.md)Perfil.

## Let

A `let` função permite que uma expressão seja armazenada como uma variável para ser usada posteriormente em um query.

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

Agora que você aprendeu sobre diversas funções, é possível usá-las em seus query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
