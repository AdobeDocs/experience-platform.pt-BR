---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Quantificadores lógicos
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---


# Funções quantificadoras lógicas

Os quantificadores lógicos podem ser usados para afirmar condições com arrays no [!DNL Profile Query Language] (PQL). Para obter mais informações sobre outras funções PQL, consulte a [[!DNL Profile Query Language] visão geral](./overview.md).

## Existe

A `exists` função determina a existência de um item em uma matriz, desde que ele satisfaça a condição fornecida.

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

A `forall` função determina todos os itens em uma matriz que satisfazem todas as condições especificadas.

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

Agora que você aprendeu sobre quantificadores lógicos, é possível usá-los nos query PQL. Para obter mais informações sobre outras funções PQL, leia a visão geral [do Idioma do Query do](./overview.md)Perfil.
