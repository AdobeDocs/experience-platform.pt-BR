---
title: Amostra de consultas de bloco anônimas
description: 'O Bloqueio Anônimo é uma sintaxe SQL compatível com o Adobe Experience Platform Query Service, que permite executar com eficiência uma sequência de consultas '
source-git-commit: dffa03d9ab8e26e2c99a359ae000022d6d469572
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Exemplos de consultas para bloco anônimo

O Adobe Experience Platform Query Service oferece suporte a blocos anônimos. O recurso de bloco anônimo permite encadear uma ou mais instruções SQL que são executadas em sequência. Permitem também a opção de tratamento de exceções.

O recurso de bloco anônimo é uma maneira eficiente de executar uma sequência de operações ou consultas. A cadeia de queries no bloco pode ser salva como um modelo e agendada para execução em um horário ou intervalo específico. Essas consultas podem ser usadas para gravar e anexar dados para criar um novo conjunto de dados e geralmente são usadas onde você tem uma dependência.

A tabela fornece um detalhamento das seções principais do bloco: execução e tratamento de exceções. As seções são definidas pelas palavras-chave `BEGIN`, `END` e `EXCEPTION`.

| seção | descrição |
|---|---|
| execução | Uma seção executável começa com a palavra-chave `BEGIN` e termina com a palavra-chave `END`. Qualquer conjunto de instruções incluído nas palavras-chave `BEGIN` e `END` será executado em sequência e garante que as consultas subsequentes não serão executadas até que a consulta anterior na sequência tenha sido concluída. |
| tratamento de exceções | A seção opcional de tratamento de exceções começa com a palavra-chave `EXCEPTION`. Ele contém o código para capturar e manipular exceções se qualquer instrução SQL na seção de execução falhar. Se algum dos queries falhar, o bloco inteiro será interrompido. |

Vale observar que um bloco é uma instrução executável e, portanto, pode ser aninhado dentro de outros blocos.

>[!NOTE]
>
> É altamente recomendável testar suas consultas em conjuntos de dados menores e garantir que funcionem conforme o esperado. Se um query tiver um erro de sintaxe, a exceção será lançada e o bloco inteiro será abortado. Depois de verificar a integridade dos queries, você pode começar a encadeá-los. Isso garante que o bloco funcione como esperado antes de colocá-los em operação.

## Exemplos de consultas de bloco anônimo

A query a seguir mostra um exemplo de cadeia de instruções SQL. Consulte a sintaxe [SQL no documento Serviço de query](../sql/syntax.md) para obter mais informações sobre qualquer sintaxe SQL usada.

```SQL
$$BEGIN
     
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
     
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
     
END$$;
```

<!-- The block below uses `SET` to persist the result of a select query with a variable. It is used in the anonymous block to store the response from a query as a local variable for use with the `SNAPSHOT` feature. -->

No exemplo abaixo, `SET` mantém o resultado de uma consulta `SELECT` na variável local especificada. A variável tem escopo para o bloco anônimo.

A ID do instantâneo é armazenada como uma variável local (`@current_sid`). Ele é usado na próxima query para retornar resultados com base no SNAPSHOT do mesmo conjunto de dados/tabela.

Um snapshot de banco de dados é uma visualização estática e somente leitura de um banco de dados do SQL Server. Para obter mais [informações sobre a cláusula de snapshot](../sql/syntax.md#SNAPSHOT-clause), consulte a documentação da sintaxe SQL.

```SQL
$$BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                                     
END$$;
```

## Próximas etapas

Ao ler este documento, agora você tem uma compreensão clara de blocos anônimos e como eles são estruturados. [Para obter mais informações sobre a execução](./writing-queries.md) do query, leia o guia sobre a execução do query no Serviço de query.

Para obter mais amostras de queries que podem ser usadas no Serviço de query, leia os guias em [Adobe Analytics sample queries](./adobe-analytics.md), [Adobe Target sample queries](./adobe-target.md) ou [ExperienceEvent sample queries](./experience-event-queries.md).
