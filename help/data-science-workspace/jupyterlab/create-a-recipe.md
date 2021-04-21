---
keywords: Experience Platform; JupyterLab; fórmula; blocos de anotações; Data Science Workspace; tópicos populares; criar fórmula
solution: Experience Platform
title: Criar uma receita usando notebooks Júpiter
topic-legacy: tutorial
type: Tutorial
description: Este tutorial percorrerá duas seções principais. Primeiro, você criará um modelo de aprendizado de máquina usando um modelo no Notebook JupyterLab. Em seguida, você exercerá o fluxo de trabalho do notebook para receber receita no JupyterLab para criar uma receita no Data Science Workspace.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# Criar uma receita usando notebooks Júpiter

Este tutorial percorrerá duas seções principais. Primeiro, você criará um modelo de aprendizado de máquina usando um modelo em [!DNL JupyterLab Notebook]. Em seguida, você exercerá o workflow do bloco de anotações para receber em [!DNL JupyterLab] para criar uma receita dentro de [!DNL Data Science Workspace].

## Conceitos introduzidos:

- **Receitas:**  Uma receita é um termo Adobe para uma especificação de modelo e um contêiner de nível superior que representa um aprendizado de máquina específico, um algoritmo de IA ou um conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo treinado e, portanto, ajudar a resolver problemas específicos de negócios.
- **Modelo:** um modelo é uma instância de uma fórmula de aprendizado de máquina treinada com dados históricos e configurações para resolver um caso de uso comercial.
- **Treinamento:** o treinamento é o processo de padrões de aprendizado e insights de dados rotulados.
- **Pontuação:** a pontuação é o processo de geração de insights de dados usando um modelo treinado.

## Introdução ao ambiente do notebook [!DNL JupyterLab]

A criação de uma receita do zero pode ser feita dentro de [!DNL Data Science Workspace]. Para iniciar, navegue até [Adobe Experience Platform](https://platform.adobe.com) e clique na guia **[!UICONTROL Notebooks]** à esquerda. Crie um novo bloco de anotações selecionando o modelo Recipe Builder no [!DNL JupyterLab Launcher].

O notebook [!UICONTROL Recipe Builder] permite executar o treinamento e a pontuação dentro do notebook. Isso proporciona a flexibilidade para fazer alterações em seus métodos `train()` e `score()` entre a execução de experimentos nos dados de treinamento e pontuação. Quando estiver satisfeito com os resultados do treinamento e da pontuação, você poderá criar uma receita a ser usada em [!DNL Data Science Workspace] usando a funcionalidade notebook para receber incorporada ao notebook do Recipe Builder.

>[!NOTE]
>
>O notebook Recipe Builder suporta o trabalho com todos os formatos de arquivo, mas atualmente a funcionalidade Criar receita suporta apenas [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder.png)

Quando você clica no notebook Recipe Builder no iniciador, o bloco de notas é aberto na guia . O modelo usado no bloco de notas é a Receita de Previsão de Vendas de Retalho de Python, que também pode ser encontrada em [este repositório público](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

Você notará que na barra de ferramentas existem três ações adicionais, a saber, - **[!UICONTROL Train]**, **[!UICONTROL Score]** e **[!UICONTROL Create Recipe]**. Esses ícones só aparecem no bloco de anotações [!UICONTROL Recipe Builder]. Mais informações sobre essas ações serão faladas sobre [na seção treinamento e pontuação](#training-and-scoring) depois de criar sua Receita no notebook.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Fazer edições nos arquivos de receita

Para fazer edições nos arquivos de receita, navegue até a célula em Júpiter correspondente ao caminho do arquivo. Por exemplo, se você deseja fazer alterações em `evaluator.py`, procure por `%%writefile demo-recipe/evaluator.py`.

Comece a fazer as alterações necessárias na célula e, quando terminar, basta executar a célula. O comando `%%writefile filename.py` gravará o conteúdo da célula no `filename.py`. Será necessário executar manualmente a célula para cada arquivo com alterações.

>[!NOTE]
>
>Você deve executar as células manualmente quando aplicável.

## Introdução ao notebook Recipe Builder

Agora que você sabe as noções básicas para o ambiente de notebook [!DNL JupyterLab], pode começar a ver os arquivos que compõem uma fórmula de modelo de aprendizado de máquina. Os arquivos sobre os quais falaremos são mostrados aqui:

- [Arquivo de requisitos](#requirements-file)
- [Arquivos de configuração](#configuration-files)
- [Carregador de dados de treinamento](#training-data-loader)
- [Carregador de dados de pontuação](#scoring-data-loader)
- [Arquivo de pipeline](#pipeline-file)
- [Arquivo do avaliador](#evaluator-file)
- [Arquivo do Data Saver](#data-saver-file)

### Arquivo de requisitos {#requirements-file}

O arquivo requirements é usado para declarar bibliotecas adicionais que você deseja usar na fórmula. Você pode especificar o número da versão se houver uma dependência. Para procurar bibliotecas adicionais, visite [anaconda.org](https://anaconda.org). Para saber como formatar o arquivo de requisitos, visite [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). A lista de bibliotecas principais já em uso inclui:

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>As bibliotecas ou versões específicas adicionadas podem ser incompatíveis com as bibliotecas acima. Além disso, se optar por criar um arquivo de ambiente manualmente, o campo `name` não poderá ser substituído.

### Arquivos de configuração {#configuration-files}

Os arquivos de configuração, `training.conf` e `scoring.conf`, são usados para especificar os conjuntos de dados que você deseja usar para treinamento e pontuação, bem como adicionar hiperparâmetros. Há configurações separadas para treinamento e pontuação.

Os usuários devem preencher as seguintes variáveis antes de executar o treinamento e a pontuação:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Para localizar o conjunto de dados e as IDs do esquema, vá para a guia de dados ![Guia Dados](../images/jupyterlab/create-recipe/dataset-tab.png) nos blocos de anotações à esquerda da barra de navegação (sob o ícone de pasta).

![](../images/jupyterlab/create-recipe/dataset_tab.png)

As mesmas informações podem ser encontradas em [Adobe Experience Platform](https://platform.adobe.com/) nas guias **[Schema](https://platform.adobe.com/schema)** e **[Datasets](https://platform.adobe.com/dataset/overview)**.

Por padrão, os seguintes parâmetros de configuração são definidos para você ao acessar os dados:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Carregador de dados de treinamento {#training-data-loader}

O objetivo do Carregador de dados de treinamento é instanciar os dados usados para criar o modelo de aprendizado de máquina. Normalmente, há duas tarefas que o carregador de dados de treinamento realizará:
- Carregar dados de [!DNL Platform]
- Preparação de dados e engenharia de recursos

As duas seções a seguir abordarão o carregamento de dados e a preparação de dados.

### Carregamento de dados {#loading-data}

Essa etapa usa o [pandas dataframe](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Os dados podem ser carregados de arquivos em [!DNL Adobe Experience Platform] usando o [!DNL Platform] SDK (`platform_sdk`) ou de fontes externas usando as funções `read_csv()` ou `read_json()` dos painéis.

- [[!DNL Platform SDK]](#platform-sdk)
- [Fontes externas](#external-sources)

>[!NOTE]
>
>No notebook Recipe Builder, os dados são carregados por meio do carregador de dados `platform_sdk`.

### [!DNL Platform] SDK {#platform-sdk}

Para obter um tutorial detalhado sobre como usar o `platform_sdk` carregador de dados, visite o [guia do SDK da plataforma](../authoring/platform-sdk.md). Este tutorial fornece informações sobre autenticação de criação, leitura básica de dados e escrita básica de dados.

### Fontes externas {#external-sources}

Esta seção mostra como importar um arquivo JSON ou CSV para um objeto de painel. A documentação oficial da biblioteca dos pandas pode ser encontrada aqui:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Primeiro, veja um exemplo de importação de um arquivo CSV. O argumento `data` é o caminho para o arquivo CSV. Essa variável foi importada de `configProperties` na [seção anterior](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

Também é possível importar de um arquivo JSON. O argumento `data` é o caminho para o arquivo CSV. Essa variável foi importada de `configProperties` na [seção anterior](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Agora seus dados estão no objeto dataframe e podem ser analisados e manipulados na [próxima seção](#data-preparation-and-feature-engineering).

### Do SDK da plataforma

Você pode carregar dados usando o SDK da plataforma. A biblioteca pode ser importada na parte superior da página, incluindo a linha :

`from platform_sdk.dataset_reader import DatasetReader`

Em seguida, usamos o método `load()` para capturar o conjunto de dados de treinamento do `trainingDataSetId`, conforme definido em nosso arquivo de configuração (`recipe.conf`).

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    
    dataset_reader = DatasetReader(client_context, config_properties['trainingDataSetId'])
    
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

>[!NOTE]
>
>Conforme mencionado na seção [Arquivo de configuração](#configuration-files), os seguintes parâmetros de configuração são definidos para você ao acessar dados do Experience Platform usando `client_context`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Agora que você tem seus dados, você pode começar com preparação de dados e engenharia de recursos.

### Preparação de dados e engenharia de recursos {#data-preparation-and-feature-engineering}

Após os dados serem carregados, eles passam pela preparação e são divididos nos conjuntos de dados `train` e `val` . O código de exemplo é visto abaixo:

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
- adicionar colunas `week` e `year`
- converter `storeType` em uma variável de indicador
- converter `isHoliday` em uma variável numérica
- deslocar `weeklySales` para obter valor de vendas futuro e passado
- dividir dados, por data, em `train` e `val` conjunto de dados

Primeiro, as colunas `week` e `year` são criadas e a coluna original `date` é convertida em [!DNL Python] [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). Valores de semana e ano são extraídos do objeto datetime.

Em seguida, `storeType` é convertido em três colunas representando os três tipos diferentes de armazenamento, (`A`, `B` e `C`). Cada um conterá um valor booleano para indicar qual `storeType` é verdadeiro. A coluna `storeType` será solta.

Da mesma forma, `weeklySales` altera o booleano `isHoliday` para uma representação numérica, uma ou zero.

Esses dados são divididos entre `train` e `val` o conjunto de dados.

A função `load()` deve ser concluída com o conjunto de dados `train` e `val` como saída.

### Carregador de dados de pontuação {#scoring-data-loader}

O procedimento para carregar dados para pontuação é semelhante ao carregamento de dados de treinamento na função `split()` . Usamos o SDK de acesso a dados para carregar dados do `scoringDataSetId` encontrado em nosso arquivo `recipe.conf`.

```PYTHON
def load(config_properties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    client_context = get_client_context(config_properties)

    dataset_reader = DatasetReader(client_context, config_properties['scoringDataSetId'])
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

Após carregar os dados, a preparação de dados e a engenharia de recursos são feitas.

```PYTHON
    #########################################
    # Data Preparation/Feature Engineering
    #########################################
    if '_id' in dataframe.columns:
        #Rename columns to strip tenantId
        dataframe = dataframe.rename(columns = lambda x : str(x)[str(x).find('.')+1:])
        #Drop id, eventType and timestamp
        dataframe.drop(['_id', 'eventType', 'timestamp'], axis=1, inplace=True)

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

    print("Scoring Data Load Finish")

    return dataframe
```

Como o objetivo do nosso modelo é prever futuras vendas semanais, será necessário criar um conjunto de dados de pontuação usado para avaliar o desempenho da previsão do modelo.

Este notebook Recipe Builder faz isso compensando nossas vendas semanais em 7 dias. Observe que há medidas para 45 armazenamentos toda semana, para que você possa direcionar os valores de `weeklySales` 45 conjuntos de dados para uma nova coluna chamada `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Da mesma forma, é possível criar uma coluna `weeklySalesLag` alterando 45 para trás. Usando isso, você também pode calcular a diferença nas vendas semanais e armazená-las na coluna `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Como você está compensando os `weeklySales` conjuntos de dados 45 para frente e 45 conjuntos de dados para trás para criar novas colunas, o primeiro e o último 45 pontos de dados terão valores NaN. Você pode remover esses pontos de nosso conjunto de dados usando a função `df.dropna()` que remove todas as linhas que têm valores NaN.

```PYTHON
df.dropna(0, inplace=True)
```

A função `load()` no carregador de dados de pontuação deve ser concluída com o conjunto de dados de pontuação como saída.

### Arquivo de pipeline {#pipeline-file}

O arquivo `pipeline.py` inclui lógica para treinamento e pontuação.

### Treinamento {#training}

O objetivo do treinamento é criar um modelo usando recursos e rótulos em seu conjunto de dados de treinamento.

>[!NOTE]
> 
>Os recursos se referem à variável de entrada usada pelo modelo de aprendizado de máquina para prever os rótulos.

A função `train()` deve incluir o modelo de treinamento e retornar o modelo treinado. Alguns exemplos de modelos diferentes podem ser encontrados na [scikit-learn user guide documentation](https://scikit-learn.org/stable/user_guide.html).

Depois de escolher o modelo de treinamento, você ajustará o conjunto de dados de treinamento x e y ao modelo e a função retornará o modelo treinado. Um exemplo que mostra isso é o seguinte:

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

Observe que, dependendo de seu aplicativo, você terá argumentos em sua função `GradientBoostingRegressor()`. `xTrainingDataset` O deve conter seus recursos usados para treinamento, enquanto  `yTrainingDataset` deve conter seus rótulos.

### Pontuação {#scoring}

A função `score()` deve conter o algoritmo de pontuação e retornar uma medição para indicar o sucesso do modelo. A função `score()` usa os rótulos do conjunto de dados de pontuação e o modelo treinado para gerar um conjunto de recursos previstos. Esses valores previstos são comparados com os recursos reais no conjunto de dados de pontuação. Neste exemplo, a função `score()` usa o modelo treinado para prever recursos usando os rótulos do conjunto de dados de pontuação. Os recursos previstos são retornados.

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

O arquivo `evaluator.py` contém uma lógica sobre como você deseja avaliar a receita treinada, bem como a divisão dos dados de treinamento. No exemplo de vendas de varejo, a lógica para carregar e preparar os dados de treinamento será incluída. Vamos analisar as duas seções abaixo.

### Dividir o conjunto de dados {#split-the-dataset}

A fase de preparação de dados para treinamento requer a divisão do conjunto de dados a ser usado para treinamento e testes. Esses dados `val` serão usados implicitamente para avaliar o modelo após seu treinamento. Esse processo é separado da pontuação.

Esta seção mostrará a função `split()` que primeiro carregará dados no bloco de dados e, em seguida, limpará os dados removendo colunas não relacionadas no conjunto de dados. A partir daí, você poderá executar a engenharia de recursos, que é o processo para criar recursos relevantes adicionais a partir de recursos brutos existentes nos dados. Um exemplo desse processo pode ser visto abaixo, juntamente com uma explicação.

A função `split()` é mostrada abaixo. O dataframe fornecido no argumento será dividido nas variáveis `train` e `val` a serem retornadas.

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

A função `evaluate()` é executada após o modelo ser treinado e retornará uma métrica para indicar o sucesso do modelo. A função `evaluate()` usa os rótulos do conjunto de dados de teste e o modelo Treinado para prever um conjunto de recursos. Esses valores previstos são comparados com os recursos reais no conjunto de dados de teste. Os algoritmos de pontuação comuns incluem:
- [Erro percentual médio absoluto (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Erro médio absoluto (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Erro de quadrado médio raiz (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


A função `evaluate()` na amostra de vendas de varejo é mostrada abaixo:

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

Observe que a função retorna um objeto `metric` contendo uma matriz de métricas de avaliação. Essas métricas serão usadas para avaliar o desempenho do modelo treinado.

### Arquivo do Data Saver {#data-saver-file}

O arquivo `datasaver.py` contém a função `save()` para salvar sua previsão ao testar a pontuação. A função `save()` fará sua previsão e, usando [!DNL Experience Platform Catalog] APIs, gravará os dados no `scoringResultsDataSetId` especificado no arquivo `scoring.conf`.

O exemplo usado na receita de amostra de vendas de varejo é visto aqui. Observe o uso da biblioteca `DataSetWriter` para gravar dados na plataforma:

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

Quando terminar de fazer alterações no seu notebook e quiser treinar a receita, clique nos botões associados na parte superior da barra para criar uma execução de treinamento na célula. Ao clicar no botão , um log de comandos e saídas do script de treinamento aparecerá no bloco de notas (na célula `evaluator.py` ). O Conda instala primeiro todas as dependências e, em seguida, o treinamento é iniciado.

Observe que você deve executar o treinamento pelo menos uma vez antes de poder executar a pontuação. Clicar no botão **[!UICONTROL Run Scoring]** marcará o modelo treinado gerado durante o treinamento. O script de pontuação será exibido em `datasaver.py`.

Para fins de depuração, se quiser ver a saída oculta, adicione `debug` ao final da célula de saída e execute-a novamente.

## Criar receita {#create-recipe}

Quando terminar de editar a receita e ficar satisfeito com a saída de treinamento/pontuação, você pode criar uma receita do notebook pressionando **[!UICONTROL Create Recipe]** na navegação superior direita.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Depois de pressionar o botão, você é solicitado a inserir um nome de receita. Esse nome representa a receita real criada em [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Depois de pressionar **[!UICONTROL Ok]**, você poderá navegar até a nova fórmula em [Adobe Experience Platform](https://platform.adobe.com/). Você pode clicar no botão **[!UICONTROL View Recipes]** para ir até a guia **[!UICONTROL Recipes]** em **[!UICONTROL ML Models]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Quando o processo estiver concluído, a receita será semelhante a esta:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - Não exclua nenhuma das células de arquivo
> - Não edite a linha `%%writefile` na parte superior das células do arquivo
> - Não crie receitas em blocos de anotações diferentes ao mesmo tempo


## Próximas etapas {#next-steps}

Ao concluir este tutorial, você aprendeu a criar um modelo de aprendizado de máquina no notebook Recipe Builder. Você também aprendeu a usar o notebook para aproveitar o fluxo de trabalho do notebook para criar uma receita dentro de [!DNL Data Science Workspace].

Para continuar aprendendo como trabalhar com recursos em [!DNL Data Science Workspace], visite a lista suspensa [!DNL Data Science Workspace] receitas e modelos.

## Recursos adicionais {#additional-resources}

O vídeo a seguir foi criado para oferecer suporte à compreensão da criação e implantação de modelos.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)
