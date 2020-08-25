---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: Otimizar um modelo
topic: Tutorial
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---


# Otimizar um modelo usando a estrutura do Model Insights

A Framework Model Insights fornece ao cientista de dados ferramentas [!DNL Data Science Workspace] para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado da máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem decisões de otimização de modelos melhores para seus clientes finais.

## O que são métricas?

Depois de implementar e treinar um modelo, o próximo passo que um cientista da área de dados faria seria descobrir o desempenho do modelo. Várias métricas são usadas para descobrir a eficácia de um modelo em relação a outras. Alguns exemplos de métricas usadas incluem:
- Precisão da classificação
- Área sob curva
- Matriz de confusão
- Relatório de classificação

## Configuração do código de fórmula

Atualmente, o Model Insights Framework suporta os seguintes tempos de execução:
- [Scala](#scala)
- [!DNL Python/Tensorflow](#pythontensorflow)
- [R](#r)

O código de amostra para fórmulas pode ser encontrado no repositório [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) em `recipes`. Arquivos específicos deste repositório serão referenciados neste tutorial.

### Scala {#scala}

Há duas maneiras de trazer métricas para as receitas. Uma é usar as métricas de avaliação padrão fornecidas pelo SDK e a outra é gravar métricas de avaliação personalizadas.

#### Métricas de avaliação padrão para Scala

As avaliações padrão são calculadas como parte dos algoritmos de classificação. Estes são alguns valores padrão para avaliadores que estão implementados no momento:

| Classe do avaliador | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

O avaliador pode ser definido na fórmula no arquivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) na `recipe` pasta. O código de amostra que permite o `DefaultBinaryClassificationEvaluator` é mostrado abaixo:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Depois que uma classe avaliadora é ativada, várias métricas serão calculadas durante o treinamento por padrão. As métricas padrão podem ser declaradas explicitamente adicionando a seguinte linha à sua `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Se a métrica não estiver definida, as métricas padrão estarão ativas.

Uma métrica específica pode ser ativada alterando o valor para `evaluation.metrics.com`. No exemplo a seguir, a métrica da Pontuação F está ativada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

A tabela a seguir indica as métricas padrão para cada classe. Um usuário também pode usar os valores na `evaluation.metric` coluna para ativar uma métrica específica.

| `evaluator.class` | Métricas padrão | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | - Precisão <br>- Matriz de <br>Confusão de Recall <br>-F-Pontuação <br>-Precisão <br>- Características Operacionais <br>Do Receptor Na Área Operacional Do Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | - Precisão <br>- Matriz de <br>Confusão de Recall <br>-F-Pontuação <br>-Precisão <br>- Características Operacionais <br>Do Receptor Na Área Operacional Do Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisão média (MAP) <br>- Média de precisão (MAP) normalizada Descontada Ganho acumulado <br>- Média de classificação <br>métrica Recírica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de avaliação personalizadas para Scala

O avaliador personalizado pode ser fornecido estendendo a interface do `MLEvaluator.scala` em seu `Evaluator.scala` arquivo. No arquivo [Evaluator.escala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) de exemplo, definimos funções personalizadas `split()` e `evaluate()` . Nossa `split()` função divide nossos dados aleatoriamente com uma proporção de 8:2 e nossa `evaluate()` função define e retorna 3 métricas: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Para a `MLMetric` classe, não use `"measures"` para `valueType` ao criar uma nova `MLMetric` outra métrica, a métrica não será preenchida na tabela de métricas de avaliação personalizadas.
>  
> Faça o seguinte: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Não é isso: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Uma vez definido na fórmula, a próxima etapa é ativá-la nas receitas. Isso é feito no arquivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) na `resources` pasta do projeto. Aqui, a classe `evaluation.class` é definida para a `Evaluator` classe definida em `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

No [!DNL Data Science Workspace], o usuário poderá ver os insights na guia &quot;Métricas de avaliação&quot; na página de experimentos.

### [!DNL Python/Tensorflow] {#pythontensorflow}

A partir de agora, não há métricas de avaliação padrão para [!DNL Python] ou [!DNL Tensorflow]. Assim, para obter as métricas de avaliação para [!DNL Python] ou [!DNL Tensorflow], será necessário criar uma métrica de avaliação personalizada. Isso pode ser feito com a implementação da `Evaluator` classe.

#### Métricas de avaliação personalizadas para [!DNL Python]

Para métricas de avaliação personalizadas, há dois métodos principais que precisam ser implementados para o avaliador: `split()` e `evaluate()`.

Para [!DNL Python], esses métodos seriam definidos em [evaluate.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para a `Evaluator` classe. Siga o link [evaluate.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para obter um exemplo do `Evaluator`.

A criação de métricas de avaliação no [!DNL Python] exige que o usuário implemente os `evaluate()` métodos e `split()` métodos.

O `evaluate()` método retorna o objeto de métrica que contém uma matriz de objetos de métrica com propriedades de `name`, `value`e `valueType`.

O objetivo do `split()` método é inserir dados e produzir um conjunto de dados de treinamento e teste. Em nosso exemplo, o `split()` método insere dados usando o `DataSetReader` SDK e limpa os dados removendo colunas não relacionadas. Daí, recursos adicionais são criados a partir de recursos brutos existentes nos dados.

O `split()` método deve retomar os dados de formação e de ensaio que são depois utilizados pelos `pipeline()` métodos de treino e ensaio do modelo ML.

#### Métricas de avaliação personalizadas para Tensorflow

Para [!DNL Tensorflow]que, semelhante a [!DNL Python], os métodos `evaluate()` e `split()` na `Evaluator` classe precisem ser implementados. No caso `evaluate()`, as métricas devem ser retornadas enquanto `split()` retorna o comboio e os conjuntos de dados de ensaio.

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

A partir de agora, não há métricas de avaliação padrão para R. Assim, para obter as métricas de avaliação para R, será necessário definir a `applicationEvaluator` classe como parte da fórmula.

#### Métricas de avaliação personalizadas para R

O objetivo principal do `applicationEvaluator` é retornar um objeto JSON contendo pares de valores chave de métricas.

Esse [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) pode ser usado como exemplo. Neste exemplo, o `applicationEvaluator` é dividido em três seções familiares:
- Carregar dados
- Preparação de dados/engenharia de recursos
- Recuperar modelo salvo e avaliar

Os dados são carregados pela primeira vez em um conjunto de dados a partir de uma fonte, conforme definido em [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir daí, os dados são limpos e projetados para se encaixarem no modelo de aprendizado da máquina. Por fim, o modelo é usado para fazer uma previsão usando nosso conjunto de dados e a partir dos valores previstos e valores reais, as métricas são calculadas. Nesse caso, MAPE, MAE e RMSE são definidos e retornados no `metrics` objeto.

## Uso de métricas pré-criadas e gráficos de visualização

O [!DNL Sensei Model Insights Framework] oferecerá suporte a um modelo padrão para cada tipo de algoritmo de aprendizado de máquina. A tabela abaixo mostra classes comuns de algoritmos de aprendizado de máquina de alto nível e métricas de avaliação e visualizações correspondentes.

| Tipo de Algoritmo ML | Métricas de avaliação | Visualizações |
--- | --- | ---
| Regressão | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Curva de sobreposição de valores previstos vs reais |
| Classificação binária | - Matriz<br>de perfusão - Precisão<br>- Precisão<br>- pontuação F (especificamente F1,F2)<br>- AUC<br>- ROC | Matriz de curva e confusão de ROC |
| Classificação multiclasse | - Matriz <br>- Para cada classe: <br>- precisão de evocação <br>- pontuação F (especificamente F1, F2) | Matriz de curva e confusão de ROC |
| Agrupamento (sem verdade básica) | - NMI (pontuação normalizada de informação mútua), AMI (pontuação de informação mútua ajustada)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- pontuação de homogeneidade, pontuação de integralidade e V-measurement<br>- FMI (índice Fowlkes-Mallows)<br>- Pureza<br>- Índice Jaccard | Gráfico de clusters mostrando clusters e centróides com tamanhos de cluster relativos refletindo os pontos de dados dentro do cluster |
| Agrupamento (sem verdade básica) | - Inércia<br>- Coeficiente<br>de silhueta- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice Dunn | Gráfico de clusters mostrando clusters e centróides com tamanhos de cluster relativos refletindo os pontos de dados dentro do cluster |
| Recomendação | -Precisão média (MAP) <br>- Média de precisão (MAP) normalizada Descontada Ganho acumulado <br>- Média de classificação <br>métrica Recírica K | TBD |
| Casos de uso do TensorFlow | Análise do modelo TensorFlow (TFMA) | Comparação profunda entre o modelo de rede neural e a visualização |
| Outro mecanismo de captura de erros | Lógica métrica personalizada (e gráficos de avaliação correspondentes) definida pelo autor do modelo. Tratamento de erros graciosos em caso de incompatibilidade do modelo | Tabela com pares de valores chave para métricas de avaliação |
