---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Declarações preparadas
topic: prepared statements
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 8%

---


# Declarações preparadas

No SQL, instruções preparadas são usadas para modelar query ou atualizações semelhantes. O Adobe Experience Platform [!DNL Query Service] suporta declarações preparadas usando um query parametrizado. Isso pode ser usado para otimizar o desempenho, pois não será mais necessário analisar novamente um query várias vezes.

## Uso de declarações preparadas

Ao usar instruções preparadas, as seguintes sintaxes são suportadas:

- [PREPARAR](#prepare)
- [EXECUTE](#execute)
- [DESALOCAR](#deallocate)

### Preparar uma declaração preparada {#prepare}

Este query SQL salva o query SELECT gravado com o nome fornecido como `PLAN_NAME`. É possível usar variáveis, como `$1` em vez de valores reais. Essa declaração preparada será salva durante a sessão atual. Observe que os nomes dos planos **não** diferenciam maiúsculas de minúsculas.

#### Formato SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### SQL de exemplo

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Executar uma declaração preparada {#execute}

Este query SQL usa a instrução preparada que foi criada anteriormente.

#### Formato SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### SQL de exemplo

```sql
EXECUTE test('canada', 'vancouver');
```

### Desalocar uma declaração preparada {#deallocate}

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
| 10001 | antoína | dubois | 1967-03-14 | example2@example.com | Paris | França |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tóquio | Japão |
| 10003 | linus | petersson | 1982-06-03 | example4@example.com | Estocolmo | Suécia |
| 10004 | aasir | wathaka | 1976-12-17 | example5@example.com | Nairobi | Quênia |
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

| id | nome | sobrenome | data de nascimento | email | city | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexandro | Davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 1967-03-14 | example2@example.com | Paris | França |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tóquio | Japão |
| 10003 | linus | petersson | 1982-06-03 | example4@example.com | Estocolmo | Suécia |
| 10004 | aasir | wathaka | 1976-12-17 | example5@example.com | Nairobi | Quênia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Depois de terminar de usar a declaração preparada, você pode desalocá-la usando a seguinte chamada:

```sql
DEALLOCATE getIdRange;
```
