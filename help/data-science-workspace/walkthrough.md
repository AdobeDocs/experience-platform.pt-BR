---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Apresentação da Data Science Workspace
topic: Walkthrough
description: Este documento fornece uma apresentação para a Adobe Experience Platform Data Science Workspace. Especificamente o fluxo de trabalho geral que um cientista de dados passaria para resolver um problema usando o aprendizado de máquina.
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---


# [!DNL Data Science Workspace] passagem

Este documento fornece uma apresentação para o Adobe Experience Platform [!DNL Data Science Workspace]. Especificamente vamos passar pelo fluxo de trabalho geral que um cientista de dados passaria para resolver um problema usando o aprendizado de máquina.

## Pré-requisitos

- Uma conta Adobe ID registrada
   - A conta da Adobe ID deve ter sido adicionada a uma organização com acesso ao Adobe Experience Platform e ao [!DNL Data Science Workspace]

## Motivação do cientista da informação

Um varejista enfrenta muitos desafios para se manter competitivo no mercado atual. Uma das principais preocupações do retalhista é decidir sobre o preço ótimo dos seus produtos e prever as tendências de venda. Com um modelo preciso de previsão, o varejista poderia encontrar a relação entre as políticas de demanda e de preços e tomar decisões otimizadas de preços para maximizar as vendas e a receita.

## Solução do cientista em dados

A solução de um cientista de dados é aproveitar a riqueza de dados históricos a que um varejista tem acesso, prever tendências futuras e otimizar as decisões de preços. Usaremos dados de vendas passadas para treinar nosso modelo de aprendizado de máquina e usar o modelo para prever tendências futuras de venda. Com isso, o varejista poderá ter insights para ajudá-lo a fazer mudanças nos preços.

Nesta visão geral, vamos passar pelos passos que um cientista de dados passaria para pegar um conjunto de dados e criar um modelo para prever vendas semanais. Iremos para as seguintes seções no Notebook de amostra de vendas de varejo no Adobe Experience Platform [!DNL Data Science Workspace]:

- [Configuração](#setup)
- [Como explorar dados](#exploring-data)
- [Engenharia de recursos](#feature-engineering)
- [Treinamento e verificação](#training-and-verification)

### Notebooks em [!DNL Data Science Workspace]

Primeiro, queremos criar um [!DNL JupyterLab] notebook para abrir a amostra de notebook &quot;Vendas de varejo&quot;. Seguir as etapas feitas pelo cientista de dados no notebook nos permitirá compreender um fluxo de trabalho típico.

Na interface do usuário do Adobe Experience Platform, clique na guia Data Science no menu superior para levá-lo ao [!DNL Data Science Workspace]. Nesta página, clique na [!DNL JupyterLab] guia que abrirá o [!DNL JupyterLab] iniciador. Você deve ver uma página semelhante a esta.

![](./images/walkthrough/jupyterlab_launcher.png)

Em nosso tutorial, usaremos o [!DNL Python] 3 no [!DNL Jupyter Notebook] para mostrar como acessar e explorar os dados. Na página Iniciador, há exemplos de notebooks fornecidos. Usaremos a amostra &quot;Vendas a varejo&quot; para [!DNL Python] 3.

![](./images/walkthrough/retail_sales.png)

### Configuração {#setup}

Com o notebook de vendas de varejo aberto, a primeira coisa que fazemos é carregar as bibliotecas necessárias para nosso fluxo de trabalho. A lista a seguir fornecerá uma breve descrição do uso de cada uma delas:
- **número** - biblioteca de computação científica que adiciona suporte para matrizes e matrizes grandes e multidimensionais
- **pandas** - biblioteca que oferta as estruturas e operações de dados usadas para manipulação e análise de dados
- **matplotlib.pypload** - biblioteca de plotamento que fornece uma experiência semelhante a MATLAB ao plotar
- **seaborn** - biblioteca de visualização de dados de interface de alto nível com base em matplotlib
- **sklearn** - biblioteca de aprendizado de máquina que apresenta classificação, regressão, vetor de suporte e algoritmos de cluster
- **avisos** - biblioteca que controla as mensagens de aviso

### Explorar dados {#exploring-data}

#### Carregar dados

Depois que as bibliotecas são carregadas, podemos start a olhar para os dados. O [!DNL Python] código a seguir usa a estrutura `DataFrame` de dados dos pandas e a função [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para ler o CSV hospedado [!DNL Github] nos pandas DataFrame:

![](./images/walkthrough/read_csv.png)

A estrutura de dados DataFrame dos painéis é uma estrutura de dados bidimensional identificada. Para ver rapidamente as dimensões dos nossos dados, podemos usar `df.shape`. Isso retorna uma tupla que representa a dimensionalidade do DataFrame:

![](./images/walkthrough/df_shape.png)

Finalmente, podemos dar uma olhada em como são os nossos dados. Podemos usar `df.head(n)` para visualização das primeiras `n` linhas do DataFrame:

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

Com isso, podemos ver que existem 6.435 instâncias para cada característica. Além disso, são fornecidas informações estatísticas como média, desvio padrão (std), mín., máx. e interquartis. Isso nos fornece informações sobre o desvio dos dados. Na próxima seção, nós iremos ver a visualização que funciona junto com essa informação para nos dar uma compreensão completa de nossos dados.

Analisando os valores mínimo e máximo para `store`, podemos ver que existem 45 armazenamentos exclusivos que os dados representam. Há também `storeTypes` que diferenciam o que é uma loja. Podemos ver a distribuição do `storeTypes` ao fazer o seguinte:

![](./images/walkthrough/df_groupby.png)

Isso significa que 22 lojas são de `storeType A` , 17 são `storeType B`e 6 são `storeType C`.

#### Visualizar dados

Agora que conhecemos nossos valores de quadro de dados, queremos complementá-los com visualizações para tornar as coisas mais claras e fáceis de identificar padrões. Esses gráficos também são úteis ao transmitir resultados a uma audiência.

#### Gráficos de variação única

Gráficos de variação única são gráficos de uma variável individual. Um gráfico univariado comum usado para visualizar seus dados são gráficos de caixa e de uísque.

Usando nosso conjunto de dados de varejo de antes, podemos gerar a caixa e o gráfico de uísque para cada uma das 45 lojas e suas vendas semanais. O gráfico é gerado usando a `seaborn.boxplot` função.

![](./images/walkthrough/box_whisker.png)

Um gráfico de caixa e uísque é usado para mostrar a distribuição de dados. As linhas exteriores da parcela mostram os quartis superior e inferior enquanto a caixa se estende pelo intervalo interquartil. A linha na caixa marca a mediana. Quaisquer pontos de dados mais de 1,5 vezes o quartil superior ou inferior são marcados como um círculo. Estes pontos são considerados exceções.

Em seguida, podemos traçar as vendas semanais com o tempo. Só mostraremos a saída da primeira loja. O código no notebook gera 6 lotes correspondentes a 6 das 45 lojas em nosso conjunto de dados.

![](./images/walkthrough/weekly_sales.png)

Com este diagrama, podemos comparar as vendas semanais ao longo de um período de 2 anos. É fácil ver os picos de venda e padrões mínimos ao longo do tempo.

#### Gráficos multivariados

Os gráficos multivariados são usados para ver a interação entre variáveis. Com a visualização, os cientistas de dados podem ver se há correlações ou padrões entre as variáveis. Um gráfico multivariado comum usado é uma matriz de correlação. Com uma matriz de correlação, as dependências entre várias variáveis são quantificadas com o coeficiente de correlação.

Usando o mesmo conjunto de dados de varejo, podemos gerar a matriz de correlação.

![](./images/walkthrough/correlation_1.png)

Observe a diagonal dos que estão no centro. Isso mostra que ao comparar uma variável com ela mesma, ela tem uma correlação positiva completa. Uma forte correlação positiva terá uma magnitude mais próxima de 1, enquanto correlações fracas estarão mais próximas de 0. A correlação negativa é mostrada com um coeficiente negativo que mostra uma tendência inversa.

### Engenharia de recursos {#feature-engineering}

Nesta seção, faremos modificações em nosso conjunto de dados de varejo. Executaremos as seguintes operações:

- adicionar colunas de semana e ano
- converter storeType em uma variável de indicador
- converter isHoliday em uma variável numérica
- prever semanalmenteVendas da próxima semana

#### Adicionar colunas de semana e ano

O formato atual para a data (`2010-02-05`) é difícil diferenciar que os dados sejam para cada semana. Por isso, convertemos a data para semana e ano.

![](./images/walkthrough/date_to_week_year.png)

Agora, a semana e a data são as seguintes:

![](./images/walkthrough/date_week_year.png)

#### Converter storeType em variável de indicador

Em seguida, queremos converter a coluna storeType em colunas representando cada uma `storeType`. Há 3 tipos de armazenamento (`A`, `B`, `C`), a partir dos quais estamos criando 3 novas colunas. O valor definido em cada será um valor booliano no qual um &quot;1&quot; será definido dependendo do que `storeType` foi e `0` das outras 2 colunas.

![](./images/walkthrough/storeType.png)

A `storeType` coluna atual será ignorada.

#### Converter isHoliday em tipo numérico

A próxima modificação é transformar o `isHoliday` booliano em uma representação numérica.

![](./images/walkthrough/isHoliday.png)


#### Prever vendas semanais da próxima semana

Agora queremos adicionar vendas semanais anteriores e futuras a cada um de nossos conjuntos de dados. Estamos a fazê-lo compensando a nossa `weeklySales`situação. Além disso, estamos calculando a `weeklySales` diferença. Isso é feito subtraindo `weeklySales` com a semana anterior `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

Como estamos deslocando os `weeklySales` dados 45 conjuntos de dados para frente e 45 conjuntos de dados para trás para criar novas colunas, o primeiro e o último 45 pontos de dados terão valores NaN. Podemos remover esses pontos de nosso conjunto de dados usando a `df.dropna()` função que remove todas as linhas que têm valores NaN.

![](./images/walkthrough/dropna.png)

Um resumo do conjunto de dados após nossas modificações é mostrado abaixo:

![](./images/walkthrough/df_info_new.png)

### Formação e verificação {#training-and-verification}

Agora, é hora de criar alguns modelos de dados e selecionar qual modelo é o melhor desempenho para prever vendas futuras. Avaliaremos os cinco algoritmos a seguir:

- Regressão Linear
- Árvore de decisão
- Floresta Aleatória
- Aumento de gradiente
- K Vizinhos

#### Dividir conjunto de dados em subconjuntos de treinamento e teste

Precisamos de uma forma de saber quão preciso o nosso modelo será capaz de prever valores. Essa avaliação pode ser feita alocando parte do conjunto de dados para ser usado como validação e o restante como dados de treinamento. Como `weeklySalesAhead` são os valores futuros reais de `weeklySales`, podemos usar isso para avaliar a precisão do modelo em prever o valor. A divisão é feita abaixo:

![](./images/walkthrough/split_data.png)

Temos agora `X_train` e `y_train` para preparar os modelos `X_test` e `y_test` para avaliação mais tarde.

#### Algoritmos de verificação de manchas

Nesta seção, declararemos todos os algoritmos em um array chamado `model`. Em seguida, nós iteramos por esse storage e, para cada algoritmo, inserimos nossos dados de treinamento com os `model.fit()` quais um modelo é criado `mdl`. Usando este modelo, nós vamos prever `weeklySalesAhead` com nossos `X_test` dados.

![](./images/walkthrough/training_scoring.png)

Para a pontuação, estamos pegando a diferença percentual média entre os valores previstos `weeklySalesAhead` e reais nos `y_test` dados. Como queremos minimizar a diferença entre nossa previsão e a real, o Gradient Boosting Regressor é o modelo de melhor desempenho.

#### Visualizar previsões

Finalmente, visualizaremos nosso modelo de previsão com os valores reais de vendas semanais. A linha azul representa os números reais, enquanto o verde representa nossa previsão usando o Gradient Boosting. O código a seguir gera 6 lotes que representam 6 dos 45 armazenamentos em nosso conjunto de dados. Somente `Store 1` é mostrado aqui:

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## Conclusão 

Com essa visão geral, passamos pelo fluxo de trabalho que um cientista de dados passaria para resolver um problema de vendas no varejo. Especificamente, passamos pelos passos a seguir para chegar a uma solução que prevê vendas semanais futuras.

- [Configuração](#setup)
- [Como explorar dados](#exploring-data)
- [Engenharia de recursos](#feature-engineering)
- [Treinamento e verificação](#training-and-verification)