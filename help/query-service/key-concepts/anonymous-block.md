---
title: Bloqueio Anônimo no Serviço de Consulta
description: O bloco anônimo é uma sintaxe SQL compatível com o Adobe Experience Platform Query Service, que permite executar uma sequência de consultas com eficiência
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 9193ba821409806cd7b4667c5de73a0cf2660c66
workflow-type: tm+mt
source-wordcount: '616'
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

## Exemplo de consultas de bloco anônimo

A consulta a seguir mostra um exemplo de instruções SQL de encadeamento. Consulte o documento [Sintaxe SQL no Serviço de Consulta](../sql/syntax.md) para obter mais informações sobre qualquer sintaxe SQL usada.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

No exemplo abaixo, `SET` persiste o resultado de uma consulta `SELECT` na variável local especificada. A variável tem escopo para o bloco anônimo.

A ID do instantâneo é armazenada como uma variável local (`@current_sid`). Ele é usado na próxima query para retornar resultados com base no SNAPSHOT do mesmo conjunto de dados/tabela.

Um instantâneo de banco de dados é uma exibição estática somente leitura de um banco de dados do SQL Server. Para obter mais [informações sobre a cláusula de instantâneo](../sql/syntax.md#SNAPSHOT-clause), consulte a documentação da sintaxe SQL.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Bloqueio anônimo com clientes de terceiros {#third-party-clients}

Alguns clientes de terceiros podem exigir um identificador separado antes e depois de um bloco SQL para indicar que uma parte do script deve ser tratada como uma única instrução. Se você receber uma mensagem de erro ao usar o Serviço de consulta com um cliente de terceiros, consulte a documentação do cliente de terceiros sobre o uso de um bloco SQL.

Por exemplo, **DbVisualizer** requer que o delimitador seja o único texto na linha. Em DbVisualizer, o valor padrão do Identificador de Início é `--/` e do Identificador de Término é `/`. Um exemplo de um bloco anônimo em DbVisualizer é visto abaixo:

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

Para DbVisualizer em particular, também há uma opção na interface do usuário para &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. Consulte a [documentação do DbVisualizer](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) para obter mais informações.

## Próximas etapas

Ao ler este documento, agora você tem uma compreensão clara dos blocos anônimos e de como eles são estruturados. Leia o [guia de execução da consulta](../best-practices/writing-queries.md) para obter mais informações sobre como gravar consultas.

Você também deve ler sobre [como os blocos anônimos são usados com o padrão de design de carga incremental](./incremental-load.md) para aumentar a eficiência da consulta.
