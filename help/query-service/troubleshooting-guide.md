---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, guia de solução de problemas, perguntas frequentes, solução de problemas;
solution: Experience Platform
title: Guia de solução de problemas do serviço de query
topic-legacy: troubleshooting
description: Este documento contém informações sobre códigos de erro comuns encontrados e as possíveis causas.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 42288ae7db6fb19bc0a0ee8e4ecfa50b7d63d017
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 4%

---

# [!DNL Query Service] guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Serviço de query e fornece uma lista de códigos de erro vistos com frequência ao usar o Serviço de query. Para dúvidas e solução de problemas relacionados a outros serviços no Adobe Experience Platform, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Serviço de query.

### Como posso obter apenas os metadados para um query?

Para obter apenas os metadados de um query, execute um query que retorne zero linhas, da seguinte maneira:

```sql
SELECT * FROM <table> WHERE 1=0
```

Essa consulta retorna somente os metadados da tabela especificada.

### Como posso iterar rapidamente em uma consulta CTAS (Criar Tabela como Selecionar) sem materializá-la?

É possível criar tabelas temporárias para iterar e experimentar rapidamente em uma query antes de materializá-la para uso. Você também pode usar tabelas temporárias para validar se um query é funcional.

Por exemplo, é possível criar uma tabela temporária:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Em seguida, é possível usar a tabela temporária da seguinte maneira:

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

### Como devo filtrar os dados das séries de tempo?

Ao consultar os dados das séries de tempo, você deve usar o filtro de carimbo de data e hora sempre que possível para obter uma análise mais precisa.

>[!NOTE]
>
> A string de data **deve** estar no formato `yyyy-mm-ddTHH24:MM:SS`.

Um exemplo de uso do filtro de carimbo de data e hora pode ser visto abaixo:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### Devo usar curingas, como *, para obter todas as linhas dos meus conjuntos de dados?

Não é possível usar curingas para obter todos os dados de suas linhas, pois o Serviço de query deve ser tratado como um **columnar-store** em vez de um sistema de armazenamento tradicional baseado em linha.

### Devo usar `NOT IN` no meu query SQL?

O operador `NOT IN` é frequentemente usado para recuperar linhas que não são encontradas em outra tabela ou instrução SQL. Esse operador pode retardar o desempenho e retornar resultados inesperados se as colunas que estão sendo comparadas aceitarem `NOT NULL`, ou se você tiver um grande número de registros.

Em vez de usar `NOT IN`, você pode usar `NOT EXISTS` ou `LEFT OUTER JOIN`.

Por exemplo, se você tiver criado as seguintes tabelas:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Se você estiver usando o operador `NOT EXISTS`, poderá replicar usando o operador `NOT IN` usando a seguinte query:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Como alternativa, se estiver usando o operador `LEFT OUTER JOIN`, você pode replicar usando o operador `NOT IN` usando a seguinte query:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### Qual é o uso correto dos operadores `OR` e `UNION`?

### Como uso corretamente o operador `CAST` para converter meus carimbos de data e hora em consultas SQL?

Ao usar o operador `CAST` para converter um carimbo de data e hora, é necessário incluir a data **e** hora.

Por exemplo, a falta do componente de tempo, como mostrado abaixo, resultará em um erro:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Um uso correto do operador `CAST` é mostrado abaixo:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

## Erros da API REST

| Código do status HTTP | Descrição | Possíveis causas |
| ---------------- | ----------- | --------------- |
| 400 | Solicitação inválida | Consulta malformada ou ilegal |
| 401° | Falha na autenticação | Token de autenticação inválido |
| 500 | Erro interno do servidor | Falha do sistema interno |

## Erros da API PostgreSQL

| Código de erro | Estado da conexão | Descrição | Causa possível |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | N/D | Tipo de mensagem não suportado | Tipo de mensagem não suportado |
| **28P01** | Iniciar - autenticação | Senha inválida | Token de autenticação inválido |
| **28000** | Iniciar - autenticação | Tipo de autorização inválido | Tipo de autorização inválido. Deve ser `AuthenticationCleartextPassword`. |
| **42P12** | Iniciar - autenticação | Nenhuma tabela encontrada | Nenhuma tabela encontrada para uso |
| **42601** | Consulta | Erro de sintaxe | Comando ou erro de sintaxe inválido |
| **42P01** | Consulta | Tabela não encontrada | A tabela especificada na consulta não foi encontrada |
| **42P07** | Consulta | Tabela existe | Já existe uma tabela com o mesmo nome (CRIAR TABELA) |
| **53400** | Consulta | LIMITE excede o valor máximo | O usuário especificou uma cláusula LIMIT superior a 100.000 |
| **53400** | Consulta | Tempo limite do demonstrativo | A declaração ao vivo enviada demorou mais de 10 minutos |
| **58000** | Consulta | Erro do sistema | Falha do sistema interno |
| **0A000** | Query/Comando | Não suportado | Não há suporte para o recurso/funcionalidade no query/comando |
| **42501** | Consulta DROP TABLE | Eliminar tabela não criada pelo Serviço de Consulta | A tabela que está sendo solta não foi criada pelo Serviço de Consulta usando a instrução `CREATE TABLE` |
| **42501** | Consulta DROP TABLE | Tabela não criada pelo usuário autenticado | A tabela que está sendo solta não foi criada pelo usuário conectado no momento |
| **42P01** | Consulta DROP TABLE | Tabela não encontrada | A tabela especificada na consulta não foi encontrada |
| **42P12** | Consulta DROP TABLE | Nenhuma tabela encontrada para `dbName`: verifique o `dbName` | Nenhuma tabela foi encontrada no banco de dados atual |
