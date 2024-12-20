---
title: Algoritmos de regressão
description: Saiba como configurar e otimizar vários algoritmos de regressão com parâmetros importantes, descrições e código de exemplo para ajudar a implementar modelos estatísticos avançados.
role: Developer
exl-id: d38733bb-0420-40bf-a70b-19e0e0e58730
source-git-commit: 8b9cfb48a11701f0e4b358416c6b627bedf1db8b
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 4%

---

# Algoritmos de regressão {#regression-algorithms}

Este documento fornece uma visão geral de vários algoritmos de regressão, com foco em sua configuração, parâmetros principais e uso prático em modelos estatísticos avançados. Algoritmos de regressão são são usados para modelar a relação entre variáveis dependentes e independentes, prevendo resultados contínuos com base em dados observados. Cada seção inclui descrições de parâmetros e código de exemplo para ajudar você a implementar e otimizar esses algoritmos para tarefas como linear, random forest e regressão de sobrevivência.

## Regressão [!DNL Decision Tree] {#decision-tree-regression}

O aprendizado [!DNL Decision Tree] é um método de aprendizado supervisionado usado em estatísticas, mineração de dados e aprendizado de máquina. Nesta abordagem, uma árvore decisória de classificação ou regressão é usada como modelo preditivo para tirar conclusões sobre um conjunto de observações.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho dos modelos de árvore de decisão.

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Esse parâmetro especifica o número máximo de compartimentos usados para discretizar recursos contínuos e determinar divisões em cada nó. Mais compartimentos resultam em granularidade e detalhes mais finos. | 32 | Deve ser pelo menos 2 e pelo menos o número de categorias em qualquer recurso categórico. |
| `CACHE_NODE_IDS` | Esse parâmetro determina se as IDs de nó devem ser armazenadas em cache para cada instância. Se `false`, o algoritmo transmite árvores para executores para corresponder instâncias com nós. Se `true`, o algoritmo armazenará em cache IDs de nó para cada instância, o que pode acelerar o treinamento de árvores mais profundas. Os usuários podem configurar a frequência com que o cache deve ser marcado ou desabilitá-lo configurando `CHECKPOINT_INTERVAL`. | false | `true` ou `false` |
| `CHECKPOINT_INTERVAL` | Esse parâmetro especifica a frequência com que as IDs de nó em cache devem ser marcadas. Por exemplo, defini-lo como `10` significa que o cache terá ponto de verificação a cada 10 iterações. Isso só é aplicável se `CACHE_NODE_IDS` estiver definido como `true` e o diretório do ponto de verificação estiver configurado em `org.apache.spark.SparkContext`. | 10 | (>=1) |
| `IMPURITY` | Esse parâmetro especifica o critério usado para calcular o ganho de informações. Os valores com suporte são `entropy` e `gini`. | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Esse parâmetro especifica a profundidade máxima da árvore. Por exemplo, uma profundidade de `0` significa 1 nó de folha, enquanto uma profundidade de `1` significa 1 nó interno e 2 nós de folha. A profundidade deve estar dentro do intervalo `[0, 30]`. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Esse parâmetro define o ganho mínimo de informações necessário para que uma divisão seja considerada válida em um nó de árvore. | 0,0 | (>=0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Esse parâmetro especifica a fração mínima da contagem de amostra ponderada que cada nó filho deve ter após uma divisão. Se qualquer nó secundário tiver uma fração menor que esse valor, a divisão será descartada. | 0,0 | [0.0, 0.5] |
| `MIN_INSTANCES_PER_NODE` | Esse parâmetro define o número mínimo de instâncias que cada nó secundário deve ter após uma divisão. Se uma divisão resultar em menos instâncias do que esse valor, a divisão será descartada como inválida. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Esse parâmetro especifica a memória máxima, em megabytes (MB), alocada para agregação de histograma. Se a memória for muito pequena, somente um nó será dividido por iteração e suas agregações poderão exceder esse tamanho. | 256 | Qualquer valor inteiro positivo |
| `PREDICTION_COL` | Esse parâmetro especifica o nome da coluna usada para armazenar previsões. | &quot;previsão&quot; | Qualquer string |
| `SEED` | Esse parâmetro define a seed aleatória usada no modelo. | None | Qualquer número de 64 bits |
| `WEIGHT_COL` | Esse parâmetro especifica o nome da coluna de peso. Se este parâmetro não estiver definido ou estiver vazio, todos os pesos da instância serão tratados como `1.0`. | Não definido | Qualquer string |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressão [!DNL Factorization Machines] {#factorization-machines-regression}

[!DNL Factorization Machines] é um algoritmo de aprendizado de regressão com suporte para descida de gradiente normal e resolução AdamW. O algoritmo é baseado no artigo de S. Rendle (2010), &quot;[!DNL Factorization Machines].&quot;

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho da regressão [!DNL Factorization Machines].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|------------------------|-------------------------------------------------------------------------------------------------|---------------|-----------------------|
| `TOL` | Esse parâmetro especifica a tolerância de convergência para o algoritmo. Valores mais altos podem resultar em convergência mais rápida, mas com menos precisão. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Esse parâmetro define a dimensionalidade dos fatores. Valores mais altos aumentam a complexidade do modelo. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Esse parâmetro indica se o modelo deve incluir um termo de interceptação. | `true` | `true`, `false` |
| `FIT_LINEAR` | Esse parâmetro especifica se um termo linear (também chamado de termo unidirecional) deve ser incluído no modelo. | `true` | `true`, `false` |
| `INIT_STD` | Esse parâmetro define o desvio padrão dos coeficientes iniciais usados no modelo. | 0,01 | (>= 0) |
| `MAX_ITER` | Esse parâmetro especifica o número máximo de iterações para execução do algoritmo. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Esse parâmetro define a fração de minilote, que determina a parte dos dados usada em cada lote. Deve estar no intervalo `(0, 1]`. | 1,0 | `(0, 1]` |
| `REG_PARAM` | Esse parâmetro define o parâmetro de regularização para evitar a sobreposição. | 0,0 | (>= 0) |
| `SEED` | Esse parâmetro especifica a seed aleatória usada para inicialização de modelo. | None | Qualquer número de 64 bits |
| `SOLVER` | Esse parâmetro especifica o algoritmo de resolução usado para otimização. | &quot;adamW&quot; | `gd` (descida de gradiente), `adamW` |
| `STEP_SIZE` | Esse parâmetro especifica o tamanho da etapa inicial (ou a taxa de aprendizagem) para a primeira etapa de otimização. | 1,0 | Qualquer valor positivo |
| `PREDICTION_COL` | Esse parâmetro especifica o nome da coluna em que as previsões são armazenadas. | &quot;previsão&quot; | Qualquer string |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressão [!DNL Generalized Linear] {#generalized-linear-regression}

Ao contrário da regressão linear, que assume que o resultado segue uma distribuição normal (Gaussiana), Modelos [!DNL Generalized Linear] (GLMs) permitem que o resultado siga diferentes tipos de distribuições, como [!DNL Poisson] ou binomial, dependendo da natureza dos dados.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho da regressão [!DNL Generalized Linear].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Define o número máximo de iterações (aplicável ao usar o solucionador `irls`). | 25 | (>= 0) |
| `REG_PARAM` | O parâmetro de regularização. | NÃO DEFINIDO | (>= 0) |
| `TOL` | A tolerância à convergência. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | A profundidade sugerida para `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | O parâmetro family, que descreve a distribuição de erros usada no modelo. As opções com suporte são `gaussian`, `binomial`, `poisson`, `gamma` e `tweedie`. | &quot;gaussiano&quot; | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | Se um termo de interceptação deve ser ajustado. | `true` | `true`, `false` |
| `LINK` | A função de ligação, que define a relação entre o preditor linear e a média da função de distribuição. As opções com suporte são `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog` e `sqrt`. | NÃO DEFINIDO | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | Este parâmetro especifica o índice na função do link de energia. O parâmetro é aplicável somente à família [!DNL Tweedie]. Se não estiver definido, o padrão será `1 - variancePower`, que se alinha ao pacote R `statmod`. Potências de link específicas de 0, 1, -1 e 0,5 correspondem aos links Log, Identity, Inverse e Sqrt, respectivamente. | 1 | Qualquer valor numérico |
| `SOLVER` | O algoritmo de resolução usado para otimização. Opção com suporte: `irls` (reponderação iterativa de quadrados mínimos). | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | Este parâmetro especifica a potência na função de variação da distribuição [!DNL Tweedie], definindo a relação entre variação e média. Os valores com suporte são 0 e `[1, inf)`. Potências de variação de 0, 1 e 2 correspondem às famílias Gaussiana, Poisson e Gamma, respectivamente. | 0,0 | `[1, inf)` |
| `LINK_PREDICTION_COL` | O nome da coluna de previsão do link (preditor linear). | NÃO DEFINIDO | Qualquer string |
| `OFFSET_COL` | O nome da coluna de deslocamento. Se não for definido, todos os deslocamentos de instância serão tratados como 0,0. O recurso offset tem um coeficiente constante de 1,0. | NÃO DEFINIDO | Qualquer string |
| `WEIGHT_COL` | O nome da coluna de peso. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. Na família Binomial, os pesos correspondem ao número de ensaios, e os pesos não inteiros são arredondados no cálculo de AIC. | NÃO DEFINIDO | Qualquer string |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressão [!DNL Gradient Boosted Tree] {#gradient-boosted-tree-regression}

As árvores com aumento de gradiente (GBTs) são um método eficaz de classificação e regressão que combina as previsões de várias árvores de decisão para melhorar a precisão preditiva e o desempenho do modelo.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho da regressão [!DNL Gradient Boosted Tree].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | O número máximo de compartimentos usados para dividir recursos contínuos em intervalos discretos, o que ajuda a determinar como os recursos são divididos em cada nó da árvore de decisão. Mais compartimentos fornecem maior granularidade. | 32 | Deve ser pelo menos 2 e igual ou superior ao número de categorias em qualquer recurso categórico. |
| `CACHE_NODE_IDS` | Se `false`, o algoritmo transmite árvores para executores para corresponder instâncias com nós. Se `true`, o algoritmo armazena em cache IDs de nó para cada instância. O armazenamento em cache pode acelerar o treinamento de árvores mais profundas. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica a frequência de ponto de verificação das IDs de nó em cache. Por exemplo, `10` significa que o cache é marcado a cada 10 iterações. | 10 | (>= 1) |
| `MAX_DEPTH` | A profundidade máxima da árvore (não negativa). Por exemplo, profundidade `0` significa 1 nó folha, e profundidade `1` significa 1 nó interno com 2 nós folha. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | O ganho mínimo de informações necessário para que uma divisão seja considerada em um nó de árvore. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | A fração mínima da contagem de amostra ponderada que cada filho deve ter após uma divisão. Se uma divisão fizer com que a fração do peso total em qualquer filho seja menor que esse valor, ela será descartada. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | O número mínimo de instâncias que cada filho deve ter após uma divisão. Se uma divisão resultar em menos instâncias do que esse valor, a divisão será descartada. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | A memória máxima, em MB, alocada para a agregação do histograma. Se esse valor for muito pequeno, apenas 1 nó será dividido por iteração e suas agregações poderão exceder esse tamanho. | 256 | Qualquer valor inteiro positivo |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `VALIDATION_INDICATOR_COL` | O nome da coluna que indica se cada linha é usada para treinamento ou validação. `false` para treinamento e `true` para validação. | NÃO DEFINIDO | Qualquer string |
| `LEAF_COL` | O nome da coluna para índices folha. O índice de folha previsto de cada instância em cada árvore, gerado pelo percurso de pré-ordem. | &quot;&quot; | Qualquer string |
| `FEATURE_SUBSET_STRATEGY` | Esse parâmetro especifica o número de recursos a serem considerados nas divisões em cada nó de árvore. | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2` ou uma fração entre 0 e 1,0 |
| `SEED` | A semente aleatória. | NÃO DEFINIDO | Qualquer número de 64 bits |
| `WEIGHT_COL` | O nome da coluna, por exemplo, pesos. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer string |
| `LOSS_TYPE` | Este parâmetro especifica a função de perda que o modelo [!DNL Gradient Boosted Tree] minimiza. | &quot;ao quadrado&quot; | `squared` (L2) e `absolute` (L1). Observação: os valores não diferenciam maiúsculas de minúsculas. |
| `STEP_SIZE` | O tamanho da etapa (também conhecido como taxa de aprendizado) no intervalo `(0, 1]`, usado para reduzir a contribuição de cada estimador. | 0,1 | `(0, 1]` |
| `MAX_ITER` | O número máximo de iterações para o algoritmo. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | A fração de dados de treinamento usada para aprender cada árvore de decisão, no intervalo `(0, 1]`. | 1,0 | `(0, 1]` |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressão [!DNL Isotonic] {#isotonic-regression}

[!DNL Isotonic Regression] é um algoritmo usado para ajustar interativamente distâncias, preservando a ordem relativa de diferenças nos dados.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho do [!DNL Isotonic Regression].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Especifica se a sequência de saída deve ser isotônica (aumentando) quando `true` ou antitônica (diminuindo) quando `false`. | `true` | `true`, `false` |
| `WEIGHT_COL` | O nome da coluna, por exemplo, pesos. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer string |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `FEATURE_INDEX` | O índice do recurso, aplicável quando `featuresCol` é uma coluna de vetor. Se não for definido, o valor padrão será `0`. Caso contrário, não tem efeito. | 0 | Qualquer inteiro não negativo |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressão [!DNL Linear] {#linear-regression}

[!DNL Linear Regression] é um algoritmo supervisionado de aprendizado de máquina que se ajusta a uma equação linear para dados, a fim de modelar a relação entre uma variável dependente e recursos independentes.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho do [!DNL Linear Regression].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | O número máximo de iterações. | 100 | (>= 0) |
| `REGPARAM` | O parâmetro de regularização usado para controlar a complexidade do modelo. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | O parâmetro de mistura ElasticNet, que controla o equilíbrio entre as penalidades L1 (Laço) e L2 (Ridge). Um valor de 0 aplica uma penalidade L2, enquanto um valor de 1 aplica uma penalidade L1. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] é um algoritmo de conjunto que cria várias árvores de decisão durante o treinamento e retorna a previsão média dessas árvores para tarefas de regressão, ajudando a evitar a sobreposição.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho do [!DNL Random Forest Regression].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | O número máximo de compartimentos usados para diferenciar recursos contínuos e determinar como os recursos são divididos em cada nó. Mais compartimentos fornecem maior granularidade. | 32 | Deve ser pelo menos 2 e pelo menos igual ao número de categorias em qualquer recurso categórico. |
| `CACHE_NODE_IDS` | Se `false`, o algoritmo transmite árvores para executores para corresponder instâncias com nós. Se `true`, o algoritmo armazenará em cache IDs de nó para cada instância, acelerando o treinamento de árvores mais profundas. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica a frequência de ponto de verificação das IDs de nó em cache. Por exemplo, `10` significa que o cache é marcado a cada 10 iterações. | 10 | (>= 1) |
| `IMPURITY` | O critério usado para o cálculo do ganho de informações (não diferencia maiúsculas de minúsculas). | &quot;entropia&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | A profundidade máxima da árvore (não negativa). Por exemplo, profundidade `0` significa 1 nó folha, e profundidade `1` significa 1 nó interno e 2 nós folha. | 5 | Qualquer inteiro não negativo |
| `MIN_INFO_GAIN` | O ganho mínimo de informações necessário para que uma divisão seja considerada em um nó de árvore. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | A fração mínima da contagem de amostra ponderada que cada filho deve ter após uma divisão. Se uma divisão fizer com que a fração do peso total em qualquer filho seja menor que esse valor, ela será descartada. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | O número mínimo de instâncias que cada filho deve ter após uma divisão. Se uma divisão resultar em menos instâncias do que esse valor, a divisão será descartada. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | A memória máxima, em MB, alocada para a agregação do histograma. Se esse valor for muito pequeno, apenas 1 nó será dividido por iteração e suas agregações poderão exceder esse tamanho. | 256 | (>= 1) |
| `BOOTSTRAP` | Usar amostras de inicialização ao construir árvores. | TRUE | `true`, `false` |
| `NUM_TREES` | O número de árvores para treinar (pelo menos 1). Se `1`, nenhum bootstrapping será usado. Se maior que `1`, o bootstrapping será aplicado. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | A fração de dados de treinamento usada para treinar cada árvore de decisão, no intervalo `(0, 1]`. | 1,0 | (>= 0,0, &lt;= 1) |
| `LEAF_COL` | O nome da coluna para índices folha, que é o índice de folha previsto de cada instância em cada árvore, gerado pelo percurso de pré-ordem. | &quot;&quot; | Qualquer string |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `SEED` | A semente aleatória. | NÃO DEFINIDO | Qualquer número de 64 bits |
| `WEIGHT_COL` | O nome da coluna, por exemplo, pesos. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer nome de coluna válido ou deixe vazio. |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] é usado para ajustar um modelo de regressão de sobrevivência paramétrica, conhecido como o modelo [!DNL Accelerated Failure Time] (AFT), baseado em [!DNL Weibull distribution]. Ele pode empilhar instâncias em blocos para melhorar o desempenho.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho do [!DNL Survival Regression].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | O número máximo de iterações que o algoritmo deve executar. | 100 | (>= 0) |
| `TOL` | A tolerância à convergência. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | A profundidade sugerida para `treeAggregate`. Se as dimensões do recurso ou o número de partições forem grandes, esse parâmetro poderá ser definido como um valor maior. | 2 | (>= 2) |
| `FIT_INTERCEPT` | Se um termo de interceptação deve ser ajustado. | TRUE | `true`, `false` |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `CENSOR_COL` | O nome da coluna para censura. Um valor de `1` indica que o evento ocorreu (sem censura), enquanto `0` significa que o evento foi censurado. | &quot;censor&quot; | 0, 1 |
| `MAX_BLOCK_SIZE_IN_MB` | A memória máxima em MB para empilhar dados de entrada em blocos. Se o tamanho dos dados restantes em uma partição for menor, esse valor será ajustado de acordo. Um valor de `0` permite o ajuste automático. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Próximas etapas

Depois de ler este documento, agora você sabe como configurar e usar vários algoritmos de regressão. Em seguida, consulte os documentos em [classificação](./classification.md) e [clustering](./clustering.md) para saber mais sobre outros tipos de modelos estatísticos avançados.
