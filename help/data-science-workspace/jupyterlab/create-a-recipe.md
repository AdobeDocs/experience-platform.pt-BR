---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Crie uma receita usando notebooks em Júpiter
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '2292'
ht-degree: 0%

---


# Crie uma receita usando notebooks em Júpiter

Este tutorial percorrerá duas seções principais. Primeiro, você criará um modelo de aprendizado de máquina usando um modelo em [!DNL JupyterLab Notebook]. Em seguida, você exercitará o notebook para obter o fluxo de trabalho da receita dentro [!DNL JupyterLab] para criar uma receita dentro [!DNL Data Science Workspace].

## Conceitos introduzidos:

- **Receitas:** Uma receita é um termo para uma especificação de modelo e um container de nível superior que representa um aprendizado de máquina específico, algoritmo AI ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo e, portanto, ajudar a resolver problemas específicos de negócios.
- **Modelo:** Um modelo é uma instância de uma fórmula de aprendizado de máquina treinada usando dados históricos e configurações para solucionar um caso de uso comercial.
- **Treinamento:** Treinamento é o processo de aprendizado de padrões e insights de dados rotulados.
- **Pontuação:** A pontuação é o processo de gerar insights a partir de dados usando um modelo treinado.

## Introdução ao ambiente [!DNL JupyterLab] notebook

Criar uma receita do zero pode ser feito dentro [!DNL Data Science Workspace]. Para start, navegue até o [Adobe Experience Platform](https://platform.adobe.com) e clique na guia **[!UICONTROL Notebooks]** à esquerda. Crie um novo bloco de anotações selecionando o modelo do Construtor de receitas no [!DNL JupyterLab Launcher].

O notebook [!UICONTROL Recipe Builder] permite que você execute treinamentos e execuções de pontuação dentro do notebook. Isso proporciona a flexibilidade para fazer mudanças em seus métodos `train()` e `score()` métodos entre experiências de execução no treinamento e dados de pontuação. Quando estiver satisfeito com os resultados do treinamento e da pontuação, você poderá criar uma receita para ser usada no [!DNL Data Science Workspace] uso do notebook para obter a funcionalidade integrada ao notebook Construtor de receita.

>[!NOTE]
>
>O notebook Construtor de receita suporta o trabalho com todos os formatos de arquivo, mas atualmente a funcionalidade Criar receita suporta apenas [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe-builder.png)

Quando você clica no notebook do Recipe Builder no lançador, o notebook será aberto na guia. O modelo usado no notebook é a Receita de Previsão de Vendas de Retalho Python, que também pode ser encontrada [neste repositório público](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

Você notará que na barra de ferramentas existem três ações adicionais, a saber: **[!UICONTROL Treinamento]**, **[!UICONTROL Pontuação]** e **[!UICONTROL Criação de Receita]**. Esses ícones só aparecerão no notebook [!UICONTROL Recipe Builder] . Mais informações sobre essas ações serão discutidas [na seção](#training-and-scoring) Treinamento e pontuação depois de criar a Receita no notebook.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Fazer edições em arquivos de receita

Para fazer edições nos arquivos de receita, navegue até a célula em Júpiter correspondente ao caminho do arquivo. Por exemplo, se você deseja fazer alterações em `evaluator.py`, procure por `%%writefile demo-recipe/evaluator.py`.

Start fazendo as alterações necessárias na célula e, quando terminar, simplesmente execute a célula. O `%%writefile filename.py` comando gravará o conteúdo da célula no `filename.py`. Será necessário executar manualmente a célula para cada arquivo com alterações.

>[!NOTE]
>
>Você deve executar as células manualmente quando aplicável.

## Introdução ao notebook Recipe Builder

Agora que você sabe as noções básicas para o ambiente de [!DNL JupyterLab] notebook, você pode começar a olhar para os arquivos que compõem uma receita de modelo de aprendizado de máquina. Os arquivos sobre os quais falaremos são mostrados aqui:

- [Arquivo de requisitos](#requirements-file)
- [Arquivos de configuração](#configuration-files)
- [Carregador de dados de treinamento](#training-data-loader)
- [Carregador de dados de pontuação](#scoring-data-loader)
- [Arquivo Pipeline](#pipeline-file)
- [Arquivo do avaliador](#evaluator-file)
- [Arquivo de Proteção de Dados](#data-saver-file)

### Arquivo de requisitos {#requirements-file}

O arquivo requirements é usado para declarar bibliotecas adicionais que você deseja usar na fórmula. Você pode especificar o número da versão se houver uma dependência. Para procurar bibliotecas adicionais, visite https://anaconda.org. A lista das principais bibliotecas já em uso inclui:

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>As bibliotecas ou versões específicas que você adicionar podem ser incompatíveis com as bibliotecas acima.

### Arquivos de configuração {#configuration-files}

Os arquivos de configuração `training.conf` e `scoring.conf`, são usados para especificar os conjuntos de dados que você deseja usar para treinamento e pontuação, bem como para adicionar hiperparâmetros. Há configurações separadas para treinamento e pontuação.

Os usuários devem preencher as seguintes variáveis antes de executar o treinamento e a pontuação:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Para localizar o conjunto de dados e as IDs de schema, vá para a guia Dados dentro dos notebooks na barra de navegação esquerda (sob o ícone de pasta).

![](../images/jupyterlab/create-recipe/datasets.png)

As mesmas informações podem ser encontradas no [Adobe Experience Platform](https://platform.adobe.com/) nas guias **[Schema](https://platform.adobe.com/schema)** e **[Conjuntos de dados](https://platform.adobe.com/dataset/overview)** .

Por padrão, os seguintes parâmetros de configuração são definidos para você ao acessar os dados:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Carregador de dados de treinamento {#training-data-loader}

A finalidade do Carregador de dados de treinamento é instanciar os dados usados para criar o modelo de aprendizado da máquina. Normalmente, há duas tarefas que o carregador de dados de treinamento realizará:
- Carregar dados de [!DNL Platform]
- Preparação de dados e engenharia de recursos

As duas seções a seguir abordarão o carregamento de dados e a preparação de dados.

### Carregando dados {#loading-data}

Esta etapa usa os dados [pandas](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Os dados podem ser carregados de arquivos no [!DNL Adobe Experience Platform] SDK ( [!DNL Platform] SDK) ou de fontes externas usando as funções dos pandas`platform_sdk`ou `read_csv()` `read_json()` .

- [!DNL Platform SDK](#platform-sdk)
- [Fontes externas](#external-sources)

>[!NOTE]
>
>No notebook do Recipe Builder, os dados são carregados pelo carregador de `platform_sdk` dados.

### [!DNL Platform] SDK {#platform-sdk}

Para obter um tutorial detalhado sobre como usar o carregador de `platform_sdk` dados, visite o guia [do SDK da](../authoring/platform-sdk.md)plataforma. Este tutorial fornece informações sobre autenticação de compilação, leitura básica de dados e escrita básica de dados.

### Fontes externas {#external-sources}

Esta seção mostra como importar um arquivo JSON ou CSV para um objeto de pandas. A documentação oficial da biblioteca de pandas pode ser encontrada aqui:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Primeiro, veja um exemplo de importação de um arquivo CSV. O `data` argumento é o caminho para o arquivo CSV. Essa variável foi importada do `configProperties` na seção [](#configuration-files)anterior.

```PYTHON
df = pd.read_csv(data)
```

Também é possível importar de um arquivo JSON. O `data` argumento é o caminho para o arquivo CSV. Essa variável foi importada do `configProperties` na seção [](#configuration-files)anterior.

```PYTHON
df = pd.read_json(data)
```

Agora seus dados estão no objeto dataframe e podem ser analisados e manipulados na [próxima seção](#data-preparation-and-feature-engineering).

### Do SDK de acesso a dados (obsoleto)

>[!CAUTION]
>
> `data_access_sdk_python` não é mais recomendado, consulte [Converter código de acesso a dados para SDK](../authoring/platform-sdk.md) da plataforma para obter um guia sobre como usar o carregador de `platform_sdk` dados.

Os usuários podem carregar dados usando o SDK de acesso a dados. A biblioteca pode ser importada na parte superior da página, incluindo a linha:

`from data_access_sdk_python.reader import DataSetReader`

Em seguida, usamos o `load()` método para capturar o conjunto de dados de treinamento do `trainingDataSetId` como definido em nosso arquivo de configuração (`recipe.conf`).

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE]
>
>Conforme mencionado na seção [Arquivo de](#configuration-files)configuração, os seguintes parâmetros de configuração são definidos para você ao acessar os dados de [!DNL Experience Platform]:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Agora que você tem seus dados, você pode começar com preparação de dados e engenharia de recursos.

### Preparação de dados e engenharia de recursos {#data-preparation-and-feature-engineering}

Depois que os dados são carregados, os dados sofrem preparação e são divididos nos conjuntos de dados `train` e `val` . O código de amostra é visto abaixo:

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

Neste exemplo, há cinco coisas sendo feitas no conjunto de dados original:
- adicionar `week` e `year` colunas
- converter `storeType` em uma variável de indicador
- converter `isHoliday` em uma variável numérica
- compensação `weeklySales` para obter valor de vendas futuras e passadas
- dividir dados, por data, em `train` e `val` conjunto de dados

Primeiro, `week` e as `year` colunas são criadas e a `date` coluna original é convertida em [!DNL Python] datetime [](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). Os valores de semana e ano são extraídos do objeto datetime.

Em seguida, `storeType` é convertido em três colunas que representam os três tipos diferentes de armazenamento (`A`, `B`e `C`). Cada um conterá um valor booliano para indicar o que `storeType` é verdadeiro. A `storeType` coluna será solta.

Da mesma forma, `weeklySales` altera o `isHoliday` booliano para uma representação numérica, um ou zero.

Esses dados são divididos entre `train` e o conjunto de dados `val` .

A `load()` função deve ser concluída com o conjunto de dados `train` e `val` como saída.

### Carregador de dados de pontuação {#scoring-data-loader}

O procedimento para carregar dados de pontuação é semelhante aos dados de treinamento de carregamento na `split()` função. Usamos o SDK de acesso a dados para carregar dados do `scoringDataSetId` encontrado em nosso `recipe.conf` arquivo.

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

Após carregar os dados, a preparação de dados e a engenharia de recursos são feitas.

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

Como o objetivo do nosso modelo é prever vendas semanais futuras, será necessário criar um conjunto de dados de pontuação usado para avaliar o desempenho da previsão do modelo.

Este notebook do Recipe Builder faz isso compensando nossas vendas semanais daqui a 7 dias. Observe que existem medidas para 45 armazenamentos todas as semanas para que você possa direcionar os `weeklySales` valores para 45 conjuntos de dados para frente em uma nova coluna chamada `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Da mesma forma, é possível criar uma coluna `weeklySalesLag` alterando 45 para trás. Com isso, também é possível calcular a diferença nas vendas semanais e armazená-las na coluna `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Como você está desconfigurando os conjuntos de dados 45 para frente e 45 para trás para criar novas colunas, o primeiro e o último 45 pontos de dados terão valores NaN. `weeklySales` Você pode remover esses pontos do nosso conjunto de dados usando a `df.dropna()` função que remove todas as linhas que têm valores NaN.

```PYTHON
df.dropna(0, inplace=True)
```

A `load()` função no carregador de dados de pontuação deve ser concluída com o conjunto de dados de pontuação como saída.

### Arquivo Pipeline {#pipeline-file}

O `pipeline.py` arquivo inclui lógica para treinamento e pontuação.

### Treinamento {#training}

O objetivo do treinamento é criar um modelo usando recursos e etiquetas no conjunto de dados de treinamento.

>[!NOTE]
> 
>_Os recursos_ se referem à variável de entrada usada pelo modelo de aprendizado da máquina para prever os _rótulos_.

A `train()` função deve incluir o modelo de treinamento e devolver o modelo treinado. Alguns exemplos de diferentes modelos podem ser encontrados na documentação [do guia do usuário](https://scikit-learn.org/stable/user_guide.html)scikit-learn.

Após escolher o modelo de treinamento, você ajustará o conjunto de dados de treinamento x e y ao modelo e a função retornará o modelo treinado. Um exemplo que mostra isso é o seguinte:

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

Observe que, dependendo de seu aplicativo, você terá argumentos em sua `GradientBoostingRegressor()` função. `xTrainingDataset` deve conter seus recursos usados para treinamento e `yTrainingDataset` conter suas etiquetas.

### Pontuação {#scoring}

A `score()` função deve conter o algoritmo de pontuação e retornar uma medida para indicar o sucesso do modelo. A `score()` função usa os rótulos de conjunto de dados de pontuação e o modelo treinado para gerar um conjunto de recursos previstos. Esses valores previstos são comparados aos recursos reais no conjunto de dados de pontuação. Neste exemplo, a `score()` função usa o modelo treinado para prever recursos usando os rótulos do conjunto de dados de pontuação. Os recursos previstos são retornados.

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### Arquivo do avaliador {#evaluator-file}

O `evaluator.py` arquivo contém uma lógica para avaliar sua fórmula treinada, bem como como seus dados de treinamento devem ser divididos. No exemplo de vendas de varejo, a lógica para carregar e preparar os dados de treinamento será incluída. Iremos analisar as duas seções que se seguem.

### Dividir o conjunto de dados {#split-the-dataset}

A fase de preparação de dados para treinamento requer a divisão do conjunto de dados a ser usado para treinamento e teste. Esses `val` dados serão usados implicitamente para avaliar o modelo depois que ele for treinado. Esse processo é separado da pontuação.

Esta seção mostrará a `split()` função que primeiro carregará dados no bloco de anotações e, em seguida, limpará os dados removendo colunas não relacionadas no conjunto de dados. A partir daí, você poderá executar a engenharia de recursos, que é o processo para criar recursos relevantes adicionais a partir dos recursos brutos existentes nos dados. Um exemplo desse processo pode ser visto abaixo, juntamente com uma explicação.

A `split()` função é mostrada abaixo. Os dados fornecidos no argumento serão divididos nas variáveis `train` e `val` a serem retornadas.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### Avaliar o modelo treinado {#evaluate-the-trained-model}

A `evaluate()` função é executada após o modelo ser treinado e retornará uma métrica para indicar o sucesso do modelo. A `evaluate()` função usa as etiquetas do conjunto de dados de teste e o modelo Treinado para prever um conjunto de recursos. Esses valores previstos são comparados aos recursos reais no conjunto de dados de teste. Algoritmos de pontuação comuns incluem:
- [Erro percentual médio absoluto (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Erro absoluto médio (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Erro quadrado médio raiz (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


A `evaluate()` função na amostra de vendas a retalho é mostrada abaixo:

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

Observe que a função retorna um `metric` objeto que contém uma matriz de métricas de avaliação. Essas métricas serão usadas para avaliar o desempenho do modelo treinado.

### Arquivo de Proteção de Dados {#data-saver-file}

O `datasaver.py` arquivo contém a `save()` função de salvar sua previsão ao testar a pontuação. A `save()` função usará sua previsão e [!DNL Experience Platform Catalog] as APIs, gravará os dados no `scoringResultsDataSetId` que você especificou no seu `scoring.conf` arquivo.

O exemplo usado na receita de amostra de vendas para venda a varejo é visto aqui. Observe o uso da `DataSetWriter` biblioteca para gravar dados na Plataforma:

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## Treinamento e pontuação {#training-and-scoring}

Quando terminar de fazer alterações no seu notebook e quiser treinar sua receita, clique nos botões associados na parte superior da barra para criar uma execução de treinamento na célula. Ao clicar no botão, um registro de comandos e saídas do script de treinamento aparecerá no bloco de anotações (sob a `evaluator.py` célula). Primeiro, o Conda instala todas as dependências e, em seguida, o treinamento é iniciado.

Observe que você deve executar o treinamento pelo menos uma vez antes de executar a pontuação. Clicar no botão **[!UICONTROL Executar pontuação]** pontuará no modelo treinado que foi gerado durante o treinamento. O script de pontuação será exibido em `datasaver.py`.

Para fins de depuração, se você quiser ver a saída oculta, adicione `debug` ao final da célula de saída e execute-a novamente.

## Criar fórmula {#create-recipe}

Quando terminar de editar a receita e estiver satisfeito com a saída de treinamento/pontuação, você poderá criar uma receita do notebook pressionando **[!UICONTROL Criar receita]** na navegação superior direita.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Depois de pressionar o botão, você será solicitado a inserir um nome de fórmula. Esse nome representa a receita real criada em [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Depois de pressionar **[!UICONTROL Ok]** , você poderá navegar até a nova fórmula no [Adobe Experience Platform](https://platform.adobe.com/). Você pode clicar no botão Receitas **[!UICONTROL de]** Visualização para levar você até a guia **[!UICONTROL Receitas]** em Modelos **[!UICONTROL ML]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Quando o processo estiver concluído, a receita ficará parecida com isso:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
> - Não excluir nenhuma das células de arquivo
> - Não edite a `%%writefile` linha na parte superior das células do arquivo
> - Não crie receitas em diferentes blocos de anotações ao mesmo tempo


## Próximas etapas {#next-steps}

Ao concluir este tutorial, você aprendeu a criar um modelo de aprendizado de máquina no notebook Construtor de receitas. Você também aprendeu a exercitar o notebook para obter o fluxo de trabalho da receita dentro do notebook para criar uma receita dentro do notebook [!DNL Data Science Workspace].

Para continuar aprendendo como trabalhar com recursos dentro [!DNL Data Science Workspace], visite a lista suspensa [!DNL Data Science Workspace] receitas e modelos.

## Recursos adicionais {#additional-resources}

O vídeo a seguir foi projetado para oferecer suporte à sua compreensão sobre a criação e implantação de modelos.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


