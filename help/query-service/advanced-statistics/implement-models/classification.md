---
title: Algoritmos de classificação
description: Saiba como configurar e otimizar vários algoritmos de classificação com parâmetros importantes, descrições e código de exemplo para ajudar a implementar modelos estatísticos avançados.
role: Developer
exl-id: 9105ab04-b480-48a0-b8f7-cf0ed5e5399d
source-git-commit: 489063fcd003e20f233a9c9d85d8cb6c22708d88
workflow-type: tm+mt
source-wordcount: '2449'
ht-degree: 4%

---

# Algoritmos de classificação {#classification-algorithms}

Este documento fornece uma visão geral de vários algoritmos de classificação, com foco em sua configuração, parâmetros principais e uso prático em modelos estatísticos avançados. Os algoritmos de classificação são usados para atribuir categorias a pontos de dados com base em recursos de entrada. Cada seção inclui descrições de parâmetros e código de exemplo para ajudar você a implementar e otimizar esses algoritmos para tarefas como árvores de decisão, random forest e classificação ingênua de Bayes.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] é uma abordagem de aprendizado supervisionada usada em estatísticas, mineração de dados e aprendizado de máquina. Nessa abordagem, uma árvore decisória é usada como modelo preditivo para tarefas de classificação, tirando conclusões de um conjunto de observações.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho de um [!DNL Decision Tree Classifier].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | O número máximo de compartimentos determina como os recursos contínuos são divididos em intervalos discretos. Isso afeta como os recursos são divididos em cada nó da árvore de decisão. Mais compartimentos fornecem maior granularidade. | 32 | Deve ser pelo menos 2 e pelo menos igual ao número de categorias em qualquer recurso categórico. |
| `CACHE_NODE_IDS` | Se `false`, o algoritmo transmite árvores para executores para corresponder instâncias com nós. Se `true`, o algoritmo armazenará em cache IDs de nó para cada instância, acelerando o treinamento de árvores mais profundas. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica a frequência de ponto de verificação das IDs de nó em cache. Por exemplo, `10` significa que o cache é marcado a cada 10 iterações. | 10 | (>= 1) |
| `IMPURITY` | O critério usado para o cálculo do ganho de informações (não diferencia maiúsculas de minúsculas). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | A profundidade máxima da árvore (não negativa). Por exemplo, profundidade `0` significa 1 nó folha, e profundidade `1` significa 1 nó interno e 2 nós folha. | 5 | (>= 0) (intervalo: [0,30]) |
| `MIN_INFO_GAIN` | O ganho mínimo de informações necessário para que uma divisão seja considerada em um nó de árvore. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | A fração mínima da contagem de amostra ponderada que cada filho deve ter após uma divisão. Se uma divisão fizer com que a fração do peso total em qualquer filho seja menor que esse valor, ela será descartada. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | O número mínimo de instâncias que cada filho deve ter após uma divisão. Se uma divisão resultar em menos instâncias do que esse valor, a divisão será descartada. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | A memória máxima, em MB, alocada para a agregação do histograma. Se esse valor for muito pequeno, apenas 1 nó será dividido por iteração e suas agregações poderão exceder esse tamanho. | 256 | (>= 0) |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `SEED` | A semente aleatória. | N/D | Qualquer número de 64 bits |
| `WEIGHT_COL` | O nome da coluna, por exemplo, pesos. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer string |
| `ONE_VS_REST` | Ativa ou desativa o encapsulamento deste algoritmo com One-vs-Rest, usado para problemas de classificação de várias classes. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

O [!DNL Factorization Machine Classifier] é um algoritmo de classificação que suporta descida de gradiente normal e a resolução AdamW. O modelo de classificação de máquina de fatoração usa perda logística, que pode ser otimizada via descida de gradiente e, muitas vezes, inclui termos de regularização como L2 para evitar sobreajuste.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho do [!DNL Factorization Machine Classifier].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | A tolerância de convergência, que controla a precisão da otimização. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | A dimensionalidade dos fatores. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Especifica se um termo de interceptação deve ser ajustado. | `true` | `true`, `false` |
| `FIT_LINEAR` | Especifica se o termo linear deve ser ajustado (também conhecido como termo unidirecional). | `true` | `true`, `false` |
| `INIT_STD` | O desvio padrão para coeficientes de inicialização. | 0,01 | (>= 0) |
| `MAX_ITER` | O número máximo de iterações para o algoritmo a ser executado. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | A fração de dados a ser usada em minilotes durante o treinamento. Deve estar no intervalo `(0, 1]`. | 1,0 | 0 &lt; valor &lt;= 1 |
| `REG_PARAM` | O parâmetro de regularização, que ajuda a controlar a complexidade do modelo e evitar a adaptação excessiva. | 0,0 | (>= 0) |
| `SEED` | A semente aleatória para controlar processos aleatórios no algoritmo. | N/D | Qualquer número de 64 bits |
| `SOLVER` | O algoritmo de resolução usado para otimização. As opções com suporte são `gd` (descida de gradiente) e `adamW`. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | O tamanho inicial da etapa para otimização, geralmente interpretado como a taxa de aprendizado. | 1,0 | > 0 |
| `PROBABILITY_COL` | O nome da coluna para probabilidades condicionais de classe previstas. Nota: nem todos os modelos produzem probabilidades bem calibradas; estas devem ser tratadas como pontuações de confiança em vez de probabilidades exatas. | &quot;probabilidade&quot; | Qualquer string |
| `PREDICTION_COL` | O nome da coluna para rótulos de classe previstos. | &quot;previsão&quot; | Qualquer string |
| `RAW_PREDICTION_COL` | O nome da coluna para valores de previsão brutos (também conhecido como confiança). | &quot;rawPrediction&quot; | Qualquer string |
| `ONE_VS_REST` | Especifica se é necessário habilitar One-vs-Rest para classificação multiclass. | FALSO | `true`, `false` |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

O [!DNL Gradient Boosted Tree Classifier] usa um conjunto de árvores de decisão para melhorar a precisão das tarefas de classificação, combinando várias árvores para melhorar o desempenho do modelo.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho do [!DNL Gradient Boosted Tree Classifier].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | O número máximo de compartimentos determina como os recursos contínuos são divididos em intervalos discretos. Isso afeta como os recursos são divididos em cada nó da árvore de decisão. Mais compartimentos fornecem maior granularidade. | 32 | Deve ser pelo menos 2 e igual ou superior ao número de categorias em qualquer recurso categórico. |
| `CACHE_NODE_IDS` | Se `false`, o algoritmo transmite árvores para executores para corresponder instâncias com nós. Se `true`, o algoritmo armazenará em cache IDs de nó para cada instância, acelerando o treinamento de árvores mais profundas. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica a frequência de ponto de verificação das IDs de nó em cache. Por exemplo, `10` significa que o cache é marcado a cada 10 iterações. | 10 | (>= 1) |
| `MAX_DEPTH` | A profundidade máxima da árvore (não negativa). Por exemplo, profundidade `0` significa 1 nó folha, e profundidade `1` significa 1 nó interno e 2 nós folha. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | O ganho mínimo de informações necessário para que uma divisão seja considerada em um nó de árvore. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | A fração mínima da contagem de amostra ponderada que cada filho deve ter após uma divisão. Se uma divisão fizer com que a fração do peso total em qualquer filho seja menor que esse valor, ela será descartada. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | O número mínimo de instâncias que cada filho deve ter após uma divisão. Se uma divisão resultar em menos instâncias do que esse valor, a divisão será descartada. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | A memória máxima, em MB, alocada para a agregação do histograma. Se esse valor for muito pequeno, apenas 1 nó será dividido por iteração e suas agregações poderão exceder esse tamanho. | 256 | (>= 0) |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `VALIDATION_INDICATOR_COL` | O nome da coluna indica se cada linha é usada para treinamento ou validação. Um valor de `false` indica treinamento e `true` indica validação. Se um valor não for definido, o valor padrão será `None`. | &quot;Nenhum&quot; | Qualquer string |
| `RAW_PREDICTION_COL` | O nome da coluna para valores de previsão brutos (também conhecido como confiança). | &quot;rawPrediction&quot; | Qualquer string |
| `LEAF_COL` | O nome da coluna para índices folha, que é o índice de folha previsto de cada instância em cada árvore, gerado pelo percurso de pré-ordem. | &quot;&quot; | Qualquer string |
| `FEATURE_SUBSET_STRATEGY` | O número de recursos considerados para divisão em cada nó de árvore. Opções com suporte: `auto` (determinado automaticamente com base na tarefa), `all` (usar todos os recursos), `onethird` (usar um terço dos recursos), `sqrt` (usar a raiz quadrada do número de recursos), `log2` (usar o logaritmo de base 2 do número de recursos) e `n` (onde n é uma fração dos recursos, se estiver no intervalo `(0, 1]`, ou um número específico de recursos, se estiver no intervalo `[1, total number of features]`). | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` |
| `WEIGHT_COL` | O nome da coluna, por exemplo, pesos. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer string |
| `LOSS_TYPE` | A função de perda que o modelo [!DNL Gradient Boosted Tree] tenta minimizar. | &quot;logística&quot; | `logistic` (não diferencia maiúsculas de minúsculas) |
| `STEP_SIZE` | O tamanho da etapa (também conhecido como taxa de aprendizado) no intervalo `(0, 1]`, usado para reduzir a contribuição de cada estimador. | 0,1 | (>= 0,0, &lt;= 1) |
| `MAX_ITER` | O número máximo de iterações para o algoritmo. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | A fração de dados de treinamento usada para treinar cada árvore decisória. O valor deve estar no intervalo 0 &lt; valor &lt;= 1. | 1,0 | `(0, 1]` |
| `PROBABILITY_COL` | O nome da coluna para probabilidades condicionais de classe previstas. Nota: nem todos os modelos produzem probabilidades bem calibradas; estas devem ser tratadas como pontuações de confiança em vez de probabilidades exatas. | &quot;probabilidade&quot; | Qualquer string |
| `ONE_VS_REST` | Ativa ou desativa o encapsulamento deste algoritmo com One-vs-Rest para classificação multiclass. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (LinearSVC) {#linear-support-vector-classifier}

O [!DNL Linear Support Vector Classifier] (LinearSVC) constrói um hiperplano para classificar dados em um espaço de alta dimensão. Você pode usá-la para maximizar a margem entre as classes para minimizar os erros de classificação.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho do [!DNL Linear Support Vector Classifier (LinearSVC)].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | O número máximo de iterações para o algoritmo a ser executado. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | A profundidade da agregação em árvore. Esse parâmetro é usado para reduzir a sobrecarga de comunicação de rede. | 2 | Qualquer número inteiro positivo |
| `FIT_INTERCEPT` | Se um termo de interceptação deve ser ajustado. | `true` | `true`, `false` |
| `TOL` | Esse parâmetro determina o limite para interromper iterações. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | A memória máxima em MB para empilhar dados de entrada em blocos. Se o parâmetro for definido como `0`, o valor ideal será escolhido automaticamente (geralmente em torno de 1 MB). | 0,0 | (>= 0) |
| `REG_PARAM` | O parâmetro de regularização, que ajuda a controlar a complexidade do modelo e evitar a adaptação excessiva. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Esse parâmetro indica se os recursos de treinamento devem ser padronizados antes da adaptação ao modelo. | `true` | `true`, `false` |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `RAW_PREDICTION_COL` | O nome da coluna para valores de previsão brutos (também conhecido como confiança). | &quot;rawPrediction&quot; | Qualquer string |
| `ONE_VS_REST` | Ativa ou desativa o encapsulamento deste algoritmo com One-vs-Rest para classificação multiclass. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] é um algoritmo supervisionado usado para tarefas de classificação binária. Ele modela a probabilidade de uma instância pertencer a uma classe usando a função logística e atribui a instância à classe com a probabilidade mais alta. Isso o torna adequado para problemas em que o objetivo é separar dados em uma de duas categorias.

**Parâmetros**

A tabela abaixo descreve os principais parâmetros para configurar e otimizar o desempenho do [!DNL Logistic Regression].

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | O número máximo de iterações que o algoritmo executa. | 100 | (>= 0) |
| `REGPARAM` | O parâmetro de regularização é usado para controlar a complexidade do modelo. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | O parâmetro de mixagem `ElasticNet` controla o equilíbrio entre as penalidades L1 (Laço) e L2 (Ridge). Um valor de 0 aplica uma penalidade L2 (Ridge, que reduz o tamanho dos coeficientes), enquanto um valor de 1 aplica uma penalidade L1 (Laço, que incentiva a dispersão definindo alguns coeficientes como zero). | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Exemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

O [!DNL Multilayer Perceptron Classifier] (MLPC) é um classificador de rede neural artificial de feed-forward. Consiste em múltiplas camadas totalmente conectadas de nós, onde cada nó aplica uma combinação linear ponderada de entradas, seguida por uma função de ativação. O MLPC é utilizado para tarefas de classificação complexas que exigem limites de decisão não lineares.

**Parâmetros**

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | O número máximo de iterações para o algoritmo a ser executado. | 100 | (>= 0) |
| `BLOCK_SIZE` | O tamanho do bloco para empilhar dados de entrada em matrizes dentro de partições. Se o tamanho do bloco exceder os dados restantes em uma partição, ele será ajustado de acordo. | 128 | (>= 0) |
| `STEP_SIZE` | O tamanho da etapa usada para cada iteração de otimização (aplicável somente para o resolvedor `gd`). | 0,03 | (> 0) |
| `TOL` | A tolerância de convergência para otimização. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `SEED` | A semente aleatória para controlar processos aleatórios no algoritmo. | NÃO DEFINIDO | Qualquer número de 64 bits |
| `PROBABILITY_COL` | O nome da coluna para probabilidades condicionais de classe previstas. Elas devem ser tratadas como pontuações de confiança em vez de probabilidades exatas. | &quot;probabilidade&quot; | Qualquer string |
| `RAW_PREDICTION_COL` | O nome da coluna para valores de previsão brutos (também conhecido como confiança). | &quot;rawPrediction&quot; | Qualquer string |
| `ONE_VS_REST` | Ativa ou desativa o encapsulamento deste algoritmo com One-vs-Rest para classificação multiclass. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] é um classificador probabilístico, multiclass simples baseado no teorema de Bayes com fortes (ingênuas) suposições de independência entre características. Ele treina com eficiência computando probabilidades condicionais em uma única passagem sobre os dados de treinamento para calcular a distribuição de probabilidade condicional de cada recurso dado cada rótulo. Para previsões, ele usa o teorema de Bayes para calcular a distribuição de probabilidade condicional de cada rótulo dado uma observação.

**Parâmetros**

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Especifica o tipo de modelo. As opções com suporte são `"multinomial"`, `"complement"`, `"bernoulli"` e `"gaussian"`. O tipo de modelo diferencia maiúsculas de minúsculas. | &quot;multinomial&quot; | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | O parâmetro de suavização é usado para lidar com problemas de frequência zero em dados categóricos. | 1,0 | (>= 0) |
| `PROBABILITY_COL` | Este parâmetro especifica o nome da coluna para probabilidades condicionais de classe previstas. Observação: nem todos os modelos fornecem estimativas de probabilidade bem calibradas; trate esses valores como confianças em vez de probabilidades precisas. | &quot;probabilidade&quot; | Qualquer string |
| `WEIGHT_COL` | O nome da coluna para pesos de instância. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer string |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `RAW_PREDICTION_COL` | O nome da coluna para valores de previsão brutos (também conhecido como confiança). | &quot;rawPrediction&quot; | Qualquer string |
| `ONE_VS_REST` | Especifica se é necessário habilitar One-vs-Rest para classificação multiclass. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] é um algoritmo de aprendizado de conjunto que cria várias árvores de decisão durante o treinamento. Atenua a sobreajuste através da média de previsões e da seleção da classe escolhida pela maioria das árvores para tarefas de classificação.

**Parâmetros**

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | O número máximo de compartimentos determina como os recursos contínuos são divididos em intervalos discretos. Isso afeta como os recursos são divididos em cada nó da árvore de decisão. Mais compartimentos fornecem maior granularidade. | 32 | Deve ser pelo menos 2 e igual ou superior ao número de categorias em qualquer recurso categórico. |
| `CACHE_NODE_IDS` | Se `false`, o algoritmo transmite árvores para executores para corresponder instâncias com nós. Se `true`, o algoritmo armazenará em cache IDs de nó para cada instância, acelerando o treinamento. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica a frequência de ponto de verificação das IDs de nó em cache. Por exemplo, `10` significa que o cache é marcado a cada 10 iterações. | 10 | (>= 1) |
| `IMPURITY` | O critério usado para o cálculo do ganho de informações (não diferencia maiúsculas de minúsculas). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | A profundidade máxima da árvore (não negativa). Por exemplo, profundidade `0` significa 1 nó folha, e profundidade `1` significa 1 nó interno e 2 nós folha. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | O ganho mínimo de informações necessário para que uma divisão seja considerada em um nó de árvore. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | A fração mínima da contagem de amostra ponderada que cada filho deve ter após uma divisão. Se uma divisão fizer com que a fração do peso total em qualquer filho seja menor que esse valor, ela será descartada. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | O número mínimo de instâncias que cada filho deve ter após uma divisão. Se uma divisão resultar em menos instâncias do que esse valor, a divisão será descartada. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | A memória máxima, em MB, alocada para a agregação do histograma. Se esse valor for muito pequeno, apenas 1 nó será dividido por iteração e suas agregações poderão exceder esse tamanho. | 256 | (>= 1) |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |
| `WEIGHT_COL` | O nome da coluna, por exemplo, pesos. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer nome de coluna válido ou em branco |
| `SEED` | A semente aleatória usada para controlar processos aleatórios no algoritmo. | -1689246527 | Qualquer número de 64 bits |
| `BOOTSTRAP` | Se amostras de inicialização são usadas ao criar árvores. | `true` | `true`, `false` |
| `NUM_TREES` | O número de árvores a treinar. Se `1`, então nenhum bootstrapping será usado. Se maior que `1`, o bootstrapping será aplicado. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | A fração de dados de treinamento usada para aprender cada árvore decisória. | 1,0 | (> 0, &lt;= 1) |
| `LEAF_COL` | O nome da coluna para os índices folha, que contém o índice folha previsto de cada instância em cada árvore por pré-ordem. | &quot;&quot; | Qualquer string |
| `PROBABILITY_COL` | O nome da coluna para probabilidades condicionais de classe previstas. Elas devem ser tratadas como pontuações de confiança em vez de probabilidades exatas. | NÃO DEFINIDO | Qualquer string |
| `RAW_PREDICTION_COL` | O nome da coluna para valores de previsão brutos (também conhecido como confiança). | &quot;rawPrediction&quot; | Qualquer string |
| `ONE_VS_REST` | Especifica se é necessário habilitar One-vs-Rest para classificação multiclass. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Próximas etapas

Depois de ler este documento, agora você sabe como configurar e usar vários algoritmos de classificação. Em seguida, consulte os documentos sobre [regressão](./regression.md) e [clustering](./clustering.md) para saber mais sobre outros tipos de modelos estatísticos avançados.
