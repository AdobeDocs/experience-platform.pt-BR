---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Apresentação da Data Science Workspace
topic: Walkthrough
description: Este documento fornece uma apresentação para a Adobe Experience Platform Data Science Workspace. Especificamente o fluxo de trabalho geral que um cientista de dados passaria para resolver um problema usando o aprendizado de máquina.
translation-type: tm+mt
source-git-commit: 0d76b14599bc6b6089f9c760ef6a6be3a19243d4
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 0%

---


# [!DNL Data Science Workspace] passagem

Este documento fornece uma apresentação para o Adobe Experience Platform [!DNL Data Science Workspace]. Este tutorial descreve um fluxo de trabalho geral do cientista de dados e como eles podem abordar e resolver um problema usando o aprendizado da máquina.

## Pré-requisitos

- Uma conta Adobe ID registrada
   - A conta Adobe ID deve ter sido adicionada a uma organização com acesso ao Adobe Experience Platform e [!DNL Data Science Workspace].

## Caso de uso de varejo

Um varejista enfrenta muitos desafios para se manter competitivo no mercado atual. Uma das principais preocupações do retalhista é decidir sobre o preço ótimo de um produto e prever as tendências de venda. Com um modelo de previsão preciso, um varejista poderia encontrar a relação entre as políticas de demanda e preços e tomar decisões otimizadas de preços para maximizar as vendas e a receita.

## Solução do cientista em dados

A solução de um cientista de dados é aproveitar a riqueza de informações históricas fornecidas por um varejista, prever tendências futuras e otimizar as decisões de preços. Esta apresentação usa dados de vendas passadas para treinar um modelo de aprendizado de máquina e usa o modelo para prever tendências futuras de venda. Com isso, você pode gerar insights para ajudar a fazer alterações ideais nos preços.

Esta visão geral reflete os passos que um cientista de dados iria seguir para pegar um conjunto de dados e criar um modelo para prever vendas semanais. Este tutorial aborda as seguintes seções no Notebook de amostra de vendas a varejo no Adobe Experience Platform [!DNL Data Science Workspace]:

- [Configuração](#setup)
- [Como explorar dados](#exploring-data)
- [Engenharia de recursos](#feature-engineering)
- [Treinamento e verificação](#training-and-verification)

### Notebooks em [!DNL Data Science Workspace]

Na interface do usuário do Adobe Experience Platform, selecione **[!UICONTROL Notebooks]** na guia **[!UICONTROL Data Science]** para trazê-lo à página de visão geral [!UICONTROL Notebooks] . Nesta página, selecione a [!DNL JupyterLab] guia para iniciar seu [!DNL JupyterLab] ambiente. A landing page padrão para [!DNL JupyterLab] é o **[!UICONTROL Iniciador]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

Este tutorial usa [!DNL Python] 3 em [!DNL JupyterLab Notebooks] para mostrar como acessar e explorar os dados. Na página Iniciador, há exemplos de notebooks fornecidos. O notebook de amostra **[!UICONTROL de vendas]** de varejo é usado nos exemplos fornecidos abaixo.

### Configuração {#setup}

Com o notebook de vendas de varejo aberto, a primeira coisa que você deve fazer é carregar as bibliotecas necessárias para o seu fluxo de trabalho. A lista a seguir fornece uma breve descrição para cada uma das bibliotecas usadas nos exemplos em etapas posteriores.

- **número**: Biblioteca de computação científica que adiciona suporte para matrizes e matrizes grandes e multidimensionais
- **pandas**: Biblioteca que oferta as estruturas e operações de dados usadas para manipulação e análise de dados
- **matplotlib.pypload**: Biblioteca de plotagem que fornece uma experiência semelhante ao MATLAB ao plotar
- **seaborn** : Biblioteca de visualização de dados de interface de alto nível com base em matplotlib
- **sklearn**: Biblioteca de aprendizado de máquina que apresenta classificação, regressão, vetor de suporte e algoritmos de cluster
- **avisos**: Biblioteca que controla as mensagens de aviso

### Pagamentos {#exploring-data}

#### Carregar dados

Depois que as bibliotecas são carregadas, você pode start observando os dados. O [!DNL Python] código a seguir usa a estrutura `DataFrame` de dados dos pandas e a função [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para ler o CSV hospedado [!DNL Github] nos pandas DataFrame:

![](./images/walkthrough/read_csv.png)

A estrutura de dados DataFrame dos painéis é uma estrutura de dados bidimensional identificada. Para ver rapidamente as dimensões dos seus dados, você pode usar `df.shape`. Isso retorna uma tupla que representa a dimensionalidade do DataFrame:

![](./images/walkthrough/df_shape.png)

Finalmente, você pode pré-visualização como seus dados se parecem. Você pode usar `df.head(n)` para visualização das primeiras `n` linhas do DataFrame:

![](./images/walkthrough/df_head.png)

#### Resumo estatístico

Podemos aproveitar a biblioteca de [!DNL Python's] pandas para obter o tipo de dados de cada atributo. A saída da chamada a seguir nos fornecerá informações sobre o número de entradas e o tipo de dados para cada uma das colunas:

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Essas informações são úteis, pois conhecer o tipo de dados para cada coluna permitirá que saibamos como tratar os dados.

Agora vamos olhar para o resumo estatístico. Somente os tipos de dados numéricos serão exibidos `date`, `storeType`e não `isHoliday` serão enviados:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Com isso, você pode ver que existem 6.435 instâncias para cada característica. Além disso, são fornecidas informações estatísticas como média, desvio padrão (std), mín., máx. e interquartis. Isso nos fornece informações sobre o desvio dos dados. Na próxima seção, você vai visualizar o que funciona junto com essas informações para nos dar uma compreensão completa dos seus dados.

Analisando os valores mínimo e máximo para `store`, você pode ver que existem 45 armazenamentos exclusivos que os dados representam. Há também `storeTypes` que diferenciam o que é uma loja. você pode ver a distribuição do `storeTypes` ao fazer o seguinte:

![](./images/walkthrough/df_groupby.png)

Isso significa que 22 lojas são de `storeType A` , 17 são `storeType B`e 6 são `storeType C`.

#### Visualizar dados

Agora que você sabe seus valores de quadro de dados, você quer complementá-los com visualizações para tornar as coisas mais claras e fáceis de identificar padrões. Esses gráficos também são úteis ao transmitir resultados a uma audiência.

#### Gráficos de variação única

Gráficos de variação única são gráficos de uma variável individual. Um gráfico univariado comum usado para visualizar seus dados são gráficos de caixa e de uísque.

Usando seu conjunto de dados de varejo de antes, você pode gerar a caixa e o gráfico de uísque para cada uma das 45 lojas e suas vendas semanais. O gráfico é gerado usando a `seaborn.boxplot` função.

![](./images/walkthrough/box_whisker.png)

Um gráfico de caixa e uísque é usado para mostrar a distribuição de dados. As linhas exteriores da parcela mostram os quartis superior e inferior enquanto a caixa se estende pelo intervalo interquartil. A linha na caixa marca a mediana. Quaisquer pontos de dados mais de 1,5 vezes o quartil superior ou inferior são marcados como um círculo. Estes pontos são considerados exceções.

Em seguida, você pode traçar as vendas semanais com o tempo. Você só mostrará a saída da primeira loja. O código no notebook gera 6 lotes correspondentes a 6 das 45 lojas em nosso conjunto de dados.

![](./images/walkthrough/weekly_sales.png)

Com este diagrama, você pode comparar as vendas semanais durante um período de 2 anos. É fácil ver os picos de venda e padrões mínimos ao longo do tempo.

#### Gráficos multivariados

Os gráficos multivariados são usados para ver a interação entre variáveis. Com a visualização, os cientistas de dados podem ver se há correlações ou padrões entre as variáveis. Um gráfico multivariado comum usado é uma matriz de correlação. Com uma matriz de correlação, as dependências entre várias variáveis são quantificadas com o coeficiente de correlação.

Usando o mesmo conjunto de dados de varejo, você pode gerar a matriz de correlação.

![](./images/walkthrough/correlation_1.png)

Observe a diagonal dos que estão no centro. Isso mostra que ao comparar uma variável com ela mesma, ela tem uma correlação positiva completa. Uma forte correlação positiva terá uma magnitude mais próxima de 1, enquanto correlações fracas estarão mais próximas de 0. A correlação negativa é mostrada com um coeficiente negativo que mostra uma tendência inversa.

### Engenharia de recursos {#feature-engineering}

Nesta seção, a engenharia de recursos é usada para fazer modificações no seu conjunto de dados Varejo, executando as seguintes operações:

- Adicionar colunas de semana e ano
- Converter storeType em uma variável de indicador
- Converter isHoliday em uma variável numérica
- Prever vendas semanais da próxima semana

#### Adicionar colunas de semana e ano

O formato atual para a data (`2010-02-05`) pode dificultar a diferenciação dos dados para cada semana. Por isso, você deve converter a data para conter semana e ano.

![](./images/walkthrough/date_to_week_year.png)

Agora, a semana e a data são as seguintes:

![](./images/walkthrough/date_week_year.png)

#### Converter storeType em variável de indicador

Em seguida, converta a coluna storeType em colunas representando cada uma `storeType`. Há três tipos de armazenamento (`A`, `B`, `C`), a partir dos quais você está criando três novas colunas. O valor definido em cada é um valor booliano no qual um &quot;1&quot; é definido dependendo do que `storeType` era e `0` das outras 2 colunas.

![](./images/walkthrough/storeType.png)

A `storeType` coluna atual é solta.

#### Converter isHoliday em tipo numérico

A próxima modificação é transformar o `isHoliday` booliano em uma representação numérica.

![](./images/walkthrough/isHoliday.png)

#### Prever vendas semanais da próxima semana

Agora você deseja adicionar vendas semanais anteriores e futuras a cada um dos seus conjuntos de dados. Você pode fazer isso compensando o seu `weeklySales`. Além disso, a `weeklySales` diferença é calculada. Isso é feito subtraindo `weeklySales` com a semana anterior `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

Como você está compensando os conjuntos de dados 45 para frente e 45 para trás para criar novas colunas, o primeiro e o último 45 pontos de dados têm valores NaN. `weeklySales` É possível remover esses pontos do conjunto de dados usando a `df.dropna()` função que remove todas as linhas que têm valores NaN.

![](./images/walkthrough/dropna.png)

Um resumo do conjunto de dados após suas modificações é mostrado abaixo:

![](./images/walkthrough/df_info_new.png)

### Formação e verificação {#training-and-verification}

Agora, é hora de criar alguns modelos de dados e selecionar qual modelo é o melhor desempenho para prever vendas futuras. Você avaliará os 5 algoritmos a seguir:

- Regressão Linear
- Árvore de decisão
- Floresta Aleatória
- Aumento de gradiente
- K Vizinhos

#### Dividir conjunto de dados em subconjuntos de treinamento e teste

Você precisa de uma maneira de saber quão preciso seu modelo será capaz de prever valores. Essa avaliação pode ser feita alocando parte do conjunto de dados para ser usado como validação e o restante como dados de treinamento. Como `weeklySalesAhead` são os valores futuros reais de `weeklySales`, você pode usar isso para avaliar a precisão do modelo na previsão do valor. A divisão é feita abaixo:

![](./images/walkthrough/split_data.png)

Agora você tem `X_train` e `y_train` para preparar os modelos e `X_test` e `y_test` para avaliação mais tarde.

#### Algoritmos de verificação de manchas

Nesta seção, você declara todos os algoritmos em uma matriz chamada `model`. Em seguida, você repete por esse storage e, para cada algoritmo, insira seus dados de treinamento com os `model.fit()` quais cria um modelo `mdl`. Usando este modelo, você pode prever `weeklySalesAhead` com seus `X_test` dados.

![](./images/walkthrough/training_scoring.png)

Para a pontuação, você está assumindo a diferença percentual média entre os valores previstos `weeklySalesAhead` e reais nos `y_test` dados. Como você deseja minimizar a diferença entre sua previsão e o resultado real, o Gradient Boosting Regressor é o modelo de melhor desempenho.

#### Visualizar previsões

Por fim, você visualiza seu modelo de previsão com os valores reais de vendas semanais. A linha azul representa os números reais, enquanto o verde representa sua previsão usando o acréscimo de gradiente. O código a seguir gera 6 parcelas que representam 6 dos 45 armazenamentos em seu conjunto de dados. Somente `Store 1` é mostrado aqui:

![](./images/walkthrough/visualize_prediction.png)

## Próximas etapas

Este documento cobriu um fluxo de trabalho geral de cientista de dados para resolver um problema de vendas de varejo. Para resumir:

- Carregue as bibliotecas necessárias para seu fluxo de trabalho.
- Depois que as bibliotecas forem carregadas, você poderá start a análise dos dados usando resumos estatísticos, visualizações e gráficos.
- Em seguida, a engenharia de recursos é usada para fazer modificações no seu conjunto de dados de varejo.
- Por fim, crie modelos de dados e selecione qual modelo é o melhor desempenho para prever vendas futuras.

Quando estiver pronto, leia o guia [do usuário do](./jupyterlab/overview.md) JupyterLab para obter uma rápida visão geral dos notebooks na Adobe Experience Platform Data Science Workspace. Além disso, se você estiver interessado em aprender sobre Modelos e receitas, leia o schema de vendas de [varejo e o tutorial de conjunto de dados](./models-recipes/create-retails-sales-dataset.md) . Este tutorial o prepara para tutoriais subsequentes da Data Science Workspace que podem ser exibidos na página [de](../tutorials/data-science-workspace.md)tutoriais da Data Science Workspace.