---
keywords: Experience Platform;home;populares tópicos;serviço de query;serviço de Query;instruções preparadas;preparadas;sql;
solution: Experience Platform
title: Declarações preparadas no serviço do Query
topic: prepared statements
description: No SQL, instruções preparadas são usadas para modelar query ou atualizações semelhantes. O Serviço de Query Adobe Experience Platform suporta declarações preparadas usando um query parametrizado.
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---


# Declarações preparadas

No SQL, instruções preparadas são usadas para modelar query ou atualizações semelhantes. A Adobe Experience Platform [!DNL Query Service] suporta instruções preparadas usando um query com parâmetros. Isso pode ser usado para otimizar o desempenho, pois não será mais necessário analisar novamente um query várias vezes.

## Uso de declarações preparadas

Ao usar instruções preparadas, as seguintes sintaxes são suportadas:

- [PREPARAR](#prepare)
- [EXECUTE](#execute)
- [DESALOCAR](#deallocate)

### Preparar uma declaração preparada {#prepare}

Este query SQL salva o query SELECT gravado com o nome fornecido como `PLAN_NAME`. Você pode usar variáveis, como `$1` no lugar de valores reais. Essa declaração preparada será salva durante a sessão atual. Observe que os nomes de plano não distinguem maiúsculas de minúsculas **e**.

#### Formato SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### SQL de exemplo

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Executar uma instrução preparada {#execute}

Este query SQL usa a instrução preparada que foi criada anteriormente.

#### Formato SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### SQL de exemplo

```sql
EXECUTE test('canada', 'vancouver');
```

### Desalocar uma instrução preparada {#deallocate}

Este query SQL é usado para excluir a instrução preparada nomeada.

#### Formato SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### SQL de exemplo

```sql
DEALLOCATE test;
```

## Fluxo de exemplo usando instruções preparadas

Inicialmente, você pode ter um query SQL, como o abaixo:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

O query SQL acima retornará a seguinte resposta:

| id | nome | sobrenome | data de nascimento | email | city | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexandro | Davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 03-01-1967 | example2@example.com | Paris | França |
| 10002 | kyoko | sakura | 11-1999-26 | example3@example.com | Tóquio | Japão |
| 10003 | linus | petersson | 1982-06-03 | example4@example.com | Estocolmo | Suécia |
| 10004 | aasir | wathaka | 17-12-1976 | example5@example.com | Nairobi | Quênia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Este query SQL pode ser parametrizado usando a seguinte instrução preparada:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Agora, a instrução preparada pode ser executada usando a seguinte chamada:

```sql
EXECUTE getIdRange(10000, 10005);
```

Quando for chamado, você verá exatamente os mesmos resultados de antes:

| id | nome | sobrenome | data de nascimento | email | cidade | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexandro | Davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 03-01-1967 | example2@example.com | Paris | França |
| 10002 | kyoko | sakura | 11-1999-26 | example3@example.com | Tóquio | Japão |
| 10003 | linus | petersson | 1982-06-03 | example4@example.com | Estocolmo | Suécia |
| 10004 | aasir | wathaka | 17-12-1976 | example5@example.com | Nairobi | Quênia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Depois de terminar de usar a declaração preparada, você pode desalocá-la usando a seguinte chamada:

```sql
DEALLOCATE getIdRange;
```
