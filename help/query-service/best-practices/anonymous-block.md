---
title: Bloqueio Anônimo no Serviço de Consulta
description: O bloco anônimo é uma sintaxe SQL compatível com o Adobe Experience Platform Query Service, que permite executar com eficiência uma sequência de consultas
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 43c5bdbfa93872ba54bde72bbea8201b73e9dfee
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Bloco anônimo no Serviço de Consulta

O Adobe Experience Platform Query Service oferece suporte a blocos anônimos. O recurso de bloco anônimo permite encadear uma ou mais instruções SQL que são executadas em sequência. Permitem também a opção de tratamento de exceções.

O recurso de bloco anônimo é uma maneira eficiente de executar uma sequência de operações ou consultas. A cadeia de queries no bloco pode ser salva como um modelo e agendada para execução em um horário ou intervalo específico. Essas consultas podem ser usadas para gravar e anexar dados para criar um novo conjunto de dados e geralmente são usadas onde você tem uma dependência.

>[!IMPORTANT]
>
>O agendamento de consultas usando blocos anônimos atualmente é possível somente por meio da variável [!DNL Query Service] API. Consulte a documentação para [complete as instruções sobre como agendar consultas por meio da API](../api/scheduled-queries.md).

A tabela fornece um detalhamento das seções principais do bloco: execução e tratamento de exceções. As seções são definidas pelas palavras-chave `BEGIN`, `END`e `EXCEPTION`.

| seção | descrição |
|---|---|
| execução | Uma seção executável começa com a palavra-chave `BEGIN` e termina com a palavra-chave `END`. Qualquer conjunto de instruções incluído na variável `BEGIN` e `END` as palavras-chave serão executadas em sequência e garante que as consultas subsequentes não serão executadas até que a consulta anterior na sequência seja concluída. |
| tratamento de exceções | A seção opcional de tratamento de exceções começa com a palavra-chave `EXCEPTION`. Ele contém o código para capturar e manipular exceções se qualquer instrução SQL na seção de execução falhar. Se algum dos queries falhar, o bloco inteiro será interrompido. |

Vale observar que um bloco é uma instrução executável e, portanto, pode ser aninhado dentro de outros blocos.

>[!NOTE]
>
> É altamente recomendável testar suas consultas em conjuntos de dados menores e garantir que funcionem conforme o esperado. Se um query tiver um erro de sintaxe, a exceção será lançada e o bloco inteiro será abortado. Depois de verificar a integridade dos queries, você pode começar a encadeá-los. Isso garante que o bloco funcione como esperado antes de colocá-los em operação.

## Exemplos de consultas de bloco anônimo

A query a seguir mostra um exemplo de cadeia de instruções SQL. Consulte a [Sintaxe SQL no Serviço de Consulta](../sql/syntax.md) documento para obter mais informações sobre qualquer sintaxe SQL usada.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

No exemplo abaixo, `SET` persiste no resultado de um `SELECT` na variável local especificada. A variável tem escopo para o bloco anônimo.

A ID do instantâneo é armazenada como uma variável local (`@current_sid`). Ele é usado na próxima query para retornar resultados com base no SNAPSHOT do mesmo conjunto de dados/tabela.

Um snapshot de banco de dados é uma visualização estática e somente leitura de um banco de dados do SQL Server. Para obter mais informações [informações sobre a cláusula de snapshot](../sql/syntax.md#SNAPSHOT-clause) consulte a documentação da sintaxe SQL.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Próximas etapas

Ao ler este documento, agora você tem uma compreensão clara de blocos anônimos e como eles são estruturados. [Para obter mais informações sobre a execução da consulta](./writing-queries.md), leia o guia sobre a execução do query no Serviço de query.

Você também deve ler sobre [como o bloco anônimo é usado com o padrão de design de carga incremental](./incremental-load.md) para aumentar a eficiência do query.
