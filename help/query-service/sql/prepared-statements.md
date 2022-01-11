---
keywords: Experience Platform; home; tópicos populares; serviço de consulta; serviço de consulta; instruções preparadas; preparado; sql;
solution: Experience Platform
title: Declarações Preparadas no Serviço de Consulta
topic-legacy: prepared statements
description: No SQL, as instruções preparadas são usadas para modelar consultas ou atualizações semelhantes. O Adobe Experience Platform Query Service oferece suporte a instruções preparadas usando uma consulta parametrizada.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 9f4e34edc47a333aa88153529d0af6a10f189a15
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 11%

---

# Instruções preparadas

No SQL, as instruções preparadas são usadas para modelar consultas ou atualizações semelhantes. Adobe Experience Platform [!DNL Query Service] O suporta instruções preparadas usando uma consulta parametrizada. Isso pode otimizar o desempenho, pois não é mais necessário analisar novamente uma consulta de forma repetitiva.

## Uso de instruções preparadas

Ao usar instruções preparadas, as seguintes sintaxes são suportadas:

- [PREPARAR](#prepare)
- [EXECUTAR](#execute)
- [DESALOCAR](#deallocate)

### Preparar uma instrução preparada {#prepare}

Esta consulta SQL salva a consulta SELECT escrita com o nome dado como `PLAN_NAME`. Você pode usar variáveis, como `$1` em vez dos valores reais. Essa instrução preparada será salva durante a sessão atual. Observe que os nomes dos planos são **not** diferencia maiúsculas de minúsculas.

#### Formato SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### SQL de exemplo

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Executar uma instrução preparada {#execute}

Esta consulta SQL usa a instrução preparada criada anteriormente.

#### Formato SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### SQL de exemplo

```sql
EXECUTE test('canada', 'vancouver');
```

### Desalocar uma instrução preparada {#deallocate}

Esta consulta SQL é usada para excluir a instrução preparada nomeada.

#### Formato SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### SQL de exemplo

```sql
DEALLOCATE test;
```

## Exemplo de fluxo usando instruções preparadas

Inicialmente, você pode ter uma consulta SQL, como a abaixo:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

A consulta SQL acima retornará a seguinte resposta:

| id | firstname | lastname | data de nascimento | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexandro | davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 1967-03-14 | example2@example.com | Paris | França |
| 10002 | kyoko | sakura | 11-1999-26 | example3@example.com | Tóquio | Japão |
| 10003 | linus | petersson | 1982-06-03 | example4@example.com | Estocolmo | Suécia |
| 10004 | aasir | wathaka | 1976-12-17 | example5@example.com | Nairobi | Quênia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Esta consulta SQL pode ser parametrizada usando a seguinte instrução preparada:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Agora, a instrução preparada pode ser executada usando a seguinte chamada:

```sql
EXECUTE getIdRange(10000, 10005);
```

Quando isso for chamado, você verá exatamente os mesmos resultados de antes:

| id | firstname | lastname | data de nascimento | email | cidade | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexandro | davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 1967-03-14 | example2@example.com | Paris | França |
| 10002 | kyoko | sakura | 11-1999-26 | example3@example.com | Tóquio | Japão |
| 10003 | linus | petersson | 1982-06-03 | example4@example.com | Estocolmo | Suécia |
| 10004 | aasir | wathaka | 1976-12-17 | example5@example.com | Nairobi | Quênia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Após terminar de usar a declaração preparada, é possível desalocá-la usando a seguinte chamada:

```sql
DEALLOCATE getIdRange;
```
