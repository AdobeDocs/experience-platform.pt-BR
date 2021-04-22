---
keywords: Experience Platform, otimizar, modelo, Data Science Workspace, tópicos populares, insights do modelo
solution: Experience Platform
title: Otimizar um modelo usando a estrutura de insights do modelo
topic-legacy: tutorial
type: Tutorial
description: A Estrutura de insights do modelo fornece ao cientista de dados ferramentas no Data Science Workspace para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Otimizar um modelo usando a estrutura de insights do modelo

A Estrutura de insights do modelo fornece ao cientista de dados ferramentas em [!DNL Data Science Workspace] para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado de máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem melhores decisões de otimização de modelos para seus clientes finais.

## O que são métricas?

Depois de implementar e treinar um modelo, o próximo passo que um cientista de dados faria é descobrir o desempenho do modelo. Várias métricas são usadas para descobrir a eficácia de um modelo em comparação com outras. Alguns exemplos de métricas usadas incluem:
- Precisão da classificação
- Área sob curva
- Matriz de confusão
- Relatório de classificação

## Configuração do código da receita

Atualmente, a Estrutura de insights do modelo oferece suporte aos seguintes tempos de execução:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

O código de amostra das receitas pode ser encontrado no repositório [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) em `recipes`. Arquivos específicos deste repositório serão referenciados neste tutorial.

### Escala {#scala}

Há duas maneiras de trazer métricas para as receitas. Uma é usar as métricas de avaliação padrão fornecidas pelo SDK e a outra é gravar métricas de avaliação personalizadas.

#### Métricas de avaliação padrão para Scala

As avaliações padrão são calculadas como parte dos algoritmos de classificação. Estes são alguns valores padrão para avaliadores que estão implementados no momento:

| Classe do Avaliador | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

O avaliador pode ser definido na fórmula no arquivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) na pasta `recipe`. O código de amostra que habilita o `DefaultBinaryClassificationEvaluator` é mostrado abaixo:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Após habilitar uma classe de avaliador, várias métricas serão calculadas durante o treinamento por padrão. As métricas padrão podem ser declaradas explicitamente, adicionando a seguinte linha em seu `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Se a métrica não estiver definida, as métricas padrão estarão ativas.

Uma métrica específica pode ser ativada alterando o valor de `evaluation.metrics.com`. No exemplo a seguir, a métrica de pontuação F é ativada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

A tabela a seguir indica as métricas padrão para cada classe. Um usuário também pode usar os valores na coluna `evaluation.metric` para ativar uma métrica específica.

| `evaluator.class` | Métricas padrão | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Precisão <br>-Receiver Operating Characteres <br>-Área Sob as Características Operacionais do Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Precisão <br>-Receiver Operating Characteres <br>-Área Sob as Características Operacionais do Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisão média (MAP) <br>-Ganho cumulativo descontado normalizado <br>-Classificação recíproca média <br>-Métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de avaliação personalizadas para Scala

O avaliador personalizado pode ser fornecido estendendo a interface de `MLEvaluator.scala` em seu arquivo `Evaluator.scala`. No exemplo do arquivo [Evaluator.escala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala), definimos funções `split()` e `evaluate()` personalizadas. Nossa função `split()` divide nossos dados aleatoriamente com uma proporção de 8:2 e nossa função `evaluate()` define e retorna 3 métricas: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Para a classe `MLMetric`, não use `"measures"` para `valueType` ao criar um novo `MLMetric`; caso contrário, a métrica não será preenchida na tabela de métricas de avaliação personalizadas.
>  
> Faça isso: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Não é isso: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Uma vez definido na receita, a próxima etapa é habilitá-la nas receitas. Isso é feito no arquivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) na pasta `resources` do projeto. Aqui, `evaluation.class` está definido para a classe `Evaluator` definida em `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

No [!DNL Data Science Workspace], o usuário poderá ver os insights na guia &quot;Métricas de Avaliação&quot; na página de experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

A partir de agora, não há métricas de avaliação padrão para [!DNL Python] ou [!DNL Tensorflow]. Assim, para obter as métricas de avaliação para [!DNL Python] ou [!DNL Tensorflow], será necessário criar uma métrica de avaliação personalizada. Isso pode ser feito implementando a classe `Evaluator` .

#### Métricas de avaliação personalizadas para [!DNL Python]

Para métricas de avaliação personalizadas, há dois métodos principais que precisam ser implementados para o avaliador: `split()` e `evaluate()`.

Para [!DNL Python], esses métodos seriam definidos em [avaliator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para a classe `Evaluator`. Siga o link [valuator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para obter um exemplo do `Evaluator`.

A criação de métricas de avaliação em [!DNL Python] requer que o usuário implemente os métodos `evaluate()` e `split()`.

O método `evaluate()` retorna o objeto de métrica que contém uma matriz de objetos de métrica com propriedades `name`, `value` e `valueType`.

O objetivo do método `split()` é inserir dados e produzir um conjunto de dados de treinamento e teste. Em nosso exemplo, o método `split()` insere dados usando o SDK `DataSetReader` e, em seguida, limpa os dados removendo colunas não relacionadas. A partir daí, recursos adicionais são criados a partir de recursos brutos existentes nos dados.

O método `split()` deve retornar um quadro de dados de formação e de ensaio que é depois utilizado pelos métodos `pipeline()` para treinar e testar o modelo ML.

#### Métricas de avaliação personalizadas para Tensorflow

Para [!DNL Tensorflow], semelhante a [!DNL Python], os métodos `evaluate()` e `split()` na classe `Evaluator` precisarão ser implementados. Para `evaluate()`, as métricas devem ser retornadas enquanto `split()` retorna o trem e os conjuntos de dados de teste.

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

A partir de agora, não há métricas de avaliação padrão para R. Assim, para obter as métricas de avaliação para R, você precisará definir a classe `applicationEvaluator` como parte da receita.

#### Métricas de avaliação personalizadas para R

O principal objetivo do `applicationEvaluator` é retornar um objeto JSON contendo pares de valores chave de métricas.

Este [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) pode ser usado como exemplo. Neste exemplo, o `applicationEvaluator` é dividido em três seções familiares:
- Carregar dados
- Preparação de dados/engenharia de recursos
- Recuperar modelo salvo e avaliar

Os dados são carregados pela primeira vez em um conjunto de dados de uma fonte, conforme definido em [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir daí, os dados são limpos e projetados para se encaixarem no modelo de aprendizado de máquina. Por fim, o modelo é usado para fazer uma previsão usando nosso conjunto de dados e dos valores previstos e valores reais, as métricas são calculadas. Nesse caso, MAPE, MAE e RMSE são definidos e retornados no objeto `metrics` .

## Uso de métricas e gráficos de visualização pré-criados

O [!DNL Sensei Model Insights Framework] oferecerá suporte a um modelo padrão para cada tipo de algoritmo de aprendizado de máquina. A tabela abaixo mostra as classes comuns de algoritmo de aprendizagem de máquina de alto nível e as métricas e visualizações de avaliação correspondentes.

| Tipo de algoritmo ML | Métricas de avaliação | Visualizações |
| --- | --- | --- |
| Regressão | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Curva de sobreposição de valores previstos e reais |
| Classificação binária | - Matriz de conversão<br>- Precisão-recuperação<br>- Precisão<br>- Pontuação F (especificamente F1,F2)<br>- AUC<br>- ROC | Curva de ROC e matriz de confusão |
| Classificação multiclasse | -Matriz de conversão <br>- Para cada classe: <br>- precisão de chamada <br>- pontuação F (especificamente F1, F2) | Curva de ROC e matriz de confusão |
| Clustering (sem verdade básica) | - NMI (pontuação normalizada de informações mútuas), AMI (pontuação de informações mútuas ajustada)<br>- RI (índice Rand ajustado), ARI (índice Rand ajustado)<br>- pontuação de homogeneidade, pontuação de integridade e V-measure<br>- FMI (índice Fowlkes-Mallow)<br>- Pureza<br>- Índice de cartão Jacob | Gráfico de clusters mostrando clusters e centróides com tamanhos de cluster relativos que refletem pontos de dados que estão no cluster |
| Clustering (sem verdade básica) | - Inertia<br>- Coeficiente de silhueta<br>- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice Dunn | Gráfico de clusters mostrando clusters e centróides com tamanhos de cluster relativos que refletem pontos de dados que estão no cluster |
| Recomendação | -Precisão média (MAP) <br>-Ganho cumulativo descontado normalizado <br>-Classificação recíproca média <br>-Métrica K | TBD |
| Casos de uso do TensorFlow | Análise de Modelo de Fluxo de Tensor (TFMA) | Comparação/visualização detalhada do modelo de rede neural |
| Mecanismo de captura de erros/outros | Lógica de métrica personalizada (e gráficos de avaliação correspondentes) definida pelo autor do modelo. Tratamento de erros significativos em caso de incompatibilidade de modelos | Tabela com pares de valores chave para métricas de avaliação |
