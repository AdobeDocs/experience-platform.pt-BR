---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;tópicos populares;%dataset;modo interativo;modo em lote;Spark sdk;python sdk;acessar dados;acesso a dados do bloco de anotações
solution: Experience Platform
title: Acesso aos dados nos notebooks Jupyterlab
description: Este guia tem como foco o uso do Jupyter Notebooks, integrado ao Data Science Workspace para acessar seus dados.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '3274'
ht-degree: 3%

---

# Acesso a dados em blocos de anotações do [!DNL Jupyterlab]

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Cada kernel suportado fornece funcionalidades integradas que permitem ler os dados do Experience Platform de um conjunto de dados em um notebook. Atualmente, o JupyterLab na Adobe Experience Platform Data Science Workspace oferece suporte a notebooks para [!DNL Python], R, PySpark e Scala. No entanto, o suporte para dados de paginação é limitado a blocos de anotações do [!DNL Python] e R. Este guia tem como foco o uso de notebooks JupyterLab para acessar seus dados.

## Introdução

Antes de ler este guia, consulte o [[!DNL JupyterLab] guia do usuário](./overview.md) para obter uma introdução geral sobre o [!DNL JupyterLab] e sua função no Data Science Workspace.

## Limites de dados de notebook {#notebook-data-limits}

>[!IMPORTANT]
>
>Para notebooks PySpark e Scala, se você estiver recebendo um erro com o motivo &quot;Cliente RPC remoto desassociado&quot;. Normalmente, isso significa que o driver ou um executor está ficando sem memória. Tente alternar para o modo [&quot;batch&quot;](#mode) para resolver esse erro.

As informações a seguir definem a quantidade máxima de dados que podem ser lidos, que tipo de dados foi usado e o período estimado para ler os dados.

Para [!DNL Python] e R, um servidor notebook configurado com 40 GB de RAM foi usado para os benchmarks. Para o PySpark e Scala, um cluster de databricks configurado em 64 GB de RAM, 8 núcleos, 2 DBUs com um máximo de 4 trabalhadores foi usado para os benchmarks descritos abaixo.

Os dados do esquema ExperienceEvent usados variaram em tamanho, começando em mil (1K) linhas, variando até um bilhão (1B) de linhas. Observe que para as métricas PySpark e [!DNL Spark], um intervalo de data de 10 dias foi usado para os dados XDM.

Os dados do esquema ad-hoc foram pré-processados usando o [!DNL Query Service] Criar Tabela como Seleção (CTAS). Esses dados também variaram em tamanho, começando com mil (1K) linhas variando até um bilhão (1B) de linhas.

### Quando usar o modo de lote vs. modo interativo {#mode}

Ao ler conjuntos de dados com notebooks PySpark e Scala, você tem a opção de usar o modo interativo ou o modo em lote para ler o conjunto de dados. Interativo é feito para resultados rápidos, enquanto o modo de lote é para conjuntos de dados grandes.

- Para notebooks PySpark e Scala, o modo de lote deve ser usado quando 5 milhões de linhas de dados ou mais estiverem sendo lidas. Para obter mais informações sobre a eficiência de cada modo, consulte as tabelas de limites de dados [PySpark](#pyspark-data-limits) ou [Scala](#scala-data-limits) abaixo.

### [!DNL Python] limites de dados do bloco de anotações

**Esquema XDM ExperienceEvent:** Você deve ser capaz de ler um máximo de 2 milhões de linhas (aproximadamente 6,1 GB de dados no disco) de dados XDM em menos de 22 minutos. A adição de linhas adicionais pode resultar em erros.

| Número de linhas | 1K | 10 K | 100 mil | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Tamanho no disco (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (em segundos) | 20,3 | 86,8 | 63 | 659 | 1315 |

**esquema ad-hoc:** Você deverá conseguir ler um máximo de 5 milhões de linhas (aproximadamente 5,6 GB de dados no disco) de dados não XDM (ad-hoc) em menos de 14 minutos. A adição de linhas adicionais pode resultar em erros.

| Número de linhas | 1K | 10 K | 100 mil | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Tamanho no disco (em MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (em segundos) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### Limites de dados do bloco de anotações R

**Esquema XDM ExperienceEvent:** Você deve ser capaz de ler no máximo 1 milhão de linhas de dados XDM (dados de 3 GB no disco) em menos de 13 minutos.

| Número de linhas | 1K | 10 K | 100 mil | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Tamanho no disco (MB) | 18,73 | 187,5 | 308 | 3000 |
| R Kernel (em segundos) | 14,03 | 69,6 | 86,8 | 775 |

**esquema ad-hoc:** Você deverá ler no máximo 3 milhões de linhas de dados ad-hoc (293 MB de dados no disco) em cerca de 10 minutos.

| Número de linhas | 1K | 10 K | 100 mil | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Tamanho no disco (em MB) | 0,082 | 0,612 | 9.0 | 91 | 188 | 293 |
| R SDK (em segundos) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Limites de dados de bloco de anotações do PySpark ([!DNL Python] kernel): {#pyspark-data-limits}

**Esquema XDM ExperienceEvent:** No modo interativo, você deve ler um máximo de 5 milhões de linhas (aproximadamente 13,42 GB de dados no disco) de dados XDM em cerca de 20 minutos. O modo interativo suporta apenas até 5 milhões de linhas. Se você quiser ler conjuntos de dados maiores, sugerimos mudar para o modo de lote. No modo de lote, você deve ser capaz de ler um máximo de 500 milhões de linhas (aproximadamente 1,31 TB de dados no disco) de dados XDM em cerca de 14 horas.

| Número de linhas | 1K | 10 K | 100 mil | 1M | 2M | 3M | 5M | 10M | 50 M | 100M | 500 M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamanho no disco | 2,93 MB | 4,38 MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| SDK (modo interativo) | 33s | 32,4s | 55,1s | 253,5s | 489,2s | 729,6s | 1206.8s | - | - | - | - |
| SDK (modo Lote) | 815,8s | 492,8s | 379.1s | 637,4s | 624,5s | 869,2s | 1104.1s | 1786 | 5387,2s | 10624.6s | 50547s |

**esquema ad-hoc:** No modo Interativo, você poderá ler um máximo de 5 milhões de linhas (aproximadamente 5,36 GB de dados no disco) de dados não XDM em menos de 3 minutos. No modo de Lote, você deve ser capaz de ler no máximo 1 bilhão de linhas (aproximadamente 1,05 TB de dados no disco) de dados não XDM em cerca de 18 minutos.

| Número de linhas | 1K | 10 K | 100 mil | 1M | 2M | 3M | 5M | 10M | 50 M | 100M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Tamanho no disco | 1,12 MB | 11,24 MB | 109,48 MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Modo interativo do SDK (em segundos) | 28,2s | 18,6s | 20.8s | 20.9s | 23,8s | 21,7s | 24,7s | - | - | - | - | - |
| Modo de lote do SDK (em segundos) | 428,8s | 578,8s | 641,4s | 538,5s | 630.9s | 467,3s | 411s | 675s | 702s | 719,2s | 1022.1s | 1122.3s |

### Limites de dados de bloco de anotações [!DNL Spark] (kernel Scala): {#scala-data-limits}

**Esquema XDM ExperienceEvent:** No modo interativo, você deve ler um máximo de 5 milhões de linhas (aproximadamente 13,42 GB de dados no disco) de dados XDM em cerca de 18 minutos. O modo interativo suporta apenas até 5 milhões de linhas. Se você quiser ler conjuntos de dados maiores, sugerimos mudar para o modo de lote. No modo de lote, você deve ser capaz de ler um máximo de 500 milhões de linhas (aproximadamente 1,31 TB de dados no disco) de dados XDM em cerca de 14 horas.

| Número de linhas | 1K | 10 K | 100 mil | 1M | 2M | 3M | 5M | 10M | 50 M | 100M | 500 M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamanho no disco | 2,93 MB | 4,38 MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| Modo interativo do SDK (em segundos) | 37,9s | 22,7s | 45,6s | 231,7s | 444,7s | 660,6s | 1100s | - | - | - | - |
| Modo de lote do SDK (em segundos) | 374,4s | 398,5s | 527s | 487,9s | 588,9s | 829s | 939.1s | 1441s | 5473,2s | 10118,8 | 49207,6 |

**esquema ad-hoc:** No modo interativo, você poderá ler um máximo de 5 milhões de linhas (aproximadamente 5,36 GB de dados no disco) de dados não XDM em menos de 3 minutos. No modo de lote, você deve ser capaz de ler no máximo 1 bilhão de linhas (aproximadamente 1,05 TB de dados no disco) de dados não XDM em cerca de 16 minutos.

| Número de linhas | 1K | 10 K | 100 mil | 1M | 2M | 3M | 5M | 10M | 50 M | 100M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Tamanho no disco | 1,12 MB | 11,24 MB | 109,48 MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Modo interativo do SDK (em segundos) | 35,7s | 31s | 19,5s | 25,3s | 23s | 33,2s | 25,5s | - | - | - | - | - |
| Modo de lote do SDK (em segundos) | 448,8s | 459,7s | 519s | 475,8s | 599,9s | 347,6s | 407,8s | 397s | 518,8s | 487,9s | 760.2s | 975,4s |

## Blocos de anotações Python {#python-notebook}

Os blocos de anotações do [!DNL Python] permitem que você pagine dados ao acessar conjuntos de dados. A amostra de código para ler dados com e sem paginação é demonstrada abaixo. Para obter mais informações sobre os notebooks Python iniciais disponíveis, visite a seção [[!DNL JupyterLab] Iniciador](./overview.md#launcher) no guia do usuário do JupyterLab.

A documentação do Python abaixo descreve os seguintes conceitos:

- [Ler de um conjunto de dados](#python-read-dataset)
- [Gravar em um conjunto de dados](#write-python)
- [Dados de consulta](#query-data-python)
- [Filtrar dados ExperienceEvent](#python-filter)

### Ler de um conjunto de dados no Python {#python-read-dataset}

**Sem paginação:**

A execução do código a seguir lerá todo o conjunto de dados. Se a execução for bem-sucedida, os dados serão salvos como um quadro de dados Pandas referenciado pela variável `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Com paginação:**

A execução do código a seguir lerá os dados do conjunto de dados especificado. A paginação é alcançada limitando e deslocando dados através das funções `limit()` e `offset()` respectivamente. A limitação de dados refere-se ao número máximo de pontos de dados a serem lidos, enquanto a compensação se refere ao número de pontos de dados a serem ignorados antes da leitura dos dados. Se a operação de leitura for executada com êxito, os dados serão salvos como um quadro de dados Pandas referenciado pela variável `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Gravar em um conjunto de dados no Python {#write-python}

Para gravar em um conjunto de dados no notebook JupyterLab, selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. Os diretórios **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** são exibidos. Selecione **[!UICONTROL Datasets]** e clique com o botão direito do mouse e selecione a opção **[!UICONTROL Write Data in Notebook]** no menu suspenso do conjunto de dados que você deseja usar. Uma entrada de código executável é exibida na parte inferior do bloco de anotações.

![](../images/jupyterlab/data-access/write-dataset.png)

- Use **[!UICONTROL Write Data in Notebook]** para gerar uma célula de gravação com o conjunto de dados selecionado.
- Use **[!UICONTROL Explore Data in Notebook]** para gerar uma célula de leitura com o conjunto de dados selecionado.
- Use **[!UICONTROL Query Data in Notebook]** para gerar uma célula de consulta básica com o conjunto de dados selecionado.

Como alternativa, você pode copiar e colar a seguinte célula de código. Substitua `{DATASET_ID}` e `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Consultar dados usando [!DNL Query Service] em [!DNL Python] {#query-data-python}

[!DNL JupyterLab] em [!DNL Experience Platform] permite que você use o SQL em um bloco de anotações [!DNL Python] para acessar dados por meio do [Serviço de Consulta Adobe Experience Platform](https://www.adobe.com/go/query-service-home-en). O acesso aos dados por meio do [!DNL Query Service] pode ser útil para lidar com grandes conjuntos de dados devido aos seus tempos de execução superiores. Observe que a consulta de dados usando o [!DNL Query Service] tem um limite de tempo de processamento de dez minutos.

Antes de usar [!DNL Query Service] em [!DNL JupyterLab], verifique se você tem uma compreensão funcional da [[!DNL Query Service] sintaxe SQL](https://www.adobe.com/go/query-service-sql-syntax-en).

A consulta de dados usando [!DNL Query Service] exige que você forneça o nome do conjunto de dados de destino. Você pode gerar as células de código necessárias localizando o conjunto de dados desejado usando o **[!UICONTROL Data explorer]**. Clique com o botão direito do mouse na lista do conjunto de dados e clique em **[!UICONTROL Query Data in Notebook]** para gerar duas células de código no seu bloco de anotações. Estas duas células são descritas em mais detalhes abaixo.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Para utilizar o [!DNL Query Service] no [!DNL JupyterLab], primeiro você deve criar uma conexão entre o bloco de anotações [!DNL Python] de trabalho e o [!DNL Query Service]. Isso pode ser feito executando a primeira célula gerada.

```python
qs_connect()
```

Na segunda célula gerada, a primeira linha deve ser definida antes da consulta SQL. Por padrão, a célula gerada define uma variável opcional (`df0`) que salva os resultados da consulta como um quadro de dados Pandas. <br>O argumento `-c QS_CONNECTION` é obrigatório e informa ao kernel para executar a consulta SQL em [!DNL Query Service]. Consulte o [apêndice](#optional-sql-flags-for-query-service) para obter uma lista de argumentos adicionais.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

As variáveis Python podem ser referenciadas diretamente em uma consulta SQL usando uma sintaxe formatada em sequência e unindo as variáveis entre chaves (`{}`), conforme mostrado no exemplo a seguir:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrar dados de [!DNL ExperienceEvent] {#python-filter}

Para acessar e filtrar um conjunto de dados [!DNL ExperienceEvent] em um bloco de anotações [!DNL Python], você deve fornecer a ID do conjunto de dados (`{DATASET_ID}`) juntamente com as regras de filtro que definem um intervalo de tempo específico usando operadores lógicos. Quando um intervalo de tempo é definido, qualquer paginação especificada é ignorada e todo o conjunto de dados é considerado.

Uma lista de operadores de filtragem é descrita abaixo:

- `eq()`: Igual a
- `gt()`: maior que
- `ge()`: Maior que ou igual a
- `lt()`: Menor que
- `le()`: Menor que ou igual a
- `And()`: Operador AND lógico
- `Or()`: Operador OR lógico

A célula a seguir filtra um conjunto de dados [!DNL ExperienceEvent] para dados existentes exclusivamente entre 1º de janeiro de 2019 e o final de 31 de dezembro de 2019.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## Blocos de anotações R {#r-notebooks}

Os blocos de anotações R permitem paginar dados ao acessar conjuntos de dados. A amostra de código para ler dados com e sem paginação é demonstrada abaixo. Para obter mais informações sobre os notebooks iniciais R disponíveis, visite a seção [[!DNL JupyterLab] Iniciador](./overview.md#launcher) no guia do usuário do JupyterLab.

A documentação do R abaixo descreve os seguintes conceitos:

- [Ler de um conjunto de dados](#r-read-dataset)
- [Gravar em um conjunto de dados](#write-r)
- [Filtrar dados ExperienceEvent](#r-filter)

### Ler de um conjunto de dados no R {#r-read-dataset}

**Sem paginação:**

A execução do código a seguir lerá todo o conjunto de dados. Se a execução for bem-sucedida, os dados serão salvos como um quadro de dados Pandas referenciado pela variável `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**Com paginação:**

A execução do código a seguir lerá os dados do conjunto de dados especificado. A paginação é alcançada limitando e deslocando dados através das funções `limit()` e `offset()` respectivamente. A limitação de dados refere-se ao número máximo de pontos de dados a serem lidos, enquanto a compensação se refere ao número de pontos de dados a serem ignorados antes da leitura dos dados. Se a operação de leitura for executada com êxito, os dados serão salvos como um quadro de dados Pandas referenciado pela variável `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### Gravar em um conjunto de dados no R {#write-r}

Para gravar em um conjunto de dados no notebook JupyterLab, selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. Os diretórios **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** são exibidos. Selecione **[!UICONTROL Datasets]** e clique com o botão direito do mouse e selecione a opção **[!UICONTROL Write Data in Notebook]** no menu suspenso do conjunto de dados que você deseja usar. Uma entrada de código executável é exibida na parte inferior do bloco de anotações.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Use **[!UICONTROL Write Data in Notebook]** para gerar uma célula de gravação com o conjunto de dados selecionado.
- Use **[!UICONTROL Explore Data in Notebook]** para gerar uma célula de leitura com o conjunto de dados selecionado.

Como alternativa, você pode copiar e colar a seguinte célula de código:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtrar dados de [!DNL ExperienceEvent] {#r-filter}

Para acessar e filtrar um conjunto de dados [!DNL ExperienceEvent] em um bloco de anotações R, você deve fornecer a ID do conjunto de dados (`{DATASET_ID}`) juntamente com as regras de filtro que definem um intervalo de tempo específico usando operadores lógicos. Quando um intervalo de tempo é definido, qualquer paginação especificada é ignorada e todo o conjunto de dados é considerado.

Uma lista de operadores de filtragem é descrita abaixo:

- `eq()`: Igual a
- `gt()`: maior que
- `ge()`: Maior que ou igual a
- `lt()`: Menor que
- `le()`: Menor que ou igual a
- `And()`: Operador AND lógico
- `Or()`: Operador OR lógico

A célula a seguir filtra um conjunto de dados [!DNL ExperienceEvent] para dados existentes exclusivamente entre 1º de janeiro de 2019 e o final de 31 de dezembro de 2019.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## Notebooks PySpark 3 {#pyspark-notebook}

A documentação do PySpark abaixo descreve os seguintes conceitos:

- [Inicializar sparkSession](#spark-initialize)
- [Ler e gravar dados](#magic)
- [Criar um quadro de dados local](#pyspark-create-dataframe)
- [Filtrar dados ExperienceEvent](#pyspark-filter-experienceevent)

### Inicializando sparkSession {#spark-initialize}

Todos os blocos de anotações do [!DNL Spark] 2.4 exigem que você inicialize a sessão com o seguinte código padrão.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Usando o conjunto de dados %s para ler e gravar com um bloco de anotações do PySpark 3 {#magic}

Com a introdução do [!DNL Spark] 2.4, a mágica personalizada do `%dataset` é fornecida para uso nos notebooks PySpark 3 ([!DNL Spark] 2.4). Para obter mais detalhes sobre comandos mágicos disponíveis no kernel IPython, visite a [documentação mágica do IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Uso**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Descrição**

Um comando mágico [!DNL Data Science Workspace] personalizado para ler ou gravar um conjunto de dados de um bloco de anotações [!DNL PySpark] ([!DNL Python] 3 kernel).

| Nome | Descrição | Obrigatório |
| --- | --- | --- |
| `{action}` | O tipo de ação a ser executada no conjunto de dados. Duas ações estão disponíveis: &quot;ler&quot; ou &quot;gravar&quot;. | Sim |
| `--datasetId {id}` | Usado para fornecer a ID do conjunto de dados para leitura ou gravação. | Sim |
| `--dataFrame {df}` | O quadro de dados dos pandas. <ul><li> Quando a ação é &quot;lida&quot;, {df} é a variável na qual os resultados da operação de leitura do conjunto de dados estão disponíveis (como um quadro de dados). </li><li> Quando a ação é &quot;gravar&quot;, esse dataframe {df} é gravado no conjunto de dados. </li></ul> | Sim |
| `--mode` | Um parâmetro adicional que altera como os dados são lidos. Os parâmetros permitidos são &quot;batch&quot; e &quot;interativo&quot;. Por padrão, o modo é definido como &quot;batch&quot;.<br> É recomendável usar o modo &quot;interativo&quot; para melhorar o desempenho da consulta em conjuntos de dados menores. | Sim |

>[!TIP]
>
>Revise as tabelas do PySpark na seção [limites de dados do bloco de anotações](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

**Exemplos**

- **Ler exemplo**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Escrever exemplo**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> O armazenamento em cache de dados usando `df.cache()` antes de gravar dados pode melhorar muito o desempenho do bloco de anotações. Isso pode ajudar se você estiver recebendo qualquer um dos seguintes erros:
> 
> - Trabalho anulado devido a falha no estágio... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Desempenho insatisfatório ao ler e gravar conjuntos de dados.
> 
> Consulte o [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

Você pode gerar automaticamente os exemplos acima na compra do JupyterLab usando o seguinte método:

Selecione a guia Data icon (destacada abaixo) no menu de navegação esquerdo do JupyterLab. Os diretórios **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** são exibidos. Selecione **[!UICONTROL Datasets]** e clique com o botão direito do mouse e selecione a opção **[!UICONTROL Write Data in Notebook]** no menu suspenso do conjunto de dados que você deseja usar. Uma entrada de código executável é exibida na parte inferior do bloco de anotações.

- Use **[!UICONTROL Explore Data in Notebook]** para gerar uma célula de leitura.
- Use **[!UICONTROL Write Data in Notebook]** para gerar uma célula de gravação.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Criar um quadro de dados local {#pyspark-create-dataframe}

Para criar um quadro de dados local usando o PySpark 3, use queries SQL. Por exemplo:

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>Você também pode especificar uma amostra de seed opcional, como um booleano com Substituição, fração dupla ou uma seed longa.

### Filtrar dados de [!DNL ExperienceEvent] {#pyspark-filter-experienceevent}

Para acessar e filtrar um conjunto de dados [!DNL ExperienceEvent] em um bloco de anotações do PySpark, é necessário fornecer a identidade do conjunto de dados (`{DATASET_ID}`), a identidade IMS da organização e as regras de filtro que definem um intervalo de tempo específico. Um intervalo de tempo de filtragem é definido com a função `spark.sql()`, na qual o parâmetro da função é uma cadeia de caracteres de consulta SQL.

As células a seguir filtram um conjunto de dados [!DNL ExperienceEvent] para dados existentes exclusivamente entre 1º de janeiro de 2019 e o final de 31 de dezembro de 2019.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Notebooks Scala {#scala-notebook}

A documentação abaixo contém exemplos dos seguintes conceitos:

- [Inicializar sparkSession](#scala-initialize)
- [Ler um conjunto de dados](#read-scala-dataset)
- [Gravar em um conjunto de dados](#scala-write-dataset)
- [Criar um quadro de dados local](#scala-create-dataframe)
- [Filtrar dados ExperienceEvent](#scala-experienceevent)

### Inicializando SparkSession {#scala-initialize}

Todos os blocos de anotações Scala exigem que você inicialize a sessão com o seguinte código padrão:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Ler um conjunto de dados {#read-scala-dataset}

No Scala, você pode importar `clientContext` para obter e retornar valores de Experience Platform. Isso elimina a necessidade de definir variáveis como `var userToken`. No exemplo da Escala abaixo, `clientContext` é usado para obter e retornar todos os valores necessários para ler um conjunto de dados.

>[!IMPORTANT]
>
> O armazenamento em cache de dados usando `df.cache()` antes de gravar dados pode melhorar muito o desempenho do bloco de anotações. Isso pode ajudar se você estiver recebendo qualquer um dos seguintes erros:
> 
> - Trabalho anulado devido a falha no estágio... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Desempenho insatisfatório ao ler e gravar conjuntos de dados.
> 
> Consulte o [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Elemento | Descrição |
| ------- | ----------- |
| df1 | Uma variável que representa o quadro de dados Pandas usado para ler e gravar dados. |
| user-token | O token do usuário que é buscado automaticamente usando o `clientContext.getUserToken()`. |
| service-token | O token de serviço que é buscado automaticamente usando o `clientContext.getServiceToken()`. |
| ims-org | A ID da organização que é buscada automaticamente usando o `clientContext.getOrgId()`. |
| api-key | A chave de API que é buscada automaticamente usando o `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise as tabelas Escala na seção [limites de dados de blocos de anotações](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

Você pode gerar automaticamente o exemplo acima na compra do JupyterLab usando o seguinte método:

Selecione a guia Data icon (destacada abaixo) no menu de navegação esquerdo do JupyterLab. Os diretórios **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** são exibidos. Selecione **[!UICONTROL Datasets]** e clique com o botão direito do mouse e selecione a opção **[!UICONTROL Explore Data in Notebook]** no menu suspenso do conjunto de dados que você deseja usar. Uma entrada de código executável é exibida na parte inferior do bloco de anotações.

E

- Use **[!UICONTROL Explore Data in Notebook]** para gerar uma célula de leitura.
- Use **[!UICONTROL Write Data in Notebook]** para gerar uma célula de gravação.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Gravar em um conjunto de dados {#scala-write-dataset}

No Scala, você pode importar `clientContext` para obter e retornar valores de Experience Platform. Isso elimina a necessidade de definir variáveis como `var userToken`. No exemplo de Escala abaixo, `clientContext` é usado para definir e retornar todos os valores necessários para gravar em um conjunto de dados.

>[!IMPORTANT]
>
> O armazenamento em cache de dados usando `df.cache()` antes de gravar dados pode melhorar muito o desempenho do bloco de anotações. Isso pode ajudar se você estiver recebendo qualquer um dos seguintes erros:
> 
> - Trabalho anulado devido a falha no estágio... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Desempenho insatisfatório ao ler e gravar conjuntos de dados.
> 
> Consulte o [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element | descrição |
| ------- | ----------- |
| df1 | Uma variável que representa o quadro de dados Pandas usado para ler e gravar dados. |
| user-token | O token do usuário que é buscado automaticamente usando o `clientContext.getUserToken()`. |
| service-token | O token de serviço que é buscado automaticamente usando o `clientContext.getServiceToken()`. |
| ims-org | A ID da organização que é buscada automaticamente usando o `clientContext.getOrgId()`. |
| api-key | A chave de API que é buscada automaticamente usando o `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise as tabelas Escala na seção [limites de dados de blocos de anotações](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

### criar um quadro de dados local {#scala-create-dataframe}

Para criar um quadro de dados local usando o Scala, são necessárias consultas SQL. Por exemplo:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtrar dados de [!DNL ExperienceEvent] {#scala-experienceevent}

Para acessar e filtrar um conjunto de dados [!DNL ExperienceEvent] em um bloco de anotações Scala, é necessário fornecer a identidade do conjunto de dados (`{DATASET_ID}`), a identidade IMS da sua organização e as regras de filtro que definem um intervalo de tempo específico. Um intervalo de tempo de Filtragem é definido com o uso da função `spark.sql()`, na qual o parâmetro da função é uma cadeia de caracteres de consulta SQL.

As células a seguir filtram um conjunto de dados [!DNL ExperienceEvent] para dados existentes exclusivamente entre 1º de janeiro de 2019 e o final de 31 de dezembro de 2019.

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## Próximas etapas

Esse documento abordou as diretrizes gerais para acessar conjuntos de dados usando notebooks JupyterLab. Para obter exemplos mais detalhados sobre consulta de conjuntos de dados, visite a documentação do [Serviço de consulta em notebooks JupyterLab](./query-service.md). Para obter mais informações sobre como explorar e visualizar seus conjuntos de dados, visite o documento em [analisando seus dados usando blocos de anotações](./analyze-your-data.md).

## Sinalizadores SQL opcionais para [!DNL Query Service] {#optional-sql-flags-for-query-service}

Esta tabela descreve os sinalizadores SQL opcionais que podem ser usados para [!DNL Query Service].

| **Sinalizador** | **Descrição** |
| --- | --- |
| `-h`, `--help` | Mostrar a mensagem de ajuda e sair. |
| `-n`, `--notify` | Alternar opção para notificar resultados da consulta. |
| `-a`, `--async` | O uso desse sinalizador executa a consulta de forma assíncrona e pode liberar o kernel enquanto a consulta é executada. Tenha cuidado ao atribuir resultados de consulta a variáveis, pois eles podem estar indefinidos se a consulta não estiver concluída. |
| `-d`, `--display` | O uso desse sinalizador impede que os resultados sejam exibidos. |
