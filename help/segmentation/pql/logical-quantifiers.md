---
keywords: Experience Platform;home;popular topics;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Idioma do Query do Perfil;quantificadores lógicos;quantificador lógico;
solution: Experience Platform
title: Quantificadores Lógicos da PQL
topic: developer guide
description: Os quantificadores lógicos podem ser usados para afirmar as condições com matrizes na Linguagem do Query do Perfil (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---


# Funções quantificadoras lógicas

Os quantificadores lógicos podem ser usados para afirmar condições com matrizes em [!DNL Profile Query Language] (PQL). Para obter mais informações sobre outras funções PQL, consulte [[!DNL Profile Query Language] overview](./overview.md).

## Existe

A função `exists` determina a existência de um item em uma matriz, desde que ela atenda à condição fornecida.

**Formato**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argumento | Descrição |
| ---------- | ----------- |
| `{VARIABLE}` | O nome de uma variável. |
| `{EXPRESSION}` | A matriz que está sendo verificada. |
| `{CONDITION}` | Uma expressão opcional que filtros os valores na matriz retornados. |

**Exemplo**

O seguinte query PQL obtém todos os eventos que têm um preço maior que US$ 50 ou têm um SKU de &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Para todos

A função `forall` determina todos os itens em um storage que satisfazem todas as condições fornecidas.

**Formato**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argumento | Descrição |
| ---------- | ----------- |
| `{VARIABLE}` | O nome de uma variável. |
| `{EXPRESSION}` | A matriz que está sendo verificada. |
| `{CONDITION}` | Uma expressão opcional que filtros os valores na matriz retornados. |

**Exemplo**

O query PQL a seguir obtém todos os eventos que têm um preço maior que US$ 50 e um SKU de &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Próximas etapas

Agora que você aprendeu sobre quantificadores lógicos, é possível usá-los nos query PQL. Para obter mais informações sobre outras funções PQL, leia a [visão geral da linguagem do Query do Perfil](./overview.md).
