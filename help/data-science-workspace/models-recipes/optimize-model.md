---
keywords: Experience Platform; otimizar; modelo; Área de trabalho de ciência de dados; tópicos populares; insights de modelo
solution: Experience Platform
title: Otimize um modelo usando a estrutura Insights modelo
type: Tutorial
description: A Estrutura Insights Modelo fornece ao cientista de dados ferramentas em data science Área de trabalho para fazer escolhas rápidas e informadas para modelos ideais de aprendizagem de máquina com base em experimentos.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---

# Otimize um modelo usando o modelo Insights estrutura

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

O Model Insights Framework fornece ao cientista de dados ferramentas para fazer escolhas [!DNL Data Science Workspace] rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia dos fluxo de Trabalho de aprendizagem de máquina, bem como melhorará a facilidade de uso para os cientistas de dados. Isso é feito fornecendo uma modelo padrão para cada tipo de algoritmo de aprendizado de máquina para ajudar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem melhores decisões de otimização de modelo para seus clientes finais.

## O que são métricas?

Depois de implementar e treinamento um modelo, o próximo passo que um cientista de dados faria é descobrir o desempenho do modelo. Várias métricas são usadas para descobrir a eficiência de um modelo em comparação com outras. Alguns exemplos de métricas usadas incluem:
- Precisão da classificação
- Área sob a curva
- Matriz de confusão
- Relatório de classificação

## Configuração do código de fórmula

Atualmente, o Modelo Insights Framework suporta os seguintes tempos de execução:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

O código de amostra para receitas pode ser encontrado no repositório [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) em `recipes`. Os arquivos específicos deste repositório serão referenciados neste tutorial.

### Scala {#scala}

Há duas maneiras de inserir métricas nas receitas. Uma é usar as métricas de avaliação padrão fornecidas pelo SDK e a outra é gravar métricas de avaliação personalizadas.

#### Métricas de avaliação padrão para Scala

As avaliações padrão são calculadas como parte dos algoritmos de classificação. Estes são alguns valores padrão para avaliadores implementados atualmente:

| Classe avaliador | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

O avaliador pode ser definido na fórmula no [arquivo aplicativo.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) na `recipe` pasta. O código de amostra que permite a exibição `DefaultBinaryClassificationEvaluator` abaixo é mostrado abaixo:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Depois que uma classe de avaliador for ativada, várias métricas serão calculadas durante treinamento por padrão. Métricas padrão podem ser declaradas explicitamente adicionando a seguinte linha.`application.properties`

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Se a métrica não estiver definida, as métricas padrão estarão ativas.

É possível ativar um métrica específico alterando o valor de `evaluation.metrics.com`. No exemplo a seguir, a Pontuação F métrica está ativada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

A tabela a seguir indica as métricas padrão para cada classe. Uma usuário também pode usar os valores na `evaluation.metric` coluna para habilitar uma métrica específica.

| `evaluator.class` | Métricas padrão | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Characteristics <br>-Area Under the Receiver Operating Characteristics | -`PRECISION` <br>- -`CONFUSION_MATRIX` <br><br>`RECALL` -`FSCORE` <br>-`ACCURACY` <br>- -`ROC` <br>`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Characteristics <br>-Area Under the Receiver Operating Characteristics | -`PRECISION` <br>- -`CONFUSION_MATRIX` <br><br>`RECALL` -`FSCORE` <br>-`ACCURACY` <br>- -`ROC` <br>`AUROC` |
| `RecommendationsEvaluator` | -Average Precision (MAP) <br>-Normalized Discounted Cumulative Gain <br>-Mean Reciprocal Rank <br>-Metric K | - -`MEAN_AVERAGE_PRECISION` <br><br>`NDCG` - - -`MRR` <br>`METRIC_K` |


#### Métricas de avaliação personalizadas para o Scala

O avaliador personalizado pode ser fornecido estendendo a interface do `MLEvaluator.scala` seu `Evaluator.scala` arquivo. No arquivo Evaluator.scala de exemplo[, definimos personalizado `split()` e `evaluate()` funções.](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) Nossa `split()` função divide nossos dados aleatoriamente com uma proporção de 8:2 e nossa `evaluate()` função define e retorna 3 métricas: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Para a `MLMetric` classe, não use `"measures"` para `valueType` quando criar outra nova `MLMetric` , a métrica não será preenchida na tabela de métricas de avaliação personalizadas.
>  
> Faça isso: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Isso não é o seguinte: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Depois de definido na fórmula, a próxima etapa é habilitá-lo nas fórmulas. Isso é feito no [arquivo aplicativo.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) da pasta do `resources` projeto. Aqui, o `evaluation.class` conjunto é definido para a `Evaluator` classe definida em `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

No usuário [!DNL Data Science Workspace]seria possível ver os insights nas &quot;Métricas de avaliação&quot; guia no experimento página.

### [!DNL Python/Tensorflow] {#pythontensorflow}

A partir de agora, não há métricas de avaliação padrão para [!DNL Python] ou [!DNL Tensorflow]. Assim, para obter as métricas de avaliação para [!DNL Python] ou [!DNL Tensorflow], será necessário criar uma avaliação personalizada métrica. Isso pode ser feito implementando a `Evaluator` classe.

#### Métricas de avaliação personalizadas para [!DNL Python]

Para métricas de avaliação personalizadas, existem dois métodos principais que precisam ser implementados para o avaliador: `split()` e `evaluate()`.

Pois [!DNL Python], esses métodos seriam definidos em [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para a `Evaluator` classe. Siga a [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) link para obter um exemplo do `Evaluator`.

A criação de métricas [!DNL Python] de avaliação requer que as usuário implementar e `split()` os `evaluate()` métodos.

O `evaluate()` método retorna o métrica objeto que contém uma matriz de objetos métrica com propriedades de `name`, `value`e `valueType`.

O objetivo do `split()` método é inserir dados e criar um treinamento e um conjunto de dados de teste. No nosso exemplo, o `split()` método insira dados usando o `DataSetReader` SDK e, em seguida, limpa os dados removendo colunas não relacionadas. A partir daí, recursos adicionais são criados a partir de recursos brutos existentes nos dados.

O `split()` método deve retornar um treinamento e testar o `pipeline()` período de dados que é então usado pelos métodos para treinar e teste o modelo ML.

#### Métricas de avaliação personalizadas para o tensorflow

Para [!DNL Tensorflow], semelhante a [!DNL Python], os métodos `evaluate()` e `split()` na `Evaluator` classe precisarão ser implementados. Em `evaluate()`, as métricas devem ser retornadas enquanto `split()` retorna o trem e o teste conjuntos de dados.

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

A partir de agora, não há métricas de avaliação padrão para R. Assim, para obter as métricas de avaliação para R, você precisará definir a `applicationEvaluator` classe como parte do fórmula.

#### Métricas de avaliação personalizadas para R

O objetivo principal é `applicationEvaluator` retornar um objeto JSON contendo pares de métricas de valor chave.

Este [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) pode ser usado como um exemplo. Neste exemplo, ele `applicationEvaluator` é dividido em três seções familiares:
- Carregar dados
- Preparação de dados/engenharia de recursos
- Recuperar modelo salvo e avaliar

Os dados são carregados primeiro em um conjunto de dados a partir de uma origem conforme definido em [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir daí, os dados são limpos e projetados para se ajustarem ao modelo de aprendizado de máquina. Por fim, o modelo é usado para fazer uma previsão usando nosso conjunto de dados e, a partir dos valores previstos e valores reais, as métricas são calculadas. Nesse caso, MAPE, MAE e RMSE são definidos e retornados no `metrics` objeto.

## Uso pré-construído métricas e gráficos de visualização

O [!DNL Sensei Model Insights Framework] oferecerá suporte a um modelo padrão para cada tipo de algoritmo de aprendizado de máquina. A tabela abaixo mostra classes comuns de algoritmo de aprendizado de máquina de alto nível e as métricas e visualizações de avaliação correspondentes.

| Tipo de algoritmo ML | Métricas de avaliação | Visualizações |
| --- | --- | --- |
| Regressão | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Valores previstos versus reais sobrepor curva |
| Binário classificação | - Matriz de confusão<br>- Precisão-recall<br>- Precisão<br> - Pontuação F (especificamente F1 ,F2)<br>- AUC<br>- ROC | Curva ROC e matriz de confusão |
| Classificação de várias classes | -Matriz de confusão <br>- Para cada classe: <br>- precisão <br>de recall - Pontuação F (especificamente F1, F2) | Curva ROC e matriz de confusão |
| Agrupamento (c/ verdade fundamental) | - NMI (pontuação normalizada de informações mútuas), AMI (pontuação ajustada de informações mútuas)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- pontuação de homogeneidade, pontuação de integridade e medida V<br>- FMI (índice Fowlkes-Mallows)<br>- Pureza<br>- índice Jaccard | Gráfico de clusters mostrando clusters e centroides com tamanhos relativos de cluster que refletem os pontos de dados que estão no cluster |
| Clustering (sem verdade fundamental) | - Inércia<br>- Coeficiente de silhueta<br>- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- índice Dunn | Gráfico de clusters mostrando clusters e centroides com tamanhos relativos de cluster que refletem os pontos de dados que estão no cluster |
| Recomendação | -Precisão Média Média (MAP) <br>-Ganho Cumulativo Descontado Normalizado <br>-Classificação Recíproca Média <br>-Métrica K | A ser definido |
| Casos de uso do TensorFlow | Análise do modelo de fluxo de tensor (TFMA) | Comparação/visualização de modelos de rede neural Deepcompare |
| Mecanismo de captura de outros/erros | Lógica de métrica personalizada (e gráficos de avaliação correspondentes) definida pelo autor do modelo. Tratamento de erros graciosos em caso de modelo incompatibilidade | Tabela com pares de valor-chave para métricas de avaliação |
