---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;instruções preparadas;preparado;sql;
solution: Experience Platform
title: Instruções Preparadas no Serviço de Consulta
description: No SQL, as instruções preparadas são usadas para modelar consultas ou atualizações semelhantes. O Serviço de consulta do Adobe Experience Platform suporta instruções preparadas usando uma consulta parametrizada.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 5%

---

# Demonstrativos preparados

No SQL, as instruções preparadas são usadas para modelar consultas ou atualizações semelhantes. O Adobe Experience Platform [!DNL Query Service] dá suporte a instruções preparadas usando uma consulta parametrizada. Isso pode otimizar o desempenho, já que não é mais necessário reanalisar repetidamente uma consulta.

## Uso de instruções preparadas

Ao usar instruções preparadas, as seguintes sintaxes são suportadas:

- [PREPARAR](#prepare)
- [EXECUTAR](#execute)
- [DESALOCAR](#deallocate)

### Preparar uma instrução preparada {#prepare}

Esta consulta SQL salva a consulta SELECT gravada com o nome especificado como `PLAN_NAME`. Você pode usar variáveis, como `$1` no lugar dos valores reais. Esta instrução preparada será salva durante a sessão atual. Observe que os nomes do plano **não** diferenciam maiúsculas de minúsculas.

#### Formato SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### SQL de Exemplo

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Executar uma instrução preparada {#execute}

Esta consulta SQL usa a instrução preparada que foi criada anteriormente.

#### Formato SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### SQL de Exemplo

```sql
EXECUTE test('canada', 'vancouver');
```

### Desalocar uma instrução preparada {#deallocate}

Esta consulta SQL é usada para excluir a instrução preparada nomeada.

#### Formato SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### SQL de Exemplo

```sql
DEALLOCATE test;
```

## Exemplo de fluxo usando instruções preparadas

Inicialmente, você pode ter uma consulta SQL, como a abaixo:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

A consulta SQL acima retornará a seguinte resposta:

| ID | firstname | sobrenome | data de nascimento | email | city | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexandre | davis | 15/09/1993 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 14-03-1967 | example2@example.com | Paris | França |
| 10002 | kyoko | sakura | 11-1999-26 | example3@example.com | Tóquio | Japão |
| 10003 | linus | pettersson | 06-1982-03 | example4@example.com | Estocolmo | Suécia |
| 10004 | aasir | waithaka | 12-1976-17 | example5@example.com | Nairóbi | Quênia |
| 10005 | fernando | rios | 30/07/2002 | example6@example.com | Santiago | Chile |

Esta consulta SQL pode ser parametrizada usando a seguinte instrução preparada:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Agora, a instrução preparada pode ser executada usando a seguinte chamada:

```sql
EXECUTE getIdRange(10000, 10005);
```

Quando isso for chamado, você verá os mesmos resultados de antes:

| ID | firstname | sobrenome | data de nascimento | email | city | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexandre | davis | 15/09/1993 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 14-03-1967 | example2@example.com | Paris | França |
| 10002 | kyoko | sakura | 11-1999-26 | example3@example.com | Tóquio | Japão |
| 10003 | linus | pettersson | 06-1982-03 | example4@example.com | Estocolmo | Suécia |
| 10004 | aasir | waithaka | 12-1976-17 | example5@example.com | Nairóbi | Quênia |
| 10005 | fernando | rios | 30/07/2002 | example6@example.com | Santiago | Chile |

Depois de concluir o uso da instrução preparada, você pode desalocá-la usando a seguinte chamada:

```sql
DEALLOCATE getIdRange;
```
