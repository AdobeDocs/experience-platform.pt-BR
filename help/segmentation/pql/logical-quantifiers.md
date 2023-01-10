---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de Segmentação; pql; PQL; Linguagem de Consulta de Perfil; quantificadores lógicos; quantificador lógico;
solution: Experience Platform
title: Quantificadores Lógicos PQL
description: Os quantificadores lógicos podem ser usados para asserção de condições com matrizes na linguagem de consulta de perfil (PQL).
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# Funções quantificadoras lógicas

Os quantificadores lógicos podem ser usados para asserção de condições com matrizes em [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Existe

O `exists` determina a existência de um item em uma matriz, desde que satisfaça a condição fornecida.

**Formato**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argumento | Descrição |
| ---------- | ----------- |
| `{VARIABLE}` | Um nome de uma variável. |
| `{EXPRESSION}` | A matriz que está sendo verificada. |
| `{CONDITION}` | Uma expressão opcional que filtra os valores na matriz retornada. |

**Exemplo**

A consulta PQL a seguir obtém todos os eventos que têm um preço maior que US$ 50 ou têm um SKU de &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Para todos

O `forall` determina todos os itens em uma matriz que satisfazem todas as condições fornecidas.

**Formato**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argumento | Descrição |
| ---------- | ----------- |
| `{VARIABLE}` | Um nome de uma variável. |
| `{EXPRESSION}` | A matriz que está sendo verificada. |
| `{CONDITION}` | Uma expressão opcional que filtra os valores na matriz retornada. |

**Exemplo**

A consulta PQL a seguir obtém todos os eventos que têm um preço maior que US$ 50 e um SKU de &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Próximas etapas

Agora que você aprendeu sobre quantificadores lógicos, é possível usá-los em queries PQL. Para obter mais informações sobre outras funções PQL, leia a seção [Visão geral do idioma de consulta do perfil](./overview.md).
