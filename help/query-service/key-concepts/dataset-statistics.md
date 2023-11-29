---
title: Computação de estatísticas do conjunto de dados
description: Este documento descreve como calcular estatísticas em nível de coluna nos conjuntos de dados do Azure Data Lake Storage (ADLS) com comandos SQL.
exl-id: 66f11cd4-b115-40b8-ba8a-c4bb3606bbbf
source-git-commit: 37aeff5131b9f67dbc99f6199918403e699478c8
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Cálculo das estatísticas do conjunto de dados

Agora é possível calcular estatísticas em nível de coluna no [!DNL Azure Data Lake Storage] (ADLS) com a variável `COMPUTE STATISTICS` Comando SQL. Os comandos SQL que calculam as estatísticas do conjunto de dados são uma extensão do `ANALYZE TABLE` comando. Detalhes completos sobre o `ANALYZE TABLE` comando pode ser encontrado no campo [Documentação de referência SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>As estatísticas calculadas são armazenadas em tabelas temporárias que têm persistência em nível de sessão. Você pode acessar os resultados dos cálculos a qualquer momento durante essa sessão. Elas não podem ser acessadas em diferentes sessões PSQL.

Para ver as estatísticas que foram calculadas com a variável `ANALYZE TABLE COMPUTE STATISTICS` você pode usar uma consulta SELECT no nome do alias ou na ID da estatística. Você também pode limitar o escopo da análise estatística a todo o conjunto de dados, a um subconjunto de um conjunto de dados, a todas as colunas ou a um subconjunto de colunas.

>[!IMPORTANT]
>
>A variável `COMPUTE STATISTICS`, `FILTERCONTEXT`, e `FOR COLUMNS` não há suporte para comandos em tabelas de armazenamento aceleradas. Essas extensões para o `ANALYZE TABLE` atualmente, só há suporte para comandos ADLS. Para obter mais informações, consulte [seção ANALISAR TABELA](../sql/syntax.md#analyze-table) do guia de sintaxe SQL.

Este guia ajuda a estruturar suas consultas para que você possa calcular as estatísticas de coluna de um conjunto de dados ADLS. Usando esses comandos, você pode ver as estatísticas geradas na sua sessão por meio de um cliente PSQL usando uma consulta SQL.

## Calcular estatísticas {#compute-statistics}

Construções adicionais foram adicionadas à `ANALYZE TABLE` comando que permite **calcular estatísticas para um subconjunto de um conjunto de dados e para determinadas colunas**. Para calcular estatísticas do conjunto de dados, você deve usar o `ANALYZE TABLE <tableName> COMPUTE STATISTICS` formato.

>[!IMPORTANT]
>
>O comportamento padrão calcula as estatísticas para o **conjunto de dados inteiro** e para **todas as colunas**. Para calcular estatísticas em todas as colunas, você usaria o formato de consulta `ANALYZE TABLE COMPUTE STATISTICS`. Você está **não** recomendado para usar o `COMPUTE STATISTICS` sem filtros em um conjunto de dados ADLS, pois o tamanho do conjunto de dados pode ser muito grande (potencialmente petabytes de dados). Em vez disso, você sempre deve considerar executar o comando analyze usando `FILTERCONTEXT` e uma lista especificada de colunas. Consulte as seções sobre [limitação de colunas analisadas](#limit-included-columns) e [adicionar uma condição de filtro](#filter-condition) para obter mais detalhes.

O exemplo visto abaixo calcula as estatísticas para o `adc_geometric` e para **all** no conjunto de dados.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>A variável `COMPUTE STATISTICS` comando não dá suporte aos tipos de dados matriz ou mapa. Você pode definir um `skip_stats_for_complex_datatypes` sinalizador a ser notificado ou para erro se o quadro de dados de entrada tiver colunas com matrizes e tipos de dados de mapa. Por padrão, o sinalizador é definido como verdadeiro. Para habilitar notificações ou erros, use o seguinte comando: `SET skip_stats_for_complex_datatypes = false`.

## Criar um nome de alias {#alias-name}

Como os resultados dos cálculos podem ser uma grande quantidade de dados, não é razoável retornar os dados calculados diretamente na saída do console. Embora os nomes de alias sejam opcionais, é recomendável usá-los como prática recomendada ao calcular estatísticas. Forneça um nome de alias na instrução para fazer referência descritiva aos resultados em suas consultas SQL. Como alternativa, um evento `Statistics ID` é gerado e usado para armazenar as informações calculadas.

O exemplo abaixo armazena as estatísticas de saída calculadas na variável `alias_name` para referência posterior. O nome do alias usado na consulta está disponível para referência assim que o `ANALYZE TABLE` comando foi executado.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

A saída para o exemplo acima é `SUCCESSFULLY COMPLETED, alias_name`. A saída do console não exibe as estatísticas na resposta ao comando analyze table compute statistics. Para ver os resultados detalhados, você deve usar uma consulta SELECT no nome do alias ou na ID da estatística.

## Exibir a saída de estatísticas calculadas {#view-output-of-computed-statistics}

Se você não fornecer um nome de alias antecipadamente, o Serviço de consulta gerará automaticamente um nome para o `Statistics ID` que segue o formato de `<tableName_stats_{incremental_number}>`. Se um nome de alias for fornecido, ele aparecerá no campo `Statistics ID` coluna.

Um exemplo de saída de um `COMPUTE STATISTICS` a consulta é a seguinte:

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

Você pode então **consultar diretamente as estatísticas calculadas** fazendo referência à variável `Statistics ID`. A instrução de exemplo abaixo permite visualizar a saída completamente quando usada com o `Statistics ID` ou o nome do alias.

```sql
SELECT * FROM adc_geometric_stats_1; 
```

A saída de estatísticas computadas pode ser semelhante ao exemplo abaixo.

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
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

## Mostrar os metadados da análise estatística {#show-statistics}

Você pode usar o `SHOW STATISTICS` comando para exibir os metadados de todas as estatísticas temporárias geradas na sessão. Este comando pode ajudá-lo a refinar o escopo da análise estatística.

Um exemplo de saída de `SHOW STATISTICS` é visto abaixo.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Uma descrição dos nomes das colunas de metadados é fornecida abaixo.

| Nome da coluna | Descrição |
|---|---|
| `statsId` | Essa ID faz referência à tabela de estatísticas temporárias gerada pelo `COMPUTE STATISTICS` comando. |
| `tableName` | A tabela original usada para análise. |
| `columnSet` | Uma lista de quaisquer colunas especificamente escolhidas para análise. Um valor vazio indica que todas as colunas foram analisadas. Consulte a seção sobre [limitação de colunas](#limit-included-columns) para obter mais informações. |
| `filterContext` | Uma lista de filtros aplicados à análise. |
| `timestamp` | Quaisquer filtros cronológicos aplicados à análise de dados para se concentrar em um período específico. Consulte a [seção condição de filtro de carimbo de data e hora](#filter-condition) para obter mais detalhes. |

Você pode usar o ID da estatística ou o nome do alias para pesquisar as estatísticas calculadas com uma instrução SELECT a qualquer momento nessa sessão. O ID da estatística e as estatísticas geradas são válidos apenas para esta sessão específica e não podem ser acessadas em sessões PSQL diferentes. As estatísticas computadas não são persistentes no momento. Consulte a seção sobre como [exibir a saída das estatísticas calculadas](#view-output-of-computed-statistics) para obter mais detalhes.

## Limitar as colunas incluídas {#limit-included-columns}

Para focalizar sua análise, você pode calcular estatísticas para colunas de conjunto de dados específicas referenciando-as por nome. Use o `FOR COLUMNS (<col1>, <col2>)` sintaxe para direcionar colunas específicas. O exemplo abaixo calcula as estatísticas das colunas  `commerce`, `id`, e `timestamp` para o conjunto de dados `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Você pode calcular as estatísticas para qualquer nível raiz ou coluna aninhada. O exemplo a seguir demonstra essas referências.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Adicionar uma condição de filtro de carimbo de data e hora {#filter-condition}

Para focalizar a análise das colunas com base na cronologia, você pode adicionar uma condição de filtro de carimbo de data e hora. Essa condição pode ser usada para filtrar dados históricos ou concentrar a análise de dados em um período específico. A variável `FILTERCONTEXT` O comando calcula estatísticas em um subconjunto do conjunto de dados com base na condição de filtro fornecida.

No exemplo abaixo, as estatísticas são computadas em todas as colunas do conjunto de dados `tableName`, em que o carimbo de data e hora da coluna tem valores entre o intervalo especificado de `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Você pode combinar o limite de coluna e o filtro para criar consultas computacionais altamente específicas para suas colunas de conjunto de dados. Por exemplo, a consulta a seguir calcula estatísticas nas colunas `commerce`, `id`, e `timestamp` para o conjunto de dados `tableName`, em que o carimbo de data e hora da coluna tem valores entre o intervalo especificado de `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Próximas etapas {#next-steps}

Ao ler este documento, agora você tem uma melhor compreensão de como gerar estatísticas em nível de coluna a partir de um conjunto de dados ADLS usando uma consulta SQL. É recomendável ler a [Guia de sintaxe SQl](../sql/syntax.md) para conhecer mais recursos do Adobe Experience Platform Query Service.
