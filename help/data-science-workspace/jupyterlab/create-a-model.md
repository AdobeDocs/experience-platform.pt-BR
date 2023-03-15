---
keywords: Experience Platform;JupyterLab;receita;blocos de anotações;Data Science Workspace;tópicos populares;criar fórmula
solution: Experience Platform
title: Criar um modelo usando o JupyterLab Notebooks
type: Tutorial
description: Este tutorial percorre as etapas necessárias para criar uma fórmula usando o modelo do construtor de fórmula de notebooks JupyterLab.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# Criar um modelo usando o JupyterLab Notebooks

Este tutorial percorre as etapas necessárias para criar um modelo usando o modelo do construtor de fórmula de notebooks JupyterLab.

## Conceitos introduzidos:

- **Receitas:** Uma fórmula é um termo de Adobe para uma especificação de modelo e é um contêiner de nível superior que representa um aprendizado de máquina específico, algoritmo de IA ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo treinado.
- **Modelo:** Um modelo é uma instância de uma fórmula de aprendizado de máquina treinada com dados históricos e configurações para resolver em um caso de uso comercial.
- **Treinamento:** Treinamento é o processo de padrões de aprendizado e insights de dados rotulados.
- **Pontuação:** A pontuação é o processo de gerar insights dos dados usando um modelo treinado.

## Baixar os ativos necessários {#assets}

Antes de prosseguir com este tutorial, você deve criar os esquemas e conjuntos de dados necessários. Visite o tutorial para [criação de esquemas e conjuntos de dados do modelo de propensão Luma](../models-recipes/create-luma-data.md) para baixar os ativos necessários e configurar os pré-requisitos.

## Introdução ao [!DNL JupyterLab] ambiente de notebook

A criação de uma fórmula do zero pode ser feita dentro de [!DNL Data Science Workspace]. Para iniciar, navegue até [Adobe Experience Platform](https://platform.adobe.com) e selecione o **[!UICONTROL Notebooks]** à esquerda. Para criar um novo bloco de anotações, selecione o modelo de Construtor de fórmula na [!DNL JupyterLab Launcher].

A variável [!UICONTROL Construtor de fórmula] permite que você execute treinamentos e execuções de pontuação dentro do notebook. Isso proporciona flexibilidade para fazer alterações em seus `train()` e `score()` métodos entre a execução de experimentos nos dados de treinamento e pontuação. Quando estiver satisfeito com os resultados do treinamento e a pontuação, você poderá criar uma fórmula e, além disso, publicá-la como um modelo usando a funcionalidade receita para modelo.

>[!NOTE]
>
>A variável [!UICONTROL Construtor de fórmula] o notebook suporta o trabalho com todos os formatos de arquivo, mas atualmente a funcionalidade criar fórmula só suporta [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

Ao selecionar a variável [!UICONTROL Construtor de fórmula] no inicializador, o bloco de anotações é aberto em uma nova guia.

Na nova guia do bloco de notas na parte superior, é carregada uma barra de ferramentas contendo três ações adicionais - **[!UICONTROL Treinamento]**, **[!UICONTROL Pontuação]**, e **[!UICONTROL Criar fórmula]**. Esses ícones só aparecem no [!UICONTROL Construtor de fórmula] notebook. Mais informações sobre essas ações são fornecidas [na seção treinamento e pontuação](#training-and-scoring) depois de criar a fórmula no bloco de anotações.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Introdução ao [!UICONTROL Construtor de fórmula] notebook

Na pasta de ativos fornecida, há um modelo de propensão Luma `propensity_model.ipynb`. Usando a opção de carregar notebook no JupyterLab, carregue o modelo fornecido e abra o notebook.

![carregar bloco de anotações](../images/jupyterlab/create-recipe/upload_notebook.png)

O restante deste tutorial aborda os seguintes arquivos que são predefinidos no bloco de anotações do modelo de propensão:

- [Arquivo de requisitos](#requirements-file)
- [Arquivos de configuração](#configuration-files)
- [Carregador de dados de treinamento](#training-data-loader)
- [Carregador de dados de pontuação](#scoring-data-loader)
- [Arquivo de pipeline](#pipeline-file)
- [Arquivo avaliador](#evaluator-file)
- [Arquivo do salvador de dados](#data-saver-file)

O tutorial em vídeo a seguir explica o bloco de anotações do modelo de propensão Luma:

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### Arquivo de requisitos {#requirements-file}

O arquivo de requisitos é usado para declarar bibliotecas adicionais que você deseja usar no modelo. Você pode especificar o número da versão se houver uma dependência. Para procurar bibliotecas adicionais, visite [anaconda.org](https://anaconda.org). Para saber como formatar o arquivo de requisitos, visite [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). A lista de bibliotecas principais já em uso inclui:

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>As bibliotecas ou versões específicas adicionadas podem ser incompatíveis com as bibliotecas acima. Além disso, se você optar por criar um arquivo de ambiente manualmente, a variável `name` O campo não pode ser substituído.

Para o notebook modelo de propensão Luma, os requisitos não precisam ser atualizados.

### Arquivos de configuração {#configuration-files}

Os arquivos de configuração, `training.conf` e `scoring.conf`, são usados para especificar os conjuntos de dados que você deseja usar para treinamento e pontuação, bem como para adicionar hiperparâmetros. Há configurações separadas para treinamento e pontuação.

Para que um modelo execute o treinamento, você deve fornecer a `trainingDataSetId`, `ACP_DSW_TRAINING_XDM_SCHEMA`, e `tenantId`. Além disso, para a pontuação, você deve fornecer a `scoringDataSetId`, `tenantId`, e `scoringResultsDataSetId `.

Para localizar o conjunto de dados e as IDs do esquema, acesse a guia de dados ![Guia Dados](../images/jupyterlab/create-recipe/dataset-tab.png) nos blocos de anotações na barra de navegação à esquerda (sob o ícone de pasta). Três IDs diferentes do conjunto de dados precisam ser fornecidas. A variável `scoringResultsDataSetId` é usado para armazenar os resultados da pontuação do modelo e deve ser um conjunto de dados vazio. Esses conjuntos de dados foram criados anteriormente na [Ativos necessários](#assets) etapa.

![](../images/jupyterlab/create-recipe/dataset_tab.png)

As mesmas informações podem ser encontradas em [Adobe Experience Platform](https://platform.adobe.com/) no **[Esquema](https://platform.adobe.com/schema)** e **[Conjuntos de dados](https://platform.adobe.com/dataset/overview)** guias.

Depois de concluído, sua configuração de treinamento e pontuação deve ser semelhante à seguinte captura de tela:

![configuração](../images/jupyterlab/create-recipe/config.png)

Por padrão, os seguintes parâmetros de configuração são definidos para você ao treinar e pontuar dados:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Noções básicas sobre o carregador de dados de treinamento {#training-data-loader}

A finalidade do Carregador de dados de treinamento é instanciar os dados usados para criar o modelo de aprendizado de máquina. Normalmente, há duas tarefas que o carregador de dados de treinamento realiza:

- Carregando dados de [!DNL Platform]
- Preparação de dados e engenharia de recursos

As duas seções a seguir abordarão o carregamento de dados e a preparação de dados.

### Carregando dados {#loading-data}

Esta etapa utiliza o [quadro de dados pandas](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Os dados podem ser carregados de arquivos no [!DNL Adobe Experience Platform] usando [!DNL Platform] SDK (`platform_sdk`), ou de fontes externas usando pandas&#39; `read_csv()` ou `read_json()` funções.

- [[!DNL Platform SDK]](#platform-sdk)
- [Fontes externas](#external-sources)

>[!NOTE]
>
>No bloco de anotações do Construtor de fórmula, os dados são carregados por meio da `platform_sdk` carregador de dados.

### SDK do [!DNL Platform] {#platform-sdk}

Para obter um tutorial detalhado sobre o uso da `platform_sdk` carregador de dados, visite o [Guia do SDK do Platform](../authoring/platform-sdk.md). Este tutorial fornece informações sobre autenticação de build, leitura básica de dados e gravação básica de dados.

### Fontes externas {#external-sources}

Esta seção mostra como importar um arquivo JSON ou CSV para um objeto pandas. A documentação oficial da biblioteca de pandas pode ser encontrada aqui:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Primeiro, veja um exemplo da importação de um arquivo CSV. A variável `data` argumento é o caminho para o arquivo CSV. Essa variável foi importada do `configProperties` no [seção anterior](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

Você também pode importar de um arquivo JSON. A variável `data` argumento é o caminho para o arquivo CSV. Essa variável foi importada do `configProperties` no [seção anterior](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Agora, seus dados estão no objeto de quadro de dados e podem ser analisados e manipulados no [próxima seção](#data-preparation-and-feature-engineering).

## Arquivo do carregador de dados de treinamento

Neste exemplo, os dados são carregados usando o SDK da Platform. A biblioteca pode ser importada na parte superior da página incluindo a linha:

`from platform_sdk.dataset_reader import DatasetReader`

Em seguida, você pode usar o `load()` para coletar o conjunto de dados de treinamento do `trainingDataSetId` conforme definido na configuração (`recipe.conf`) arquivo.

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>Tal como mencionado no [Seção Arquivo de Configuração](#configuration-files), os seguintes parâmetros de configuração são definidos para você quando acessar dados do Experience Platform usando `client_context = get_client_context(config_properties)`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Agora que você tem seus dados, pode começar com a preparação de dados e a engenharia de recursos.

### Preparação de dados e engenharia de recursos {#data-preparation-and-feature-engineering}

Após os dados serem carregados, eles precisam ser limpos e submetidos à preparação. Neste exemplo, o objetivo do modelo é prever se um cliente solicitará um produto ou não. Como o modelo não está observando produtos específicos, você não precisa `productListItems` e, portanto, a coluna é solta. Em seguida, são soltas colunas adicionais que contêm apenas um único valor ou dois valores em uma única coluna. Ao treinar um modelo, é importante manter apenas dados úteis que ajudarão a prever sua meta.

![exemplo de preparação de dados](../images/jupyterlab/create-recipe/data_prep.png)

Depois de descartar os dados desnecessários, você pode iniciar a engenharia de recursos. Os dados de demonstração usados para este exemplo não contêm informações sobre a sessão. Normalmente, você gostaria de ter dados sobre as sessões atuais e anteriores de um cliente específico. Devido à falta de informações da sessão, este exemplo imita sessões atuais e passadas por meio da demarcação da jornada.

![Demarcação de jornada](../images/jupyterlab/create-recipe/journey_demarcation.png)

Após a conclusão da demarcação, os dados são rotulados e uma jornada é criada.

![rotular os dados](../images/jupyterlab/create-recipe/label_data.png)

Em seguida, os recursos são criados e divididos em passado e presente. Em seguida, qualquer coluna desnecessária é descartada, deixando você com as jornadas anteriores e atuais para clientes do Luma. Essas jornadas contêm informações como se um cliente comprou um item e a jornada que ele levou até a compra.

![treinamento final atual](../images/jupyterlab/create-recipe/final_journey.png)

## Carregador de dados de pontuação {#scoring-data-loader}

O procedimento para carregar dados para pontuação é semelhante ao carregamento de dados de treinamento. Observando de perto o código, você pode ver que tudo é o mesmo, exceto o `scoringDataSetId` no `dataset_reader`. Isso ocorre porque a mesma fonte de dados do Luma é usada para treinamento e pontuação.

Caso deseje usar arquivos de dados diferentes para treinamento e pontuação, o carregador de dados de treinamento e pontuação será separado. Isso permite executar pré-processamento adicional, como mapear os dados de treinamento para os dados de pontuação, se necessário.

## Arquivo de pipeline {#pipeline-file}

A variável `pipeline.py` O arquivo inclui lógica para treinamento e pontuação.

O objetivo do treinamento é criar um modelo usando recursos e rótulos em seu conjunto de dados de treinamento. Depois de escolher o modelo de treinamento, você deve ajustar o conjunto de dados de treinamento x e y ao modelo e a função retorna o modelo treinado.

>[!NOTE]
> 
>Os recursos se referem à variável de entrada usada pelo modelo de aprendizado de máquina para prever os rótulos.

![def train](../images/jupyterlab/create-recipe/def_train.png)

A variável `score()` A função deve conter o algoritmo de pontuação e retornar uma medição para indicar o desempenho do modelo. A variável `score()` A função usa os rótulos do conjunto de dados de pontuação e o modelo treinado para gerar um conjunto de recursos previstos. Esses valores previstos são comparados com os recursos reais no conjunto de dados de pontuação. Neste exemplo, a variável `score()` A função usa o modelo treinado para prever recursos usando os rótulos do conjunto de dados de pontuação. Os recursos previstos são retornados.

![pontuação def](../images/jupyterlab/create-recipe/def_score.png)

## Arquivo avaliador {#evaluator-file}

A variável `evaluator.py` O arquivo contém uma lógica de como você deseja avaliar sua fórmula treinada, bem como de como seus dados de treinamento devem ser divididos.

### Dividir o conjunto de dados {#split-the-dataset}

A fase de preparação dos dados de treinamento exige a divisão do conjunto de dados a ser usado para treinamento e teste. Este `val` Os dados do são usados implicitamente para avaliar o modelo após o treinamento. Esse processo é separado da pontuação.

Esta seção mostra a `split()` função que carrega dados no bloco de anotações e, em seguida, limpa os dados removendo colunas não relacionadas no conjunto de dados. A partir daí, você pode executar a engenharia de recursos, que é o processo para criar recursos relevantes adicionais a partir de recursos brutos existentes nos dados.

![Função Split](../images/jupyterlab/create-recipe/split.png)

### Avaliar o modelo treinado {#evaluate-the-trained-model}

A variável `evaluate()` A função é executada depois que o modelo é treinado e retorna uma métrica para indicar o desempenho do modelo. A variável `evaluate()` A função usa os rótulos do conjunto de dados de teste e o modelo treinado para prever um conjunto de recursos. Esses valores previstos são comparados com os recursos reais no conjunto de dados de teste. Neste exemplo, as métricas usadas são `precision`, `recall`, `f1`, e `accuracy`. Observe que a função retorna um valor `metric` objeto que contém uma matriz de métricas de avaliação. Essas métricas são usadas para avaliar o desempenho do modelo treinado.

![avaliar](../images/jupyterlab/create-recipe/evaluate.png)

Adicionando `print(metric)` permite exibir os resultados da métrica.

![resultados da métrica](../images/jupyterlab/create-recipe/evaluate_metric.png)

## Arquivo do salvador de dados {#data-saver-file}

A variável `datasaver.py` o arquivo contém o `save()` e é usada para salvar sua previsão enquanto testa a pontuação. A variável `save()` A função faz a previsão e usa [!DNL Experience Platform Catalog] , grava os dados na `scoringResultsDataSetId` você especificou em seu `scoring.conf` arquivo. Você pode

![Economizador de dados](../images/jupyterlab/create-recipe/data_saver.png)

## Treinamento e pontuação {#training-and-scoring}

Quando terminar de fazer alterações no seu bloco de anotações e quiser treinar sua fórmula, você poderá selecionar os botões associados na parte superior da barra para criar um treinamento executado na célula. Ao selecionar o botão, um registro de comandos e saídas do script de treinamento é exibido no bloco de notas (sob a `evaluator.py` célula). Primeiro, o Conda instala todas as dependências e, em seguida, o treinamento é iniciado.

Observe que você deve executar o treinamento pelo menos uma vez antes de poder executar a pontuação. Selecionar o **[!UICONTROL Executar pontuação]** O botão pontuará no modelo treinado que foi gerado durante o treinamento. O script de pontuação aparece em `datasaver.py`.

Para fins de depuração, se quiser ver a saída oculta, adicione `debug` para o final da célula de saída e execute-a novamente.

![treinar e pontuar](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Criar uma fórmula {#create-recipe}

Quando terminar de editar a fórmula e estiver satisfeito com a saída do treinamento/pontuação, você poderá criar uma fórmula no bloco de anotações selecionando **[!UICONTROL Criar fórmula]** no canto superior direito.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Depois de selecionar **[!UICONTROL Criar fórmula]**, será solicitado que você insira um nome de fórmula. Esse nome representa a fórmula real criada em [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Depois de selecionar **[!UICONTROL Ok]**, o processo de criação da fórmula será iniciado. Isso pode levar algum tempo e uma barra de progresso é exibida no lugar do botão Criar fórmula. Após a conclusão, é possível selecionar o **[!UICONTROL Exibir Receitas]** botão para levá-lo ao **[!UICONTROL Receitas]** em **[!UICONTROL Modelos ML]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - Não excluir nenhuma das células do arquivo
> - Não edite o `%%writefile` linha na parte superior das células do arquivo
> - Não criar receitas em blocos de anotações diferentes ao mesmo tempo


## Próximas etapas {#next-steps}

Ao concluir este tutorial, você aprendeu a criar um modelo de aprendizado de máquina na [!UICONTROL Construtor de fórmula] notebook. Você também aprendeu a exercitar o fluxo de trabalho de notebook para receita.

Para continuar aprendendo como trabalhar com recursos dentro do [!DNL Data Science Workspace], visite o [!DNL Data Science Workspace] lista suspensa receitas e modelos.