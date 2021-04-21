---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, Serviço de segmentação, pql, PQL, Linguagem de consulta de perfil, funções de string, string;
solution: Experience Platform
title: Funções de sequência de caracteres PQL
topic-legacy: developer guide
description: A Linguagem de consulta de perfil (PQL) oferece funções para simplificar a interação com strings.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 7%

---

# Funções da string

[!DNL Profile Query Language] (PQL) oferece funções para simplificar a interação com strings. Mais informações sobre outras funções PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Like

A função `like` é usada para determinar se uma string corresponde a um padrão especificado.

**Formato**

```sql
{STRING_1} like {STRING_2}
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A expressão a ser comparada com a primeira string. Há dois caracteres especiais compatíveis para criar uma expressão: `%` e `_`. <ul><li>`%` é usada para representar zero ou mais caracteres.</li><li>`_` é usada para representar exatamente um caractere.</li></ul> |

**Exemplo**

A consulta PQL a seguir recupera todas as cidades que contêm o padrão &quot;es&quot;.

```sql
city like "%es%"
```

## Começa com

A função `startsWith` é usada para determinar se uma string começa com uma substring especificada.

**Formato**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A string a ser procurada na primeira string. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como true. |

**Exemplo**

A consulta PQL a seguir determina, com diferenciação entre maiúsculas e minúsculas, se o nome da pessoa começa com &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Does not start with

A função `doesNotStartWith` é usada para determinar se uma string não inicia com uma substring especificada.

**Formato**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A string a ser procurada na primeira string. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como true. |

**Exemplo**

A consulta PQL a seguir determina, com diferenciação entre maiúsculas e minúsculas, se o nome da pessoa não inicia com &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Termina com

A função `endsWith` é usada para determinar se uma string termina com uma substring especificada.

**Formato**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A string a ser procurada na primeira string. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como true. |

**Exemplo**

A consulta PQL a seguir determina, com diferenciação de maiúsculas e minúsculas, se o endereço de email da pessoa termina com &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Não termina com

A função `doesNotEndWith` é usada para determinar se uma string não termina com uma substring especificada.

**Formato**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A string a ser procurada na primeira string. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como true. |

**Exemplo**

A consulta PQL a seguir determina, com diferenciação de maiúsculas e minúsculas, se o endereço de email da pessoa não termina com &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

A função `contains` é usada para determinar se uma string contém uma substring especificada.

**Formato**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A string a ser procurada na primeira string. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como true. |

**Exemplo**

A consulta PQL a seguir determina, com diferenciação entre maiúsculas e minúsculas, se o endereço de email da pessoa contém a string &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## Não contém

A função `doesNotContain` é usada para determinar se uma string não contém uma substring especificada.

**Formato**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A string a ser procurada na primeira string. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como true. |

**Exemplo**

A consulta PQL a seguir determina, com diferenciação entre maiúsculas e minúsculas, se o endereço de email da pessoa não contém a string &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Igual a

A função `equals` é usada para determinar se uma string é igual à string especificada.

**Formato**

```sql
{STRING_1}.equals({STRING_2})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A string a ser comparada com a primeira string. |

**Exemplo**

A consulta PQL a seguir determina, com diferenciação entre maiúsculas e minúsculas, se o nome da pessoa é &quot;John&quot;.

```sql
person.name.equals("John")
```

## Not equal to

A função `notEqualTo` é usada para determinar se uma string não é igual à string especificada.

**Formato**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A string na qual executar a verificação. |
| `{STRING_2}` | A string a ser comparada com a primeira string. |

**Exemplo**

A consulta PQL a seguir determina, com diferenciação entre maiúsculas e minúsculas, se o nome da pessoa não é &quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Corresponde

A função `matches` é usada para determinar se uma string corresponde a uma expressão regular específica. Consulte [este documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) para obter mais informações sobre padrões correspondentes em expressões regulares.

**Formato**

```sql
{STRING_1}.matches(STRING_2})
```

**Exemplo**

A consulta PQL a seguir determina, sem distinção entre maiúsculas e minúsculas, se o nome da pessoa começa com &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

## Grupo de expressões regulares

A função `regexGroup` é usada para extrair informações específicas, com base na expressão regular fornecida.

**Formato**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Exemplo**

A consulta PQL a seguir é usada para extrair o nome de domínio de um endereço de email.

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## Próximas etapas

Agora que você aprendeu sobre funções de string, pode usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia a [Visão geral da linguagem de consulta de perfil](./overview.md).
