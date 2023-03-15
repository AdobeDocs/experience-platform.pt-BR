---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;pql;PQL;Profile Query Language;string functions;string;
solution: Experience Platform
title: Funções de String PQL
description: A Linguagem de consulta de perfil (PQL) oferece funções para simplificar a interação com strings.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 7%

---

# Funções de string

[!DNL Profile Query Language] O (PQL) oferece funções para simplificar a interação com strings. Mais informações sobre outras funções PQL podem ser encontradas no [[!DNL Profile Query Language] visão geral](./overview.md).

## Curtir

A variável `like` é usada para determinar se uma sequência de caracteres corresponde a um padrão especificado.

**Formato**

```sql
{STRING_1} like {STRING_2}
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A expressão que deve corresponder à primeira sequência. Há dois caracteres especiais suportados para criar uma expressão: `%` e `_`. <ul><li>`%` é usado para representar zero ou mais caracteres.</li><li>`_` é usado para representar exatamente um caractere.</li></ul> |

**Exemplo**

A consulta PQL a seguir recupera todas as cidades que contêm o padrão &quot;es&quot;.

```sql
city like "%es%"
```

## Começa com

A variável `startsWith` é usada para determinar se uma sequência de caracteres inicia com uma subsequência especificada.

**Formato**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A sequência de caracteres a ser pesquisada na primeira sequência. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como verdadeiro. |

**Exemplo**

A consulta PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o nome da pessoa começa com &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Does not start with

A variável `doesNotStartWith` é usada para determinar se uma sequência de caracteres não inicia com uma subsequência especificada.

**Formato**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A sequência de caracteres a ser pesquisada na primeira sequência. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como verdadeiro. |

**Exemplo**

A consulta PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o nome da pessoa não começa com &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Termina com

A variável `endsWith` é usada para determinar se uma sequência de caracteres termina com uma subsequência especificada.

**Formato**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A sequência de caracteres a ser pesquisada na primeira sequência. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como verdadeiro. |

**Exemplo**

A consulta PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o endereço de email da pessoa termina com &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Não termina com

A variável `doesNotEndWith` é usada para determinar se uma sequência de caracteres não termina com uma subsequência especificada.

**Formato**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A sequência de caracteres a ser pesquisada na primeira sequência. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como verdadeiro. |

**Exemplo**

A consulta PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o endereço de email da pessoa não termina com &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

A variável `contains` é usada para determinar se uma sequência de caracteres contém uma subsequência especificada.

**Formato**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A sequência de caracteres a ser pesquisada na primeira sequência. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como verdadeiro. |

**Exemplo**

A consulta PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o endereço de email da pessoa contém a cadeia de caracteres &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## Não contém

A variável `doesNotContain` é usada para determinar se uma sequência de caracteres não contém uma subsequência especificada.

**Formato**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A sequência de caracteres a ser pesquisada na primeira sequência. |
| `{BOOLEAN}` | Um parâmetro opcional para determinar se a verificação diferencia maiúsculas de minúsculas. Por padrão, isso é definido como verdadeiro. |

**Exemplo**

A consulta PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o endereço de email da pessoa não contém a cadeia de caracteres &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Igual a

A variável `equals` é usada para determinar se uma sequência de caracteres é igual à sequência especificada.

**Formato**

```sql
{STRING_1}.equals({STRING_2})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A sequência de caracteres a ser comparada com a primeira sequência. |

**Exemplo**

A consulta PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o nome da pessoa é &quot;John&quot;.

```sql
person.name.equals("John")
```

## Not equal to

A variável `notEqualTo` é usada para determinar se uma sequência de caracteres não é igual à sequência especificada.

**Formato**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A sequência de caracteres a ser comparada com a primeira sequência. |

**Exemplo**

A consulta PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o nome da pessoa não é &quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Corresponde 

A variável `matches` é usada para determinar se uma sequência de caracteres corresponde a uma expressão regular específica. Consulte [este documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) para obter mais informações sobre padrões correspondentes em expressões regulares.

**Formato**

```sql
{STRING_1}.matches(STRING_2})
```

**Exemplo**

A consulta PQL a seguir determina, sem diferenciar maiúsculas de minúsculas, se o nome da pessoa começa com &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Se você estiver usando funções de expressão regular, como `\w`, você **deve** escape do caractere de barra invertida. Então, em vez de escrever apenas `\w`, você deve incluir uma barra invertida e uma gravação extras `\\w`.

## Grupo de expressão regular

A variável `regexGroup` é usada para extrair informações específicas, com base na expressão regular fornecida.

**Formato**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Exemplo**

A consulta PQL a seguir é usada para extrair o nome de domínio de um endereço de email.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Se você estiver usando funções de expressão regular, como `\w`, você **deve** escape do caractere de barra invertida. Então, em vez de escrever apenas `\w`, você deve incluir uma barra invertida e uma gravação extras `\\w`.

## Próximas etapas

Agora que você aprendeu sobre funções de string, é possível usá-las em consultas PQL. Para obter mais informações sobre outras funções PQL, leia o [Visão geral do idioma de consulta do perfil](./overview.md).
