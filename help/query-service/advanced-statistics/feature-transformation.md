---
title: Técnicas de transformação de recursos
description: Saiba mais sobre técnicas essenciais de pré-processamento, como transformação de dados, codificação e dimensionamento de recursos, que preparam dados para o treinamento de modelos estatísticos. Ele aborda a importância de lidar com valores ausentes e converter dados categóricos para melhorar o desempenho e a precisão do modelo.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '3437'
ht-degree: 8%

---

# Técnicas de transformação de recursos

As transformações são etapas cruciais de pré-processamento que convertem ou dimensionam dados em um formato adequado para treinamento e análise de modelo, garantindo desempenho e precisão ideais. Este documento serve como um recurso de sintaxe complementar, fornecendo detalhes detalhados sobre as principais técnicas de transformação de recursos para pré-processamento de dados.

Os modelos de aprendizado de máquina não podem processar diretamente valores de sequência de caracteres ou valores nulos, tornando o pré-processamento de dados essencial. Este guia explica como usar várias transformações para imputar valores ausentes, converter dados categóricos em formatos numéricos e aplicar técnicas de dimensionamento de recursos, como codificação e vetorização one-hot. Esses métodos permitem que os modelos interpretem e aprendam efetivamente com os dados, melhorando, em última análise, o desempenho.

## Transformação automática de recursos {#automatic-transformations}

Se você optar por ignorar a cláusula `TRANSFORM` no comando `CREATE MODEL`, a transformação de recursos ocorrerá automaticamente. O pré-processamento automático de dados inclui transformações de substituição nula e de recursos padrão (com base no tipo de dados ). As colunas numéricas e de texto são automaticamente imputadas e as transformações de recursos são realizadas para garantir que os dados estejam em um formato adequado para o treinamento do modelo de aprendizado de máquina. Esse processo inclui imputação de dados ausentes e transformações categóricas, numéricas e booleanas.

>[!IMPORTANT]
>
>A transformação de recursos utilizada no momento do treino será também utilizada para a transformação de recursos no momento da previsão e avaliação.

As tabelas a seguir explicam como tipos de dados diferentes são tratados quando a cláusula `TRANSFORM` é omitida durante o comando `CREATE MODEL`.

### Substituição nula {#automatic-null-replacement}

| Tipo de dados | Substituição nula |
|-----------------|-----------------------------------------------------|
| Numérico | Nulos são substituídos pelo valor médio da coluna. |
| Categórico | Nulos são substituídos pela palavra-chave `ml_unknown`. |
| Booleano | Nulos são substituídos por um valor `FALSE`. |
| Carimbo de data e hora | Espera-se que esse campo seja contínuo. |
| Aninhado/STRUCT | A substituição depende do tipo de dados do nó folha. |

### Transformação de recursos {#automatic-feature-transformation}

| Tipo de dados | Transformação de recurso |
|-----------------|-----------------------------------------------------|
| Numérico | NÃO OBRIGATÓRIO - Como esse tipo de dados é entendido pelos algoritmos de aprendizado de máquina do. |
| String | A indexação da string ocorre. |
| Booleano | A indexação da string ocorre. |
| Carimbo de data e hora | Nenhuma operação ocorre. |
| STRUCT | O valor é expandido para seu nó folha. A transformação ocorre com base no tipo de dados do nó folha. |

**exemplo**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Transformações manuais de recursos {#manual-transformations}

Para definir o pré-processamento de dados personalizado na instrução `CREATE MODEL`, use a cláusula `TRANSFORM` em combinação com qualquer número de funções de transformação disponíveis. Essas funções de pré-processamento manual também podem ser usadas fora da cláusula `TRANSFORM`. Todas as transformações discutidas na [seção de transformador abaixo](#available-transformations) podem ser usadas para pré-processar os dados manualmente.

### Características principais

Estas são as principais características da transformação de recursos a serem consideradas ao definir suas funções de pré-processamento:

- **Sintaxe**: `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - O nome do alias é obrigatório na sintaxe. Você deve fornecer um nome de alias, caso contrário a consulta falhará.

- **Parâmetros**: os parâmetros são argumentos posicionais. Isso significa que cada parâmetro só pode ter determinados valores. Consulte a documentação relevante para obter detalhes sobre qual função aceita qual argumento.

- **Transformadores de encadeamento**: a saída de um transformador pode se tornar a entrada para outro transformador.

- **Uso de recursos**: a última transformação de recursos é usada como um recurso do modelo de aprendizado de máquina.

**Exemplo**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## Transformações disponíveis {#available-transformations}

Há 19 transformações disponíveis. Essas transformações estão divididas em [Transformações gerais](#general-transformations), [Transformações numéricas](#numeric-transformations), [Transformações categóricas](#categorical-transformations) e [Transformações textuais](#textual-transformations).

### Transformações gerais {#general-transformations}

Leia esta seção para obter detalhes sobre os transformadores usados para uma grande variedade de tipos de dados. Essas informações são essenciais se você precisar aplicar transformações que não são específicas para dados categóricos ou textuais.

>[!NOTE]
>
>O tipo de dados de entrada refere-se à coluna na qual a imputação é aplicada. O tipo de dados de saída se refere à coluna que é produzida como uma saída depois que a transformação entra em vigor.

#### Imputador numérico {#numeric-imputer}

O transformador **imputador numérico** conclui valores ausentes em um conjunto de dados. Usa a média, a mediana ou o modo das colunas em que os valores ausentes estão localizados. As colunas de entrada devem ser `DoubleType` ou `FloatType`. Mais informações e exemplos podem ser encontrados na [documentação do algoritmo Spark](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer).

>[!NOTE]
>
>Todos os valores nulos nas colunas de entrada são tratados como ausentes e, portanto, também imputados.

**Tipos de dados**

- Tipo de dados de entrada: Numérico
- Tipo de dados de saída: Numérico

**Definição**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | Uma estratégia de imputação. Valores disponíveis: [`mean`, `median`, `mode`]. | sequência de caracteres | média | opcional |

{style="table-layout:auto"}

**Exemplo antes da imputação**

| ID | hora |
|---|---|
| 0 | 18,0 |
| 1 | nulo |
| 2 | 8,0 |

**Exemplo após imputação (usando estratégia média)**

| ID | hora |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Imputador de string {#string-imputer}

O transformador **imputador de cadeia de caracteres** conclui valores ausentes em um conjunto de dados usando uma cadeia de caracteres fornecida pelo usuário como um argumento de função. As colunas de entrada e saída devem ser do tipo de dados `string`.

>[!NOTE]
>
>Todos os valores nulos nas colunas de entrada são tratados como ausentes e substituídos pela cadeia de caracteres especificada.

**Tipos de dados**

- Tipo de dados de entrada: cadeia de caracteres
- Tipo de dados de saída: cadeia de caracteres

**Definição**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | O valor que substitui nulos. | sequência de caracteres | ml_unknown | opcional |

{style="table-layout:auto"}

**Exemplo antes da imputação**

| ID | name |
|---|---|
| 0 | John |
| 1 | nulo |
| 2 | Alice |

**Exemplo após imputação (usando &#39;ml_unknown&#39; como substituição)**

| ID | name |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Imputador booleano {#imputer}

O transformador **imputador booleano** conclui valores ausentes em um conjunto de dados para uma coluna booleana. As colunas de entrada e saída devem ser do tipo `Boolean`.

>[!NOTE]
>
>Todos os valores nulos nas colunas de entrada são tratados como ausentes e substituídos pelo valor booleano especificado.

**Tipos de dados**

- Tipo de dados de entrada: Booleano
- Tipo de dados de saída: Booleano

**Definição**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Imputador booleano. Valores permitidos: [`true`, `false`]. | booleano | false | opcional |

**Exemplo antes da imputação**

| ID | sinalizador |
|---|---|
| 0 | true |
| 1 | nulo |
| 2 | false |

**Exemplo após imputação (usando &#39;true&#39; como substituição)**

| ID | sinalizador |
|---|---|
| 0 | true |
| 1 | true |
| 2 | false |

#### Montador de vetor {#vector-assembler}

O transformador `VectorAssembler` combina uma lista especificada de colunas de entrada em uma única coluna de vetor, facilitando o gerenciamento de vários recursos em modelos de aprendizado de máquina. Isso é particularmente útil para mesclar recursos brutos e gerados por diferentes transformadores de recursos em um vetor de recursos unificado. `VectorAssembler` aceita colunas de entrada de tipos numéricos, booleanos e vetoriais. Em cada linha, os valores das colunas de entrada são concatenados em um vetor na ordem especificada.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Tipos de dados**

- Tipo de dados de entrada: `array[string]` (nomes de coluna com valores numéricos/de matriz[numéricos])
- Tipo de dados de saída: `Vector[double]`

**Definição**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
| -------- | ------------ | ----- | -------- | -------- |
| ND | Não são necessários parâmetros adicionais para esse transformador. | ND | ND | ND |

{style="table-layout:auto"}

**Exemplo antes da transformação**

| ID | hora | dispositivos móveis | userFeatures | clicado |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1,0 | [0.0, 10.0, 0.5] | 1,0 |

{style="table-layout:auto"}

**Exemplo após a transformação**

| ID | hora | dispositivos móveis | userFeatures | clicado | recursos |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1,0 | [0.0, 10.0, 0.5] | 1,0 | [18.0, 1.0, 0.0, 10.0, 0.5] |

{style="table-layout:auto"}

### Transformações numéricas {#numeric-transformations}

Leia esta seção para saber mais sobre os transformadores disponíveis para processamento e dimensionamento de dados numéricos. Esses transformadores são necessários para manipular e otimizar recursos numéricos em seus conjuntos de dados.

#### Binarizador {#binarizer}

O transformador `Binarizer` converte recursos numéricos em recursos binários (0/1) por meio de um processo chamado binarização. Valores de recurso maiores que o limite especificado são convertidos para 1.0, enquanto valores iguais ou inferiores ao limite são convertidos para 0.0. O `Binarizer` dá suporte aos tipos `Vector` e `Double` para a coluna de entrada.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**Tipos de dados**

- Tipo de dados de entrada: coluna numérica
- Tipo de dados de saída: Numérico

**Definição**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | Parâmetro do limite usado para binarizar recursos contínuos. Os recursos maiores que o limite são binarizados para 1.0, enquanto os recursos iguais ou menores que o limite são binarizados para 0.0. | int/double | 0,0 | opcional |

{style="table-layout:auto"}

**Exemplo de entrada antes da binarização**

| ID | avaliação |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**Exemplo de saída após a binarização (limite padrão de 0,0)**

| ID | avaliação |
|---|---------|
| 0 | 0,0 |
| 1 | 1,0 |
| 2 | 1,0 |

**Definição com limite personalizado**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**Exemplo de saída após binarização (com um limite de 14.0)**

| ID | idade |
|---|-------|
| 0 | 0,0 |
| 1 | 0,0 |
| 2 | 1,0 |

#### Bucketizer {#bucketizer}

O transformador `Bucketizer` converte uma coluna de recursos contínuos em uma coluna de compartimentos de recursos, com base em limites especificados pelo usuário. Esse processo é útil para segmentar dados contínuos em compartimentos ou compartimentos discretos. `Bucketizer` requer um parâmetro `splits`, que define os limites dos buckets.

**Tipos de dados**

- Tipo de dados de entrada: coluna numérica
- Tipo de dados de saída: Numérico (valores agrupados)

**Definição**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | Um parâmetro para mapear recursos contínuos em compartimentos. Com `n+1` divisões, há `n` compartimentos. As divisões devem estar em ordem estritamente crescente, e o intervalo (x,y) é usado para cada bucket, exceto o último, que inclui y. | matriz (duplo) | N/D | opcional |

{style="table-layout:auto"}

**Exemplos de divisões**

- Matriz(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Matriz(0.0, 1.0, 2.0)

As divisões devem abranger todo o intervalo de valores Double; caso contrário, os valores fora das divisões especificadas serão tratados como erros.

**Exemplo de transformação**

Este exemplo pega uma coluna de recursos contínuos (`course_duration`), agrupa-a de acordo com o `splits` fornecido e monta os compartimentos resultantes com outros recursos.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

O transformador `MinMaxScaler` redimensiona cada recurso em um conjunto de dados de linhas de vetor para um intervalo especificado, normalmente [0, 1]. Isso garante que todos os recursos contribuam igualmente para o modelo. É particularmente útil para modelos sensíveis ao dimensionamento de recursos, como algoritmos baseados em descida de gradiente. O `MinMaxScaler` opera nos seguintes parâmetros:

- **min**: o limite inferior da transformação, compartilhado por todos os recursos. O padrão é `0.0`.
- **max**: O limite superior da transformação, compartilhado por todos os recursos. O padrão é `1.0`.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**Tipos de dados**

- Tipo de dados de entrada: `Array[Double]`
- Tipo de dados de saída: `Array[Double]`

**Definição**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | Limite inferior após a transformação, compartilhado por todos os recursos. | duplo | 0,0 | opcional |
| `max` | Limite superior após a transformação, compartilhado por todos os recursos. | duplo | 1,0 | opcional |

**Exemplo de transformação**

Este exemplo transforma um conjunto de recursos, redimensionando-os para o intervalo especificado usando MinMaxScaler após aplicar várias outras transformações.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

O transformador `MaxAbsScaler` redimensiona cada recurso em um conjunto de dados de linhas de vetor para o intervalo [-1, 1] dividindo pelo valor absoluto máximo de cada recurso. Essa transformação é ideal para preservar a dispersão em conjuntos de dados com valores positivos e negativos, pois não altera ou centraliza os dados. Isso torna o `MaxAbsScaler` particularmente adequado para modelos que são sensíveis à escala de recursos de entrada, como aqueles que envolvem cálculos de distância.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**Tipos de dados**

- Tipo de dados de entrada: `Array[Double]`
- Tipo de dados de saída: `Array[Double]`

**Definição**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| ND | MaxAbsScaler não requer parâmetros adicionais para sua operação. | ND | ND | ND |

**Exemplo de transformação**

Este exemplo aplica várias transformações, incluindo `MaxAbsScaler`, para redimensionar recursos no intervalo [-1, 1].

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normalizador {#normalizer}

`Normalizer` é um transformador que normaliza cada vetor em um conjunto de dados de linhas de vetor para ter uma norma de unidade. Esse processo garante uma escala consistente sem alterar a direção dos vetores. Essa transformação é particularmente útil em modelos de aprendizado de máquina que dependem de medidas de distância ou outros cálculos baseados em vetores, especialmente quando a magnitude dos vetores varia significativamente.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**Tipos de dados**

- Tipo de dados de entrada: `array[double]` / `vector[double]`
- Tipo de dados de saída: `vector[double]`

**Definição**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | Especifica o `p-norm` usado para normalização (por exemplo, `1-norm`, `2-norm`, etc.). | inteiro | 2 | opcional |

**Exemplo de transformação**

Este exemplo demonstra como aplicar várias transformações, incluindo o `Normalizer`, para normalizar um conjunto de recursos usando o `p-norm` especificado.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

O `QuantileDiscretizer` é um transformador que converte uma coluna com recursos contínuos em recursos categóricos agrupados, com o número de agrupamentos determinado pelo parâmetro `numBuckets`. Em alguns casos, o número real de buckets pode ser menor do que o número especificado se houver poucos valores distintos para criar quantidades suficientes.

Essa transformação é particularmente útil para simplificar a representação de dados contínuos ou prepará-la para algoritmos que funcionam melhor com entradas categóricas.

**Tipos de dados**

- Tipo de dados de entrada: coluna numérica
- Tipo de dados de saída: coluna numérica (categórica)

**Definição**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | O número de buckets (quantis ou categorias) nos quais os pontos de dados são agrupados. Esse número deve ser maior ou igual a dois. | inteiro | 2 | opcional |

**Exemplo de transformação**

Este exemplo demonstra como o `QuantileDiscretizer` agrupa uma coluna de recursos contínuos (`hour`) em três compartimentos categóricos.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Exemplo antes e depois da diferenciação**

| ID | hora | resultado |
|---|------|--------|
| 0 | 18,0 | 2.0 |
| 1 | 19,0 | 2.0 |
| 2 | 8,0 | 1,0 |
| 3 | 5.0 | 1,0 |
| 4 | 2,2 | 0,0 |

#### StandardScaler {#standardscaler}

O `StandardScaler` é um transformador que normaliza cada recurso em um conjunto de dados de linhas de vetor para ter um desvio padrão de unidade e/ou média zero. Esse processo torna os dados mais adequados para algoritmos que assumem que os recursos são centralizados em torno de zero com uma escala consistente. Essa transformação é particularmente importante para modelos de aprendizado de máquina como SVM, regressão logística e redes neurais, onde dados não padronizados podem levar a problemas de convergência ou precisão reduzida.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**Tipos de dados**

- Tipo de dados de entrada: vetor
- Tipo de dados de saída: vetor

**Definição**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | Dimensiona os dados para ter o desvio padrão da unidade. | booleano | Verdadeiro | opcional |
| `withMean` | Centraliza os dados com a média antes do dimensionamento. Essa opção produz saída densa, portanto, tenha cuidado com entradas esparsas. | booleano | Falso | opcional |

**Exemplo de transformação**

Este exemplo demonstra como aplicar o StandardScaler a um conjunto de recursos, normalizando-os com desvio padrão de unidade e média zero.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Transformações categóricas {#categorical-transformations}

Leia esta seção para obter uma visão geral dos transformadores disponíveis criados para converter e pré-processar dados categóricos para modelos de aprendizado de máquina do. Essas transformações são projetadas para pontos de dados que representam categorias ou rótulos distintos, em vez de valores numéricos.

#### IndexadorDeCadeiaDeCaracteres {#stringindexer}

`StringIndexer` é um transformador que codifica uma coluna de rótulos de cadeia de caracteres em uma coluna de índices numéricos. Os índices variam de 0 a `numLabels` e são ordenados por frequência de rótulo (o rótulo mais frequente recebe um índice de 0). Se a coluna de entrada for numérica, ela será convertida em uma string antes da indexação. Rótulos não vistos podem ser atribuídos ao índice `numLabels` se especificados pelo usuário.

Essa transformação é particularmente útil para converter dados de sequência categórica em forma numérica, tornando-a adequada para modelos de aprendizado de máquina que exigem entrada numérica.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**Tipos de dados**

- Tipo de dados de entrada: cadeia de caracteres
- Tipo de dados de saída: Numérico

**Definição**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------|-------------|------|---------|----------|
| ND | `StringIndexer` não requer parâmetros adicionais para sua operação. | ND | ND | ND |

**Exemplo de transformação**

Este exemplo demonstra como aplicar o `StringIndexer` a um recurso categórico, convertendo-o em um índice numérico.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

`OneHotEncoder` é um transformador que converte uma coluna de índices de rótulos em uma coluna de vetores binários esparsos, onde cada vetor tem no máximo um único valor. Essa codificação é particularmente útil para permitir que algoritmos que exigem entrada numérica, como Regressão lógica, incorporem dados categóricos de maneira eficaz.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**Tipos de dados**

- Tipo de dados de entrada: Numérico
- Tipo de dados de saída: Vetor[Int]

**Definição**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------|-------------|------|---------|----------|
| ND | O OneHotEncoder não requer parâmetros adicionais para sua operação. | ND | ND | ND |

**Exemplo de transformação**

Este exemplo demonstra como aplicar primeiro o `StringIndexer` a um recurso categórico e, em seguida, usar o `OneHotEncoder` para converter os valores indexados em um vetor binário.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Transformações textuais {#textual-transformations}

Esta seção fornece detalhes sobre os transformadores disponíveis para processar e converter dados de texto em formatos que podem ser usados por modelos de aprendizado de máquina. Esta seção é crucial para desenvolvedores que trabalham com dados de linguagem natural e análise de texto.

#### CountVetorizer {#countvectorizer}

O `CountVectorizer` é um transformador que converte uma coleção de documentos de texto em vetores de contagem de tokens, produzindo representações esparsas com base no vocabulário extraído do corpus. Essa transformação é essencial para converter dados de texto em um formato numérico que pode ser usado por algoritmos de aprendizado de máquina, como LDA (Latent Dirichlet Allocation), representando a frequência de tokens em cada documento.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Tipos de dados**

- Tipo de dados de entrada: Matriz[Cadeia de caracteres]
- Tipo de dados de saída: Vetor denso

**Definição**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Tamanho máximo do vocabulário. CountVetorizer cria um vocabulário que considera apenas os `vocabSize` termos principais ordenados por frequência de termo no corpo. | Int | 218 | opcional |
| `MIN_DOC_FREQ` | Especifica o número mínimo de documentos diferentes que um termo deve aparecer para ser incluído no vocabulário. Pode ser um número absoluto ou uma fração de documentos (se for duplo). | Duplo | 1,0 | opcional |
| `MAX_DOC_FREQ` | Especifica o número máximo de documentos diferentes que um termo pode aparecer para ser incluído no vocabulário. Pode ser um número absoluto ou uma fração de documentos (se for duplo). | Duplo | (263)-1 | opcional |
| `MIN_TERM_FREQ` | Filtra palavras raras em um documento. Os termos com frequência/contagem menor que o limite fornecido são ignorados. Pode ser um número absoluto ou uma fração da contagem de tokens do documento. | Duplo | 1,0 | opcional |

{style="table-layout:auto"}

**Exemplo de transformação**

Este exemplo demonstra como o CountVetorizer converte uma coleção de matrizes de texto em vetores de contagens de token, produzindo uma representação esparsa.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Exemplo antes e depois da vetorização**

| ID | textos | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;) | (3,[0,1,2],[1.0,1.0,1.0]) |
| 1 | Array(&quot;a&quot;, &quot;b&quot;, &quot;b&quot;, &quot;c&quot;, &quot;a&quot;) | (3,[0,1,2],[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

O `NGram` é um transformador que gera uma sequência de n-gramas, onde um n-grama é uma sequência de tokens (&#39;??&#39;) (normalmente palavras) para algum inteiro (`𝑛`). A saída consiste em strings delimitadas por espaços de &#39;??&#39; palavras consecutivas, que podem ser usadas como recursos em modelos de aprendizado de máquina, particularmente aqueles focados no processamento de linguagem natural.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Tipos de dados**

- Tipo de dados de entrada: Matriz[Cadeia de caracteres]
- Tipo de dados de saída: Matriz[Cadeia]

**Definição**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | O comprimento mínimo de n-gramas deve ser maior ou igual a 1. | inteiro | 2 (recursos de bigrama) | opcional |

{style="table-layout:auto"}

**Exemplo de transformação**

Este exemplo demonstra como o transformador NGram cria uma sequência de 3 gramas de uma lista de tokens derivados de dados de texto.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Exemplo antes e depois da transformação n-grama**

| ID | textos | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;este&quot;, &quot;era&quot;, &quot;um&quot;, &quot;entretenimento&quot;, &quot;filme&quot;] | [&quot;este foi um&quot;, &quot;foi um filme divertido&quot;, &quot;um filme divertido&quot;] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

O `StopWordsRemover` é um transformador que remove palavras de interrupção de uma sequência de cadeias de caracteres, filtrando palavras comuns que não têm significado significativo. Ele assume como entrada uma sequência de cadeias de caracteres (como a saída de um tokenizador) e remove todas as palavras de interrupção especificadas pelo parâmetro `stopWords`.

Essa transformação é útil para pré-processar dados de texto, melhorando a eficácia de modelos de aprendizado de máquina downstream ao eliminar palavras que não contribuem muito para o significado geral.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Tipos de dados**

- Tipo de dados de entrada: Matriz[Cadeia de caracteres]
- Tipo de dados de saída: Matriz[Cadeia]

**Definição**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | As palavras a serem filtradas. | matriz [cadeia] | Por padrão: Inglês stop words | opcional |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**Exemplo de transformação**

Este exemplo mostra como o `StopWordsRemover` filtra palavras de interrupção comuns em inglês de uma lista de tokens.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Exemplo antes e depois da remoção de palavras de interrupção**

| ID | raw | filtrado |
|----|------------------------------|--------------------------|
| 0 | [Eu, vi, o, vermelho, balão] | [serra, vermelha, balão] |
| 1 | [Maria, teve, um, pequeno, cordeiro] | [Maria, pequena, cordeiro] |

**Exemplo com palavras de interrupção personalizadas**

Este exemplo demonstra como usar uma lista personalizada de palavras de interrupção para filtrar palavras específicas das sequências de entrada.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Exemplo antes e depois da remoção de palavras de interrupção personalizadas**

| ID | raw | filtrado |
|----|------------------------------|--------------------------|
| 0 | [Eu, vi, o, vermelho, balão] | [viu, o, balão] |
| 1 | [Maria, teve, um, pequeno, cordeiro] | [Maria, pequena, cordeiro] |

#### TF- IDF {#tf-idf}

O `TF-IDF` (Frequência de termo-frequência inversa do documento) é um transformador usado para medir a importância de uma palavra dentro de um documento relativo a um corpo. Frequência do termo (TF) refere-se ao número de vezes que um termo \(t\) aparece em um documento \(d\), enquanto frequência do documento (DF) mede quantos documentos no corpo \(D\) contêm o termo \(t\). Esse método é amplamente utilizado na mineração de texto para reduzir a influência de palavras comuns, como &quot;a&quot;, &quot;o&quot; e &quot;de&quot;, que trazem pouca informação única.

Essa transformação é particularmente valiosa em tarefas de mineração de texto e processamento de linguagem natural, pois atribui um valor numérico à importância de cada palavra em um documento e em todo o corpo.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**Tipos de dados**

- Tipo de dados de entrada: Matriz[Cadeia de caracteres]
- Tipo de dados de saída: Vetor[Int]

**Definição**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | O número de recursos a serem gerados. Deve ser superior a 0. | Int | 262144 | opcional |
| `MIN_DOC_FREQ` | O número mínimo de documentos nos quais um termo deve parecer estar incluído no modelo. | Int | 0 | opcional |

{style="table-layout:auto"}

**Exemplo de transformação**

Este exemplo demonstra como usar TF-IDF para transformar frases tokenizadas em um vetor de recursos que representa a importância de cada termo no contexto de todo o corpo.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

O `Tokenizer` é um transformador que divide o texto, como uma frase, em termos individuais, geralmente palavras. Ele converte sentenças em matrizes de tokens, fornecendo uma etapa fundamental no pré-processamento de texto que prepara os dados para análise de texto adicional ou processos de modelagem.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Tipos de dados**

- Tipo de dados de entrada: sentença textual
- Tipo de dados de saída: Matriz[Cadeia]

**Definição**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|-----------|-------------|------|---------|----------|
| ND | O `Tokenizer` não requer parâmetros adicionais para sua operação. | ND | ND | ND |

**Exemplo de transformação**

Este exemplo demonstra como o `Tokenizer` divide frases em palavras individuais (tokens) como parte de um pipeline de processamento de texto.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

O `Word2Vec` é um estimador que processa sequências de palavras representando documentos e treina um `Word2VecModel`. Esse modelo mapeia cada palavra para um vetor de tamanho fixo exclusivo e transforma cada documento em um vetor, calculando a média dos vetores de todas as palavras no documento. Amplamente usado em tarefas de processamento de linguagem natural, o `Word2Vec` cria incorporações de palavras que capturam o significado semântico, convertendo dados de texto em vetores numéricos que representam as relações entre as palavras e habilitando análises de texto e modelos de aprendizado de máquina mais eficazes.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**Tipos de dados**

- Tipo de dados de entrada: Matriz[Cadeia de caracteres]
- Tipo de dados de saída: Vetor[Double]

**Definição**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Parâmetros**

| Parâmetro | Descrição | Tipo | Padrão | Opcional |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | A dimensão do vetor em que cada palavra é transformada. | Número inteiro | 100 | opcional |
| `MIN_COUNT` | O número mínimo de vezes que um token deve aparecer para ser incluído no vocabulário do modelo `Word2Vec`. | Número inteiro | 5 | opcional |

{style="table-layout:auto"}

**Exemplo de transformação**

Este exemplo mostra como `Word2Vec` converte uma revisão tokenizada em um vetor de tamanho fixo que representa a média dos vetores de palavras no documento.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Exemplo antes e depois da transformação do Word2Vec**

| revisão | tokenizado | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| este foi um filme divertido | [este, foi, um, divertido, filme] | [-0.025713888928294182,0.00818799751577899,0.0092235435731709,-0.0151538523377 7133,0.012175946310162545,3.1129065901041035E-4,0.0025145105042611252,0.0057570 19785232843,-0.021328244300093502,0.009335877187550069] |

{style="table-layout:auto"}
