---
keywords: Experience Platform;otimizar;modelo;Data Science Workspace;tópicos populares;insights de modelo
solution: Experience Platform
title: Otimizar um modelo usando a estrutura do Model Insights
type: Tutorial
description: A estrutura do Model Insights fornece ao cientista de dados ferramentas no Data Science Workspace para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Otimizar um modelo usando a estrutura do Model Insights

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

A Estrutura do Model Insights fornece ao cientista de dados ferramentas no [!DNL Data Science Workspace] para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado de máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem melhores decisões de otimização de modelos para seus clientes finais.

## O que são métricas?

Depois de implementar e treinar um modelo, o próximo passo que um cientista de dados faria é descobrir o desempenho do modelo. Várias métricas são usadas para descobrir a eficiência de um modelo em comparação com outras. Alguns exemplos de métricas usadas:

- Precisão da classificação
- Área sob a curva
- Matriz de confusão
- Relatório de classificação

## Configuração do código de fórmula

Atualmente, a Estrutura do Model Insights é compatível com os seguintes tempos de execução:

- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

O código de amostra para receitas pode ser encontrado no repositório [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) em `recipes`. Os arquivos específicos deste repositório serão referenciados neste tutorial.

### Scala {#scala}

Há duas maneiras de inserir métricas nas receitas. Uma é usar as métricas de avaliação padrão fornecidas pelo SDK e a outra é gravar métricas de avaliação personalizadas.

#### Métricas de avaliação padrão para a Scala

As avaliações padrão são calculadas como parte dos algoritmos de classificação. Estes são alguns valores padrão para avaliadores que estão implementados no momento:

| Classe do avaliador | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

O avaliador pode ser definido na fórmula do arquivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) na pasta `recipe`. O exemplo de código que habilita o `DefaultBinaryClassificationEvaluator` é mostrado abaixo:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Depois que uma classe de avaliador é ativada, várias métricas são calculadas durante o treinamento por padrão. As métricas padrão podem ser declaradas explicitamente ao adicionar a seguinte linha ao seu `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Se a métrica não for definida, as métricas padrão estarão ativas.

Uma métrica específica pode ser habilitada alterando-se o valor de `evaluation.metrics.com`. No exemplo a seguir, a métrica F-Score está ativada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

A tabela a seguir especifica as métricas padrão para cada classe. Um usuário também pode usar os valores na coluna `evaluation.metric` para habilitar uma métrica específica.

| `evaluator.class` | Métricas padrão | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Characteristics <br>-Area Sob As Características Operacionais Do Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Characteristics <br>-Area Sob As Características Operacionais Do Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisão Média Média (MAP) <br>-Ganho Cumulativo Descontado Normalizado <br>-Classificação Recíproca Média <br>-Métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de avaliação personalizadas para a Scala

O avaliador personalizado pode ser fornecido estendendo a interface de `MLEvaluator.scala` no arquivo `Evaluator.scala`. No arquivo de exemplo [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala), definimos funções `split()` e `evaluate()` personalizadas. Nossa função `split()` divide nossos dados aleatoriamente com uma proporção de 8:2 e nossa função `evaluate()` define e retorna 3 métricas: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Para a classe `MLMetric`, não use `"measures"` para `valueType` ao criar um novo `MLMetric`; caso contrário, a métrica não será preenchida na tabela de métricas de avaliação personalizadas.
>  
> Faça isto: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Não é isto: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Uma vez definido na fórmula, o próximo passo é ativá-lo nas receitas. Isso é feito no arquivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) da pasta `resources` do projeto. Aqui o `evaluation.class` está definido como a classe `Evaluator` definida em `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

No [!DNL Data Science Workspace], o usuário poderia ver os insights na guia &quot;Métricas de avaliação&quot; na página de experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Até agora, não há métricas de avaliação padrão para [!DNL Python] ou [!DNL Tensorflow]. Assim, para obter as métricas de avaliação para [!DNL Python] ou [!DNL Tensorflow], será necessário criar uma métrica de avaliação personalizada. Isso pode ser feito implementando a classe `Evaluator`.

#### Métricas de avaliação personalizadas para [!DNL Python]

Para métricas de avaliação personalizadas, há dois métodos principais que precisam ser implementados para o avaliador: `split()` e `evaluate()`.

Para [!DNL Python], esses métodos seriam definidos em [valuator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para a classe `Evaluator`. Siga o link [valuator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para obter um exemplo de `Evaluator`.

A criação de métricas de avaliação em [!DNL Python] requer que o usuário implemente os métodos `evaluate()` e `split()`.

O método `evaluate()` retorna o objeto de métrica que contém uma matriz de objetos de métrica com propriedades `name`, `value` e `valueType`.

A finalidade do método `split()` é inserir dados e produzir um conjunto de dados de treinamento e teste. Em nosso exemplo, o método `split()` insere dados usando o SDK `DataSetReader` e, em seguida, limpa os dados removendo colunas não relacionadas. A partir daí, os recursos adicionais são criados a partir dos recursos brutos existentes nos dados.

O método `split()` deve retornar um dataframe de treinamento e teste que é usado pelos métodos `pipeline()` para treinar e testar o modelo ML.

#### Métricas de avaliação personalizadas para Tensorflow

Para [!DNL Tensorflow], semelhante a [!DNL Python], os métodos `evaluate()` e `split()` na classe `Evaluator` precisarão ser implementados. Para `evaluate()`, as métricas devem ser retornadas, enquanto `split()` retorna o trem e os conjuntos de dados de teste.

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

A partir de agora, não há métricas de avaliação padrão para R. Assim, para obter as métricas de avaliação para R, será necessário definir a classe `applicationEvaluator` como parte da fórmula.

#### Métricas de avaliação personalizadas para o R

A principal finalidade do `applicationEvaluator` é retornar um objeto JSON que contém pares de valores-chave de métricas.

Este [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) pode ser usado como exemplo. Neste exemplo, o `applicationEvaluator` está dividido em três seções familiares:

- Carregar dados
- Preparação de dados/engenharia de recursos
- Recuperar modelo salvo e avaliar

Os dados são carregados primeiro em um conjunto de dados a partir de uma origem conforme definido em [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir daí, os dados são limpos e projetados para se ajustarem ao modelo de aprendizado de máquina. Por fim, o modelo é usado para fazer uma previsão usando nosso conjunto de dados e, a partir dos valores previstos e valores reais, as métricas são calculadas. Nesse caso, MAPE, MAE e RMSE são definidos e retornados no objeto `metrics`.

## Uso de métricas e gráficos de visualização pré-criados

O [!DNL Sensei Model Insights Framework] oferecerá suporte a um modelo padrão para cada tipo de algoritmo de aprendizado de máquina. A tabela abaixo mostra classes comuns de algoritmo de aprendizado de máquina de alto nível e as métricas e visualizações de avaliação correspondentes.

| Tipo de algoritmo ML | Métricas de avaliação | Visualizações |
| --- | --- | --- |
| Regressão | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Curva de sobreposição de valores previstos versus reais |
| Classificação binária | - Matriz de confusão<br>- Precision-recall<br>- Precisão<br>- Pontuação F (especificamente F1 ,F2)<br>- AUC<br>- ROC | Curva ROC e matriz de confusão |
| Classificação de várias classes | -Matriz de confusão <br>- Para cada classe: <br>- precisão-recall <br>- Pontuação F (especificamente F1, F2) | Curva ROC e matriz de confusão |
| Agrupamento (c/ verdade fundamental) | - NMI (pontuação normalizada de informações mútuas), AMI (pontuação ajustada de informações mútuas)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- pontuação de homogeneidade, pontuação de integridade e medida V<br>- FMI (índice Fowlkes-Mallows)<br>- Pureza<br>- índice Jaccard | Gráfico de clusters mostrando clusters e centroides com tamanhos relativos de cluster que refletem os pontos de dados que estão no cluster |
| Clustering (sem verdade fundamental) | - Inércia<br>- Coeficiente de silhueta<br>- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- índice Dunn | Gráfico de clusters mostrando clusters e centroides com tamanhos relativos de cluster que refletem os pontos de dados que estão no cluster |
| Recomendação | -Precisão Média Média (MAP) <br>-Ganho Cumulativo Descontado Normalizado <br>-Classificação Recíproca Média <br>-Métrica K | A definir |
| Casos de uso do TensorFlow | Análise do modelo TensorFlow (TFMA) | Comparação/visualização do modelo de rede neural Deepcompare |
| Outro/mecanismo de captura de erros | Lógica de métrica personalizada (e gráficos de avaliação correspondentes) definida pelo autor do modelo. Tratamento de erros naturais em caso de incompatibilidade de modelo | Tabela com pares de valores-chave para métricas de avaliação |
