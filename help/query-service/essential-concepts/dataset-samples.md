---
title: Amostras do conjunto de dados
description: Os conjuntos de dados de amostra do Serviço de query permitem realizar consultas exploratórias em grandes dados com um tempo de processamento muito reduzido ao custo da precisão da consulta. Este guia fornece informações sobre como gerenciar suas amostras para o processamento aproximado de consultas
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 13779e619345c228ff2a1981efabf5b1917c4fdb
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Amostras do conjunto de dados

O Adobe Experience Platform Query Service fornece conjuntos de dados de amostra como parte de seus recursos aproximados de processamento de consultas. Os conjuntos de dados de amostra são criados com amostras aleatórias uniformes de [!DNL Azure Data Lake Storage] (ADLS) conjuntos de dados que usam apenas uma porcentagem dos registros do original. Esta percentagem é conhecida como taxa de amostragem. Ajustar a taxa de amostragem para controlar o equilíbrio de precisão e tempo de processamento permite realizar consultas exploratórias em grandes dados com um tempo de processamento muito reduzido ao custo da precisão da consulta.

Como muitos usuários não precisam de uma resposta exata para uma operação de agregação em um conjunto de dados, emitir uma consulta aproximada para retornar uma resposta aproximada é mais eficiente para consultas exploratórias em grandes conjuntos de dados. Como os conjuntos de dados de amostra contêm apenas uma porcentagem dos dados do conjunto de dados original, ele permite trocar a precisão da consulta por um tempo de resposta aprimorado. No tempo de leitura, o Serviço de query precisa verificar menos linhas que produzem resultados mais rápido do que se você consultasse o conjunto de dados inteiro.

Para ajudar você a gerenciar suas amostras para o processamento aproximado de consultas, o Serviço de Consultas oferece suporte às seguintes operações para amostras de conjuntos de dados:

- [Crie uma amostra de conjunto de dados aleatória e uniforme.](#create-a-sample)
- [Especifique opcionalmente um critério de filtro](##optional-filter-criteria)
- [Exiba a lista de amostras para uma tabela ADLS.](#view-list-of-samples)
- [Consulte os conjuntos de dados de amostra diretamente.](#query-sample-datasets)
- [Exclua uma amostra.](#delete-a-sample)
- Exclua amostras associadas quando a tabela ADLS original for solta.

## Introdução {#get-started}

Para usar os recursos de criação e exclusão aproximados de processamento de consultas detalhados neste documento, você deve definir o sinalizador de sessão para `true`. Na linha de comando do Editor de consultas ou do cliente PSQL, insira o `SET aqp=true;` comando.

>[!NOTE]
>
>Você deve ativar o sinalizador de sessão sempre que fizer logon na Platform.

![O Editor de consultas com o comando &#39;SET aqp=true;&#39; está realçado.](../images/essential-concepts/set-session-flag.png)

## Criar uma amostra de conjunto de dados aleatória e uniforme {#create-a-sample}

Use o `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` com um nome de conjunto de dados para criar uma amostra aleatória uniforme a partir desse conjunto de dados.

A taxa de amostra é a porcentagem de registros obtidos do conjunto de dados original. É possível controlar a taxa de amostra usando a variável `TABLESAMPLE SAMPLERATE` palavras-chave. Neste exemplo, o valor de 5,0 equivale a uma taxa de amostra de 50%. Um valor de 2,5 seria equivalente a 25% e assim por diante.

>[!IMPORTANT]
>
>O sistema permite no máximo cinco amostras para cada conjunto de dados. Se você tentar criar um sexto conjunto de dados de amostra, uma mensagem de erro será exibida na tela informando que o limite de amostra foi atingido.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## Especifique opcionalmente um critério de filtro {#optional-filter-criteria}

Você pode optar por especificar um critério de filtro para amostras aleatórias uniformes. Isso permite criar uma amostra com base no subconjunto filtrado da tabela analisada.

Ao criar uma amostra, o filtro opcional é aplicado primeiro e a amostra é criada a partir da exibição filtrada do conjunto de dados. Uma amostra de conjunto de dados com um filtro aplicado segue o seguinte formato de consulta:

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

Exemplos práticos desse tipo de conjunto de dados de amostra filtrado são:

```sql
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

Nos exemplos fornecidos, o nome da tabela é `large_table`, a condição de filtro na tabela original é `month(to_timestamp(timestamp)) in ('8', '9')`e a taxa de amostragem é (X% dos dados filtrados), neste caso, `10`.

## Exibir a lista de amostras {#view-list-of-samples}

Use o `sample_meta()` para exibir a lista de amostras associadas a uma tabela ADLS.

```sql
SELECT sample_meta('example_dataset_name')
```

A lista de amostras do conjunto de dados é exibida no formato do exemplo abaixo.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## Consulte o conjunto de dados de amostra {#query-sample-datasets}

Use o `{EXAMPLE_DATASET_NAME}` para consultar tabelas de amostra diretamente. Como alternativa, adicione o `WITHAPPROXIMATE` palavra-chave ao final de um query e Serviço de query usam automaticamente a amostra criada mais recentemente.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Excluir amostras do conjunto de dados {#delete-a-sample}

A operação de exclusão permite criar novas amostras quando o limite máximo de cinco amostras do conjunto de dados for atingido.

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Se você tiver vários conjuntos de dados de amostra derivados de um conjunto de dados ADLS original, quando o original for descartado, todas as amostras associadas também serão excluídas.
