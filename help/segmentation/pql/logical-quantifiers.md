---
keywords: Experience Platform;home;popular tópicos;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: Quantificadores Lógicos PQL
description: Quantificadores lógicos podem ser usados para determinar condições com matrizes na linguagem de consulta de perfil (PQL).
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# Funções quantificadoras lógicas

Quantificadores lógicos podem ser usados para estabelecer condições com matrizes em [!DNL Profile Query Language] (PQL). Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Existe

A variável `exists` determina a existência de um item em uma matriz, desde que atenda à condição fornecida.

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

A consulta PQL a seguir obtém todos os eventos com preço superior a US$ 50 ou com uma SKU de &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Para todos

A variável `forall` determina todos os itens em uma matriz que satisfazem todas as condições fornecidas.

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

A consulta PQL a seguir obtém todos os eventos com preço superior a US$ 50 e com uma SKU de &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Próximas etapas

Agora que você aprendeu sobre quantificadores lógicos, é possível usá-los em consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
