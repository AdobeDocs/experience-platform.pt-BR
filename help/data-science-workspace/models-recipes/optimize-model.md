---
keywords: Experience Platform, otimizar, modelo, Data Science Workspace, tópicos populares, insights do modelo
solution: Experience Platform
title: Otimizar um modelo usando a estrutura de insights do modelo
type: Tutorial
description: A Estrutura de insights do modelo fornece ao cientista de dados ferramentas no Data Science Workspace para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Otimizar um modelo usando a estrutura de insights do modelo

A Estrutura de insights do modelo fornece ao cientista de dados ferramentas em [!DNL Data Science Workspace] fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado de máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem melhores decisões de otimização de modelos para seus clientes finais.

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

O código de amostra das receitas pode ser encontrado no [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) repositório em `recipes`. Arquivos específicos deste repositório serão referenciados neste tutorial.

### Scala {#scala}

Há duas maneiras de trazer métricas para as receitas. Uma é usar as métricas de avaliação padrão fornecidas pelo SDK e a outra é gravar métricas de avaliação personalizadas.

#### Métricas de avaliação padrão para Scala

As avaliações padrão são calculadas como parte dos algoritmos de classificação. Estes são alguns valores padrão para avaliadores que estão implementados no momento:

| Classe do Avaliador | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

O avaliador pode ser definido na fórmula na variável [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) no `recipe` pasta. Exemplo de código que permite o `DefaultBinaryClassificationEvaluator` é mostrado abaixo:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Após habilitar uma classe de avaliador, várias métricas serão calculadas durante o treinamento por padrão. As métricas padrão podem ser declaradas explicitamente adicionando a seguinte linha à sua `application.properties`.

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

A tabela a seguir indica as métricas padrão para cada classe. Um usuário também pode usar os valores na variável `evaluation.metric` para ativar uma métrica específica.

| `evaluator.class` | Métricas padrão | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precisão <br>-Recall <br>- Matriz de Confusão <br>-Pontuação F <br>-Precisão <br>- Características operacionais do receptor <br>-Área sob as características operacionais do receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precisão <br>-Recall <br>- Matriz de Confusão <br>-Pontuação F <br>-Precisão <br>- Características operacionais do receptor <br>-Área sob as características operacionais do receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisão média (MAP) <br>-Ganho Cumulativo Descontado Normalizado <br>-Classificação Recíproca Média <br>-Métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de avaliação personalizadas para Scala

O avaliador personalizado pode ser fornecido estendendo a interface de `MLEvaluator.scala` em seu `Evaluator.scala` arquivo. No exemplo [Evaluator.escala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) , definimos personalizado `split()` e `evaluate()` funções. Nosso `split()` divide nossos dados aleatoriamente com uma proporção de 8:2 e nossos `evaluate()` define e retorna 3 métricas: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Para o `MLMetric` classe, não use `"measures"` para `valueType` ao criar um novo `MLMetric` caso contrário, a métrica não será preenchida na tabela de métricas de avaliação personalizadas.
>  
> Faça isso: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Não é isso: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Uma vez definido na receita, a próxima etapa é habilitá-la nas receitas. Isso é feito no [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) no `resources` pasta. Aqui a `evaluation.class` é definido como `Evaluator` classe definida em `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

No [!DNL Data Science Workspace], o usuário poderá ver os insights na guia &quot;Métricas de avaliação&quot; na página de experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

A partir de agora, não há métricas de avaliação padrão para [!DNL Python] ou [!DNL Tensorflow]. Assim, para obter as métricas de avaliação para o [!DNL Python] ou [!DNL Tensorflow], será necessário criar uma métrica de avaliação personalizada. Isso pode ser feito implementando a variável `Evaluator` classe .

#### Métricas de avaliação personalizadas para [!DNL Python]

Para métricas de avaliação personalizadas, há dois métodos principais que precisam ser implementados para o avaliador: `split()` e `evaluate()`.

Para [!DNL Python], esses métodos seriam definidos em [avaliador.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para `Evaluator` classe . Siga as [avaliador.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para obter um exemplo da variável `Evaluator`.

Criar métricas de avaliação no [!DNL Python] exige que o usuário implemente a variável `evaluate()` e `split()` métodos.

O `evaluate()` retorna o objeto de métrica que contém uma matriz de objetos de métrica com propriedades de `name`, `value`e `valueType`.

O objetivo da `split()` é inserir dados e produzir um conjunto de dados de treinamento e teste. Em nosso exemplo, a variável `split()` O método insere dados usando o `DataSetReader` O SDK e, em seguida, limpa os dados removendo colunas não relacionadas. A partir daí, recursos adicionais são criados a partir de recursos brutos existentes nos dados.

O `split()` O método deve retornar um dado de treinamento e teste que é usado pelo `pipeline()` métodos de formação e ensaio do modelo ML.

#### Métricas de avaliação personalizadas para Tensorflow

Para [!DNL Tensorflow], semelhante a [!DNL Python], os métodos `evaluate()` e `split()` no `Evaluator` A classe precisará ser implementada. Para `evaluate()`, as métricas devem ser retornadas enquanto `split()` retorna o comboio e os conjuntos de dados de ensaio.

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

A partir de agora, não há métricas de avaliação padrão para R. Assim, para obter as métricas de avaliação para R, você precisará definir a variável `applicationEvaluator` como parte da receita.

#### Métricas de avaliação personalizadas para R

O principal objetivo da `applicationEvaluator` é retornar um objeto JSON contendo pares de métricas de valores chave.

Essa [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) pode ser usado como exemplo. Neste exemplo, a variável `applicationEvaluator` O é dividido em três seções familiares:
- Carregar dados
- Preparação de dados/engenharia de recursos
- Recuperar modelo salvo e avaliar

Os dados são carregados pela primeira vez em um conjunto de dados a partir de uma fonte, conforme definido em [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir daí, os dados são limpos e projetados para se encaixarem no modelo de aprendizado de máquina. Por fim, o modelo é usado para fazer uma previsão usando nosso conjunto de dados e dos valores previstos e valores reais, as métricas são calculadas. Nesse caso, MAPE, MAE e RMSE são definidos e retornados no `metrics` objeto.

## Uso de métricas e gráficos de visualização pré-criados

O [!DNL Sensei Model Insights Framework] oferecerá suporte a um modelo padrão para cada tipo de algoritmo de aprendizado de máquina. A tabela abaixo mostra as classes comuns de algoritmo de aprendizagem de máquina de alto nível e as métricas e visualizações de avaliação correspondentes.

| Tipo de algoritmo ML | Métricas de avaliação | Visualizações |
| --- | --- | --- |
| Regressão | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Curva de sobreposição de valores previstos e reais |
| Classificação binária | - Matriz de perfusão<br>- Recolha de precisão<br>- Precisão<br>- pontuação F (especificamente F1, F2)<br>- AUC<br>- ROC | Curva de ROC e matriz de confusão |
| Classificação multiclasse | - Matriz de perfusão <br>- Para cada classe: <br>- precisão da evocação <br>- pontuação F (especificamente F1, F2) | Curva de ROC e matriz de confusão |
| Clustering (sem verdade básica) | - NMI (pontuação de informação mútua normalizada), AMI (pontuação de informação mútua ajustada)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- pontuação de homogeneidade, pontuação de integralidade e medida V<br>- FMI (índice Fowlkes-Mallow)<br>- Pureza<br>- Índice Jaccard | Gráfico de clusters mostrando clusters e centróides com tamanhos de cluster relativos que refletem pontos de dados que estão no cluster |
| Clustering (sem verdade básica) | - Inércia<br>- Coeficiente de silhueta<br>- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice de cobrança | Gráfico de clusters mostrando clusters e centróides com tamanhos de cluster relativos que refletem pontos de dados que estão no cluster |
| Recomendação | -Precisão média (MAP) <br>-Ganho Cumulativo Descontado Normalizado <br>-Classificação Recíproca Média <br>-Métrica K | TBD |
| Casos de uso do TensorFlow | Análise de Modelo de Fluxo de Tensor (TFMA) | Comparação/visualização detalhada do modelo de rede neural |
| Mecanismo de captura de erros/outros | Lógica de métrica personalizada (e gráficos de avaliação correspondentes) definida pelo autor do modelo. Tratamento de erros significativos em caso de incompatibilidade de modelos | Tabela com pares de valores chave para métricas de avaliação |
