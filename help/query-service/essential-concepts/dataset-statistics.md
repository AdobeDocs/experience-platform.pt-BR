---
title: Computação de estatísticas do conjunto de dados
description: Este documento descreve como calcular estatísticas em nível de coluna nos conjuntos de dados do Azure Data Lake Storage (ADLS) com comandos SQL.
source-git-commit: c7bc395038906e27449c82c518bd33ede05c5691
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Cálculo das estatísticas do conjunto de dados

Agora é possível calcular estatísticas em nível de coluna no [!DNL Azure Data Lake Storage] (ADLS) com a variável `COMPUTE STATISTICS` e `SHOW STATISTICS` Comandos SQL. Os comandos SQL que calculam as estatísticas do conjunto de dados são uma extensão do `ANALYZE TABLE` comando. Detalhes completos sobre o `ANALYZE TABLE` comando pode ser encontrado no campo [Documentação de referência SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Atualmente, as estatísticas geradas são válidas somente para essa sessão e não são persistentes entre sessões. Elas não podem ser acessadas em diferentes sessões PSQL.

Com o `SHOW STATISTICS FOR <alias_name>` você pode ver as estatísticas que foram computadas com o comando `ANALYZE TABLE COMPUTE STATISTICS` comando. Com a combinação desses comandos, agora é possível calcular estatísticas de coluna no conjunto de dados inteiro, em um subconjunto de um conjunto de dados, em todas as colunas ou em um subconjunto de colunas.

>[!IMPORTANT]
>
>A variável `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, e `SHOW STATISTICS` não há suporte para comandos em tabelas do data warehouse. Essas extensões para o `ANALYZE TABLE` atualmente, só há suporte para comandos ADLS. Para obter mais informações, consulte [seção ANALISAR TABELA](../sql/syntax.md#analyze-table) do guia de sintaxe SQL.

Este guia ajuda a estruturar suas consultas para que você possa calcular as estatísticas de coluna de um conjunto de dados ADLS. Usando esses comandos, você pode ver as estatísticas geradas na sua sessão por meio de um cliente PSQL usando uma consulta SQL.

## Calcular estatísticas {#compute-statistics}

Construções adicionais foram adicionadas à `ANALYZE TABLE` comando que permite **calcular estatísticas para um subconjunto de um conjunto de dados e para determinadas colunas**. Para fazer isso, você deve usar o `ANALYZE TABLE <tableName> COMPUTE STATISTICS` formato.

>[!IMPORTANT]
>
>O comportamento padrão calcula as estatísticas para o **conjunto de dados inteiro** e para **todas as colunas**. Para calcular estatísticas em todas as colunas, você usaria o formato de consulta `ANALYZE TABLE COMPUTE STATISTICS`. Você está **não** recomendado usar isso em um conjunto de dados ADLS, pois o tamanho do conjunto de dados pode ser muito grande (potencialmente petabytes de dados). Em vez disso, você sempre deve considerar executar o comando analyze usando `FILTERCONTEXT` e uma lista especificada de colunas. Consulte as seções sobre [limitação de colunas analisadas](#limit-included-columns) e [adicionar uma condição de filtro](#filter-condition) para obter mais detalhes.

O exemplo visto abaixo calcula as estatísticas para o `adc_geometric` e para **all** no conjunto de dados.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` não suporta os tipos de dados matriz ou mapa. Você pode definir um `skip_stats_for_complex_datatypes` sinalizador a ser notificado ou erro se o quadro de dados de entrada tiver colunas com matrizes e tipos de dados de mapa. Por padrão, o sinalizador é definido como verdadeiro. Para habilitar notificações ou erros, use o seguinte comando: `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

A saída do console não exibe as estatísticas em resposta ao comando analyze table compute statistics. Em vez disso, o console exibirá uma única coluna de linha de `Statistics ID` com um identificador universal exclusivo para fazer referência aos resultados. Você também pode optar por **consultar diretamente no`Statistics ID`**. Após a conclusão com êxito de um `COMPUTE STATISTICS` , os resultados são exibidos da seguinte maneira:

```console
| Statistics ID    | 
| ---------------- |
| adc_geometric_stats_1 |
(1 row)
```

Você pode consultar a saída da estatística diretamente fazendo referência à variável `Statistics ID` como se vê a seguir:

```sql
SELECT * FROM adc_geometric_stats_1; 
```

Essa instrução permite exibir a saída de maneira semelhante ao comando SHOW STATISTICS quando usado com o `Statistics ID`.

Você pode exibir uma lista de todas as estatísticas calculadas na sessão executando o comando SHOW STATISTICS. Um exemplo de saída do comando SHOW STATISTICS é visto abaixo.

```console
statsId | tableName | columnSet | filterContext | timestamp
-----------+---------------+-----------+---------------------------------------+---------------
adc_geometric_stats_1 |adc_geometric | (age) | | 25/06/2023 09:22:26
demo_table_stats_1 | demo_table | (*) | ((age > 25)) | 25/06/2023 12:50:26
```

<!-- Commented out until the <alias_name> feature is released.

To see the output, you must use the `SHOW STATISTICS` command. Instructions on [how to show the statistics](#show-statistics) are provided later in the document. 

-->

## Limitar as colunas incluídas {#limit-included-columns}

Você pode calcular estatísticas para colunas de conjunto de dados específicas referenciando-as por nome. Use o `FOR COLUMNS (<col1>, <col2>)` sintaxe para direcionar colunas específicas. O exemplo abaixo calcula estatísticas para as colunas  `commerce`, `id`, e `timestamp` para o conjunto de dados `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Você pode calcular as estatísticas para qualquer nível raiz ou coluna aninhada. O exemplo a seguir demonstra essas referências.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Adicionar uma condição de filtro de carimbo de data e hora {#filter-condition}

Você pode adicionar uma condição de filtro de carimbo de data e hora para focalizar a análise de suas colunas. Isso pode ser usado para filtrar dados históricos ou concentrar a análise de dados em um período específico. A variável `FILTERCONTEXT` O comando calcula estatísticas em um subconjunto do conjunto de dados com base na condição de filtro fornecida.

No exemplo abaixo, as estatísticas são computadas em todas as colunas do conjunto de dados `tableName`, em que o carimbo de data e hora da coluna tem valores entre o intervalo especificado de `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Você pode combinar o limite de coluna e o filtro para criar consultas computacionais altamente específicas para suas colunas de conjunto de dados. Por exemplo, a consulta a seguir calcula estatísticas nas colunas `commerce`, `id`, e `timestamp` para o conjunto de dados `tableName`, em que o carimbo de data e hora da coluna tem valores entre o intervalo especificado de `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

<!-- Commented out until the <alias_name> feature is released.
## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. 
-->

<!-- Commented out until the <alias_name> feature is released.

## Show the statistics {#show-statistics}

The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  

Even with a filter condition and a column list, the computation can target a large amount of data. Query Service generates a universally unique identifier for the statistics ID to store this calculated information. You can then use this statistics ID to look up the computed statistics with the `SHOW STATISTICS` command at any time within that session. 

The statistics ID and the statistics generated are only valid for this particular session and cannot be accessed across different PSQL sessions. The computed statistics are not currently persistent. To display the statistics, use the command seen below.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

An output might look similar to the example below. 

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(12 rows)
```

-->

## Próximas etapas {#next-steps}

Ao ler este documento, agora você tem uma melhor compreensão de como gerar estatísticas em nível de coluna a partir de um conjunto de dados ADLS usando uma consulta SQL. É recomendável ler a [Guia de sintaxe SQl](../sql/syntax.md) para conhecer mais recursos do Adobe Experience Platform Query Service.
