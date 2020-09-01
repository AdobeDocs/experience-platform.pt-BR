---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;miscellaneous functions;misc;
solution: Experience Platform
title: Funções diversas
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 3%

---


# Funções diversas

A função a seguir é diversa para [!DNL Profile Query Language] (PQL). Para obter mais informações sobre outras funções PQL, consulte a [[!DNL Profile Query Language] visão geral](./overview.md).

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
