---
keywords: Experience Platform;otimizar;modelo;Data Science Workspace;tópicos populares;insights de modelo
solution: Experience Platform
title: Otimizar um modelo usando a estrutura do Model Insights
type: Tutorial
description: A estrutura do Model Insights fornece ao cientista de dados ferramentas no Espaço de trabalho de ciência de dados para fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Otimizar um modelo usando a estrutura do Model Insights

A Estrutura do Model Insights fornece ao cientista de dados ferramentas no [!DNL Data Science Workspace] fazer escolhas rápidas e informadas para modelos ideais de aprendizado de máquina com base em experimentos. A estrutura melhorará a velocidade e a eficácia do fluxo de trabalho de aprendizado de máquina, bem como a facilidade de uso para cientistas de dados. Isso é feito fornecendo um modelo padrão para cada tipo de algoritmo de aprendizado de máquina para auxiliar no ajuste do modelo. O resultado final permite que cientistas de dados e cientistas de dados cidadãos tomem melhores decisões de otimização de modelos para seus clientes finais.

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

O código de amostra para receitas pode ser encontrado no [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) repositório em `recipes`. Os arquivos específicos deste repositório serão referenciados neste tutorial.

### Scala {#scala}

Há duas maneiras de inserir métricas nas receitas. Uma é usar as métricas de avaliação padrão fornecidas pelo SDK e a outra é gravar métricas de avaliação personalizadas.

#### Métricas de avaliação padrão para a Scala

As avaliações padrão são calculadas como parte dos algoritmos de classificação. Estes são alguns valores padrão para avaliadores que estão implementados no momento:

| Classe do avaliador | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

O avaliador pode ser definido na fórmula do [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) arquivo no `recipe` pasta. Código de exemplo que habilita o `DefaultBinaryClassificationEvaluator` é mostrado abaixo:

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

Uma métrica específica pode ser ativada ao alterar o valor de `evaluation.metrics.com`. No exemplo a seguir, a métrica F-Score está ativada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

A tabela a seguir especifica as métricas padrão para cada classe. Um usuário também pode usar os valores na variável `evaluation.metric` para ativar uma métrica específica.

| `evaluator.class` | Métricas padrão | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precisão <br>-Retroceder <br>-Matriz de Confusão <br>-F-Score <br>-Precisão <br>-Características de operação do receptor <br>-Área sob as características operacionais do receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precisão <br>-Retroceder <br>-Matriz de Confusão <br>-F-Score <br>-Precisão <br>-Características de operação do receptor <br>-Área sob as características operacionais do receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisão média (MAP) <br>-Ganho Acumulado Descontado Normalizado <br>-Classificação Recíproca Média <br>-Métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de avaliação personalizadas para a Scala

O avaliador personalizado pode ser fornecido estendendo a interface do `MLEvaluator.scala` no seu `Evaluator.scala` arquivo. No exemplo [Avaliador.escala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) arquivo, definimos personalizado `split()` e `evaluate()` funções. Nosso `split()` A função divide nossos dados aleatoriamente com uma proporção de 8:2 e nossos `evaluate()` define e retorna três métricas: MAPE, MAE e RMSE.

>[!IMPORTANT]
>
>Para o `MLMetric` classe, não use `"measures"` para `valueType` ao criar um novo `MLMetric` caso contrário, a métrica não será preenchida na tabela métricas de avaliação personalizadas.
>  
> Faça o seguinte: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Não isto: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Uma vez definido na fórmula, o próximo passo é ativá-lo nas receitas. Isso é feito no [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) no arquivo do projeto `resources` pasta. Aqui, o `evaluation.class` está definido como `Evaluator` classe definida em `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

No [!DNL Data Science Workspace], o usuário poderá ver os insights na guia &quot;Métricas de avaliação&quot; na página de experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Por enquanto, não há métricas de avaliação padrão para [!DNL Python] ou [!DNL Tensorflow]. Assim, para obter as métricas de avaliação para [!DNL Python] ou [!DNL Tensorflow], será necessário criar uma métrica de avaliação personalizada. Isso pode ser feito implementando o `Evaluator` classe.

#### Métricas de avaliação personalizadas para [!DNL Python]

Para métricas de avaliação personalizadas, há dois métodos principais que precisam ser implementados para o avaliador: `split()` e `evaluate()`.

Para [!DNL Python], estes métodos seriam definidos em [avaliador.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para o `Evaluator` classe. Siga as [avaliador.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para obter um exemplo do `Evaluator`.

Criação de métricas de avaliação no [!DNL Python] exige que o usuário implemente o `evaluate()` e `split()` métodos.

A variável `evaluate()` método retorna o objeto de métrica que contém uma matriz de objetos de métrica com propriedades de `name`, `value`, e `valueType`.

O objetivo da `split()` é inserir dados e produzir um treinamento e um conjunto de dados de teste. No nosso exemplo, a variável `split()` o método insere dados usando o `DataSetReader` e, em seguida, limpa os dados removendo colunas não relacionadas. A partir daí, os recursos adicionais são criados a partir dos recursos brutos existentes nos dados.

A variável `split()` deve retornar um quadro de dados de treinamento e teste que é então usado pelo `pipeline()` métodos para treinar e testar o modelo de ML.

#### Métricas de avaliação personalizadas para Tensorflow

Para [!DNL Tensorflow], semelhante a [!DNL Python], os métodos `evaluate()` e `split()` no `Evaluator` precisará ser implementada. Para `evaluate()`, as métricas devem ser retornadas enquanto `split()` retorna o trem e os conjuntos de dados de teste.

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

A partir de agora, não há métricas de avaliação padrão para R. Assim, para obter as métricas de avaliação para R, será necessário definir o `applicationEvaluator` classe como parte da fórmula.

#### Métricas de avaliação personalizadas para o R

O principal objetivo da `applicationEvaluator` é retornar um objeto JSON que contém pares de valores-chave das métricas.

Este [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) pode ser usado como exemplo. Neste exemplo, a variável `applicationEvaluator` O está dividido em três seções familiares:
- Carregar dados
- Preparação de dados/engenharia de recursos
- Recuperar modelo salvo e avaliar

Os dados são carregados pela primeira vez em um conjunto de dados a partir de uma origem, conforme definido na [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir daí, os dados são limpos e projetados para se ajustarem ao modelo de aprendizado de máquina. Por fim, o modelo é usado para fazer uma previsão usando nosso conjunto de dados e, a partir dos valores previstos e valores reais, as métricas são calculadas. Nesse caso, MAPE, MAE e RMSE são definidos e retornados na variável `metrics` objeto.

## Uso de métricas e gráficos de visualização pré-criados

A variável [!DNL Sensei Model Insights Framework] O oferecerá suporte a um modelo padrão para cada tipo de algoritmo de aprendizado de máquina. A tabela abaixo mostra classes comuns de algoritmo de aprendizado de máquina de alto nível e as métricas e visualizações de avaliação correspondentes.

| Tipo de algoritmo ML | Métricas de avaliação | Visualizações |
| --- | --- | --- |
| Regressão | - RMSE<br>- MAPE<br>- MASSA<br>- MAE | Curva de sobreposição de valores previstos versus reais |
| Classificação binária | - Matriz de confusão<br>- Recolha de precisão<br>- Precisão<br>- Pontuação F (especificamente F1 ,F2)<br>- AUC<br>- ROC | Curva ROC e matriz de confusão |
| Classificação de várias classes | -Matriz de confusão <br>- Para cada classe: <br>- precisão da recuperação de precisão <br>- Pontuação F (especificamente F1, F2) | Curva ROC e matriz de confusão |
| Agrupamento (c/ verdade fundamental) | - NMI (pontuação normalizada de informação mútua), AMI (pontuação ajustada de informação mútua)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- pontuação de homogeneidade, pontuação de integridade e medida V<br>- FMI (índice Fowlkes-Mallows)<br>- Pureza<br>- Índice Jaccard | Gráfico de clusters mostrando clusters e centroides com tamanhos relativos de cluster que refletem os pontos de dados que estão no cluster |
| Clustering (sem verdade fundamental) | - Inércia<br>- Coeficiente de silhueta<br>- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice de Dunn | Gráfico de clusters mostrando clusters e centroides com tamanhos relativos de cluster que refletem os pontos de dados que estão no cluster |
| Recomendação | -Precisão média (MAP) <br>-Ganho Acumulado Descontado Normalizado <br>-Classificação Recíproca Média <br>-Métrica K | A confirmar |
| Casos de uso do TensorFlow | Análise do modelo TensorFlow (TFMA) | Comparação/visualização do modelo de rede neural Deepcompare |
| Outro/mecanismo de captura de erros | Lógica de métrica personalizada (e gráficos de avaliação correspondentes) definida pelo autor do modelo. Tratamento de erros naturais em caso de incompatibilidade de modelo | Tabela com pares de valores-chave para métricas de avaliação |
