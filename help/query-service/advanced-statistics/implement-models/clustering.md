---
title: Algoritmos de Cluster
description: Saiba como configurar e otimizar vários algoritmos de clustering com parâmetros-chave, descrições e código de exemplo para ajudar a implementar modelos estatísticos avançados.
role: Developer
exl-id: 273853c6-85d2-43e5-b51a-aa9d20b313ae
source-git-commit: 69c08f688d355e689e78426dd4b0ed1f4934965c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 4%

---

# Algoritmos de cluster {#clustering-algorithms}

Os algoritmos de cluster agrupam pontos de dados em clusters distintos com base em suas semelhanças, permitindo o aprendizado não supervisionado para descobrir padrões nos dados. Para criar um algoritmo de clustering, use o parâmetro `type` na cláusula `OPTIONS` para especificar o algoritmo que deseja usar para treinamento de modelo. Em seguida, defina os parâmetros relevantes como pares de valores-chave para ajustar o modelo.

>[!NOTE]
>
>Compreenda os requisitos de parâmetro para o algoritmo escolhido. Se você optar por não personalizar determinados parâmetros, o sistema aplicará as configurações padrão. Consulte a documentação relevante para entender a função de cada parâmetro e os valores padrão.

## [!DNL K-Means] {#kmeans}

`K-Means` é um algoritmo de clustering que particiona dados em um número predefinido de clusters (k). É um dos algoritmos mais usados para clustering devido à sua simplicidade e eficiência.

**Parâmetros**

Ao usar `K-Means`, os seguintes parâmetros podem ser definidos na cláusula `OPTIONS`:

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITER` | O número de iterações que o algoritmo deve executar. | `20` | (>= 0) |
| `TOL` | O nível de tolerância de convergência. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | O número de clusters a serem criados (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | O algoritmo usado para calcular a distância entre dois pontos. O valor diferencia maiúsculas e minúsculas. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | O algoritmo de inicialização para os centros de cluster. | `k-means\|\|` | `random`, `k-means\|\|` (Uma versão paralela de k-means++) |
| `INIT_STEPS` | O número de etapas para o modo de inicialização `k-means\|\|` (aplicável somente quando `KMEANS_INIT_METHOD` é `k-means\|\|`). | `2` | (>0) |
| `PREDICTION_COL` | O nome da coluna onde as previsões serão armazenadas. | `prediction` | Qualquer string |
| `SEED` | Uma semente aleatória para reprodutibilidade. | `-1689246527` | Qualquer número de 64 bits |
| `WEIGHT_COL` | O nome da coluna usada para pesos de instância. Se não estiver definido, todas as instâncias serão ponderadas igualmente. | `not set` | N/D |

{style="table-layout:auto"}

**Exemplo**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means] é um algoritmo de cluster hierárquico que usa uma abordagem divisiva (ou &quot;de cima para baixo&quot;). Todas as observações começam em um único cluster e as divisões são executadas de forma recursiva à medida que a hierarquia é criada. [!DNL Bisecting K-means] pode ser mais rápido que K-means normal, mas geralmente produz resultados de cluster diferentes.

**Parâmetros**

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | O número máximo de iterações que o algoritmo executa. | 20 | (>= 0) |
| `WEIGHT_COL` | O nome da coluna para pesos de instância. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer string |
| `NUM_CLUSTERS` | O número desejado de clusters folha. O número real pode ser menor se nenhum cluster divisível permanecer. | 4 | (> 1) |
| `SEED` | A semente aleatória usada para controlar processos aleatórios no algoritmo. | NÃO DEFINIDO | Qualquer número de 64 bits |
| `DISTANCE_MEASURE` | A medida de distância usada para calcular a similaridade entre pontos. | &quot;euclidiano&quot; | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | O número mínimo de pontos (se >= 1,0) ou a proporção mínima de pontos (se &lt; 1,0) necessários para que um cluster seja divisível. | 1,0 | (>= 0) |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |

{style="table-layout:auto"}

**Exemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] representa uma distribuição composta onde os pontos de dados são retirados de uma de k sub-distribuições Gaussianas, cada uma com sua própria probabilidade. Ele é usado para modelar conjuntos de dados que são assumidos como sendo gerados a partir de uma mistura de várias distribuições Gaussianas.

**Parâmetros**

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | O número máximo de iterações para o algoritmo a ser executado. | 100 | (>= 0) |
| `WEIGHT_COL` | O nome da coluna, por exemplo, pesos. Se não estiver definido ou vazio, todos os pesos de instância serão tratados como `1.0`. | NÃO DEFINIDO | Qualquer nome de coluna válido ou em branco |
| `NUM_CLUSTERS` | O número de distribuições Gaussianas independentes no modelo de mistura. | 2 | (> 1) |
| `SEED` | A semente aleatória usada para controlar processos aleatórios no algoritmo. | NÃO DEFINIDO | Qualquer número de 64 bits |
| `AGGREGATION_DEPTH` | Esse parâmetro controla a profundidade das árvores de agregação usadas durante o cálculo. | 2 | (>= 1) |
| `PROBABILITY_COL` | O nome da coluna para probabilidades condicionais de classe previstas. Elas devem ser tratadas como pontuações de confiança em vez de probabilidades exatas. | &quot;probabilidade&quot; | Qualquer string |
| `TOL` | A tolerância de convergência para algoritmos iterativos. | 0,01 | (>= 0) |
| `PREDICTION_COL` | O nome da coluna para saída de previsão. | &quot;previsão&quot; | Qualquer string |

{style="table-layout:auto"}

**Exemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) é um modelo probabilístico que captura a estrutura de tópicos subjacente de uma coleção de documentos. É um modelo bayesiano hierárquico de três níveis com camadas de palavras, tópicos e documentos. O LDA usa essas camadas, juntamente com os documentos observados, para criar uma estrutura de tópico latente.

**Parâmetros**

| Parâmetro | Descrição | Valor padrão | Valores possíveis |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | O número máximo de iterações que o algoritmo executa. | 20 | (>= 0) |
| `OPTIMIZER` | O otimizador ou algoritmo de inferência usado para estimar o modelo LDA. As opções com suporte são `"online"` (Baias de Variação Online) e `"em"` (Expectativa-Maximização). | &quot;online&quot; | `online`, `em` (não diferencia maiúsculas de minúsculas) |
| `NUM_CLUSTERS` | O número de clusters a serem criados (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Especifica a frequência de ponto de verificação das IDs de nó em cache. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | O parâmetro de concentração (&quot;alfa&quot;) determina as suposições anteriores sobre a distribuição de tópicos entre documentos. O comportamento padrão é determinado pelo otimizador. Para o otimizador `EM`, os valores alfa devem ser maiores que 1,0 (padrão: distribuídos uniformemente como (50/k) + 1), garantindo distribuições de tópicos simétricas. Para o otimizador `online`, os valores alfa podem ser 0 ou maiores (padrão: distribuídos uniformemente como 1,0/k), permitindo uma inicialização de tópico mais flexível. | Automático | Qualquer valor único ou vetor de comprimento k em que valores > 1 para EM |
| `KEEP_LAST_CHECKPOINT` | Indica se o último ponto de verificação deve ser mantido ao usar o otimizador `em`. A exclusão do ponto de verificação pode causar falhas se uma partição de dados for perdida. Os pontos de verificação são removidos automaticamente do armazenamento quando não são mais necessários, conforme determinado pela contagem de referências. | `true` | `true`, `false` |
| `LEARNING_DECAY` | Taxa de aprendizado do otimizador `online`, definida como uma taxa de declínio exponencial entre `(0.5, 1.0]`. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | Um parâmetro de aprendizado para o otimizador `online` que reduz as iterações iniciais para diminuir a contagem de iterações iniciais. | 1024 | (> 0) |
| `SEED` | Semente aleatória para controlar processos aleatórios no algoritmo. | NÃO DEFINIDO | Qualquer número de 64 bits |
| `OPTIMIZE_DOC_CONCENTRATION` | Para o otimizador `online`: se o `docConcentration` (parâmetro Dirichlet para distribuição de tópico de documento) deve ser otimizado durante o treinamento. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | Para o otimizador `online`: a fração do corpo amostrada e usada em cada iteração de descida de gradiente de minilote, no intervalo `(0, 1]`. | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | O parâmetro de concentração (&quot;beta&quot; ou &quot;eta&quot;) define as suposições anteriores colocadas nas distribuições dos tópicos em termos. O valor padrão é determinado pelo otimizador: Para `EM`, valores > 1,0 (padrão = 0,1 + 1). Para `online`, valores ≥ 0 (padrão = 1,0/k). | Automático | Qualquer valor único ou vetor de comprimento k, em que valores > 1 para EM |
| `TOPIC_DISTRIBUTION_COL` | Esse parâmetro gera a distribuição estimada da mistura de tópicos para cada documento, geralmente chamada de &quot;teta&quot; na literatura. Para documentos vazios, retorna um vetor de zeros. As estimativas são derivadas usando uma aproximação variacional (&quot;gama&quot;). | NÃO DEFINIDO | Qualquer string |

{style="table-layout:auto"}

**Exemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Próximas etapas

Depois de ler este documento, agora você sabe como configurar e usar vários algoritmos de cluster. Em seguida, consulte os documentos sobre [classificação](./classification.md) e [regressão](./regression.md) para saber mais sobre outros tipos de modelos estatísticos avançados.
