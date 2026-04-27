---
title: Bloqueio Anônimo no Serviço de Consulta
description: O bloco anônimo é uma sintaxe SQL compatível com o Adobe Experience Platform Query Service, que permite executar uma sequência de consultas com eficiência
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: f2d81f05c8c19c6f28849fc4dbe9bfa26be64645
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Bloqueio anônimo no serviço de consulta

O Serviço de consulta do Adobe Experience Platform oferece suporte a blocos anônimos. O recurso de bloqueio anônimo permite encadear uma ou mais instruções SQL que são executadas em sequência. Permitem também a opção de tratamento de exceções.

O recurso de bloco anônimo é uma maneira eficiente de executar uma sequência de operações ou consultas. A cadeia de consultas no bloco pode ser salva como um modelo e agendada para execução em um horário ou intervalo específico. Essas queries podem ser usadas para gravar e anexar dados para criar um novo conjunto de dados e normalmente são usadas onde você tem uma dependência.

A tabela fornece um detalhamento das seções principais do bloco: execução e tratamento de exceções. As seções são definidas pelas palavras-chave `BEGIN`, `END` e `EXCEPTION`.

| seção | descrição |
|---|---|
| execução | Uma seção executável começa com a palavra-chave `BEGIN` e termina com a palavra-chave `END`. Qualquer conjunto de instruções incluídas nas palavras-chave `BEGIN` e `END` será executado em sequência e garante que as consultas subsequentes não serão executadas até que a consulta anterior na sequência tenha sido concluída. |
| tratamento de exceções | A seção opcional de tratamento de exceções começa com a palavra-chave `EXCEPTION`. Ele contém o código para capturar e tratar exceções se qualquer uma das instruções SQL na seção de execução falhar. Se qualquer uma das queries falhar, o bloco inteiro será interrompido. |

Vale observar que um bloco é uma instrução executável e, portanto, pode ser aninhado dentro de outros blocos.

>[!NOTE]
>
> É altamente recomendável testar suas consultas em conjuntos de dados menores e garantir que elas funcionem conforme o esperado. Se uma consulta tiver um erro de sintaxe, a exceção será lançada e o bloco inteiro será anulado. Depois de verificar a integridade das consultas, você pode começar a encadeá-las. Isso garante que o bloco funcione conforme esperado antes de você colocá-lo em operação.

## Sample anonymous block queries

The following query shows an example of chaining SQL statements. See the [SQL syntax in Query Service](../sql/syntax.md) document for more information on any of the SQL syntax used.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHERS THEN SET @ret = SELECT 'ERROR';
END
$$;
```

In the example below, `SET` persists the result of a `SELECT` query in the specified local variable. The variable is scoped to the anonymous block.

The snapshot ID is stored as a local variable (`@current_sid`). It is then used in the next query to return results based on the SNAPSHOT from the same dataset/table. For more [information on the snapshot clause](../sql/syntax.md#SNAPSHOT-clause) see the SQL syntax documentation.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Anonymous block with third-party clients {#third-party-clients}

Certain third-party clients may require a separate identifier before and after an SQL block to indicate that a part of the script should be handled as a single statement. If you receive an error message when using Query Service with a third-party client, you should refer to the documentation of the third-party client regarding the use of an SQL block.

For example, **DbVisualizer** requires that the delimiter must be the only text on the line. In DbVisualizer, the default value for the Begin Identifier is `--/` and for the End Identifier it is `/`. An example of an anonymous block in DbVisualizer is seen below:

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHERS THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

For DbVisualizer in particular, there is also an option in the UI to &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. See the [DbVisualizer documentation](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) for more information.

## Próximas etapas

By reading this document, you now have a clear understanding of anonymous blocks and how they are structured. Please read the [query execution guide](../best-practices/writing-queries.md) for more information on writing queries.

You should also read about [how anonymous blocks are used with the incremental load design pattern](./incremental-load.md) to increase query efficiency.
