---
solution: Experience Platform
title: Funções de string do PQL
description: O Profile Query Language (PQL) oferece funções para tornar a interação com strings mais simples.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 5%

---

# Funções de string

O [!DNL Profile Query Language] (PQL) oferece funções para simplificar a interação com cadeias de caracteres. Mais informações sobre outras funções do PQL podem ser encontradas na [[!DNL Profile Query Language] visão geral](./overview.md).

## Curtir

A função `like` é usada para determinar se uma cadeia de caracteres corresponde a um padrão especificado como booleano.

**Formato**

```sql
{STRING_1} like {STRING_2}
```

| Argumento | Descrição |
| --------- | ----------- |
| `{STRING_1}` | A sequência de caracteres a ser verificada. |
| `{STRING_2}` | A expressão que deve corresponder à primeira sequência. Há dois caracteres especiais suportados para a criação de uma expressão: `%` e `_`. <ul><li>`%` é usado para representar zero ou mais caracteres.</li><li>`_` é usado para representar exatamente um caractere.</li></ul> |

**Exemplo**

A consulta PQL a seguir recupera todas as cidades que contêm o padrão &quot;es&quot;.

```sql
city like "%es%"
```

## Inicia com

A função `startsWith` é usada para determinar se uma sequência de caracteres inicia com uma subsequência especificada como booleana.

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

## Não inicia com

A função `doesNotStartWith` é usada para determinar se uma cadeia de caracteres não inicia com uma subcadeia especificada como booleana.

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

A função `endsWith` é usada para determinar se uma sequência de caracteres termina com uma subsequência especificada como booleana.

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

A consulta do PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o endereço de email da pessoa termina com &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Não termina com

A função `doesNotEndWith` é usada para determinar se uma cadeia de caracteres não termina com uma subcadeia especificada como booleana.

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

A consulta do PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o endereço de email da pessoa não termina com &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

A função `contains` é usada para determinar se uma cadeia de caracteres contém uma subsequência especificada como booleana.

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

A consulta do PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o endereço de email da pessoa contém a cadeia de caracteres &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## Não contém

A função `doesNotContain` é usada para determinar se uma cadeia de caracteres não contém uma subsequência especificada como booleana.

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

A consulta do PQL a seguir determina, com distinção entre maiúsculas e minúsculas, se o endereço de email da pessoa não contém a cadeia de caracteres &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Igual a

A função `equals` é usada para determinar se uma cadeia de caracteres é igual à cadeia de caracteres especificada como booleana.

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

## Não é igual a

A função `notEqualTo` é usada para determinar se uma cadeia de caracteres não é igual à cadeia de caracteres especificada como booleana.

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

A função `matches` é usada para determinar se uma sequência de caracteres corresponde a uma expressão regular específica. Consulte [este documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) para obter mais informações sobre padrões correspondentes em expressões regulares como booleano.

**Formato**

```sql
{STRING_1}.matches(STRING_2})
```

**Exemplo**

A consulta do PQL a seguir determina, sem diferenciar maiúsculas de minúsculas, se o nome da pessoa começa com &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Se você estiver usando funções de expressão regular, como `\w`, **deverá** escapar do caractere de barra invertida. Então, em vez de escrever apenas `\w`, você deve incluir uma barra invertida extra e escrever `\\w`.

## Grupo de expressão regular

A função `regexGroup` é usada para extrair informações específicas, com base na expressão regular fornecida como uma cadeia de caracteres.

**Formato**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Exemplo**

A consulta do PQL a seguir é usada para extrair o nome de domínio de um endereço de email.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Se você estiver usando funções de expressão regular, como `\w`, **deverá** escapar do caractere de barra invertida. Então, em vez de escrever apenas `\w`, você deve incluir uma barra invertida extra e escrever `\\w`.

## Próximas etapas

Agora que você aprendeu sobre funções de string, é possível usá-las em queries do PQL. Para obter mais informações sobre outras funções do PQL, leia a [visão geral do Profile Query Language](./overview.md).
