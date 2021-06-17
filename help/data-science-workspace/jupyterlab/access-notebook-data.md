---
keywords: Experience Platform; JupyterLab; blocos de anotações; Data Science Workspace; tópicos populares;%conjunto de dados; modo interativo; modo de lote; Spark sdk; python sdk; dados de acesso; acesso a dados do notebook
solution: Experience Platform
title: Acesso a dados em notebooks Jupyterlab
topic-legacy: Developer Guide
description: Este guia tem como foco o uso de notebooks Júpiter, criados no Data Science Workspace para acessar seus dados.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 9e41db60580146fa90542ed00ceedd4eecb88b47
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 8%

---

# Acesso a dados em blocos de anotações [!DNL Jupyterlab]

Cada kernel suportado fornece funcionalidades integradas que permitem ler os dados da plataforma a partir de um conjunto de dados dentro de um notebook. Atualmente, o JupyterLab no Adobe Experience Platform Data Science Workspace oferece suporte a notebooks para [!DNL Python], R, PySpark e Scala. No entanto, o suporte para paginação de dados é limitado aos blocos de anotações [!DNL Python] e R. Este guia tem como foco o uso de notebooks JupyterLab para acessar seus dados.

## Introdução

Antes de ler este guia, revise o [[!DNL JupyterLab] guia do usuário](./overview.md) para obter uma introdução de alto nível a [!DNL JupyterLab] e sua função no Data Science Workspace.

## Limites de dados do notebook {#notebook-data-limits}

>[!IMPORTANT]
>
>Para blocos de anotações PySpark e Scala, se você estiver recebendo um erro com o motivo &quot;Cliente RPC remoto desassociado&quot;. Isso normalmente significa que o driver ou um executor está ficando sem memória. Tente alternar para o modo [&quot;batch&quot;](#mode) para resolver este erro.

As informações a seguir definem a quantidade máxima de dados que podem ser lidos, o tipo de dados usado e o período estimado de leitura dos dados.

Para [!DNL Python] e R, foi usado um servidor de notebook configurado com 40 GB de RAM para os benchmarks. Para PySpark e Scala, um cluster de databricks configurado em 64 GB de RAM, 8 núcleos, 2 DBU com no máximo 4 trabalhadores foi usado para os benchmarks descritos abaixo.

Os dados de esquema ExperienceEvent usados variaram em tamanho começando em mil (1K) linhas que variam de até um bilhão (1B) de linhas. Observe que para as métricas PySpark e [!DNL Spark], um período de 10 dias foi usado para os dados XDM.

Os dados do esquema ad-hoc foram pré-processados usando [!DNL Query Service] Criar tabela como seleção (CTAS). Esses dados também variaram em tamanho a partir de mil linhas (1.000) que variam de até um bilhão (1B) de linhas.

### Quando usar o modo de lote vs. o modo interativo {#mode}

Ao ler conjuntos de dados com blocos de dados PySpark e Scala, você tem a opção de usar o modo interativo ou o modo de lote para ler o conjunto de dados. Interativo é feito para resultados rápidos, enquanto o modo de lote é para grandes conjuntos de dados.

- Para notebooks PySpark e Scala, o modo de lote deve ser usado quando 5 milhões de linhas de dados ou mais estão sendo lidas. Para obter mais informações sobre a eficiência de cada modo, consulte as tabelas de limite de dados [PySpark](#pyspark-data-limits) ou [Scala](#scala-data-limits) abaixo.

### [!DNL Python] limites de dados do notebook

**Esquema XDM ExperienceEvent:** você deve ser capaz de ler no máximo 2 milhões de linhas (~6,1 GB de dados no disco) de dados XDM em menos de 22 minutos. A adição de linhas adicionais pode resultar em erros.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Tamanho no disco (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (em segundos) | 20,3 | 86,8 | 63º | 659 | 1315 |

**esquema ad-hoc:** você deve ser capaz de ler no máximo 5 milhões de linhas (~5,6 GB de dados no disco) de dados não-XDM (ad-hoc) em menos de 14 minutos. A adição de linhas adicionais pode resultar em erros.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5 M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Tamanho no disco (em MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (em segundos) | 7,27 | 9,04 | 27,3 | 180º | 346 | 487 | 819 |

### Limites de dados do notebook R

**Esquema XDM ExperienceEvent:** você deve conseguir ler no máximo 1 milhão de linhas de dados XDM (dados de 3 GB no disco) em menos de 13 minutos.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Tamanho no disco (MB) | 18,73 | 187,5 | 308 | 3000 |
| R Kernel (em segundos) | 14,03 | 69,6 | 86,8 | 775 |

**esquema ad-hoc:** você deve conseguir ler no máximo 3 milhões de linhas de dados ad-hoc (dados de 293 MB em disco) em aproximadamente 10 minutos.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Tamanho no disco (em MB) | 0,082 | 0,612 | 9.0 | 91º | 188 | 293º |
| SDK R (em segundos) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Limites de dados do bloco de notas PySpark ([!DNL Python] kernel): {#pyspark-data-limits}

**Esquema XDM ExperienceEvent:** no modo interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~13,42 GB de dados no disco) dos dados XDM em cerca de 20 minutos. O modo interativo suporta apenas até 5 milhões de linhas. Caso deseje ler conjuntos de dados maiores, sugerimos que você alterne para o modo de lote. No modo de lote, é possível ler no máximo 500 milhões de linhas (~1,31 TB de dados no disco) de dados XDM em cerca de 14 horas.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5 M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamanho no disco | 2,93 MB | 4,38 MB | 29,02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1,31 TB |
| SDK (Modo interativo) | 33s | 32,4 s | 55,1s | 253,5 s | 489,2 s | 729,6 s | 1206,8 s | - | - | - | - |
| SDK (Modo de lote) | 815,8 s | 492,8 s | 379,1s | 637,4 s | 624,5 s | 869,2 s | 1104.1s | 1786s | 5387,2 s | 10624.6s | 50547s |

**esquema ad-hoc:** no modo Interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~5,36 GB de dados no disco) de dados não-XDM em menos de 3 minutos. No modo Lote, você deve ser capaz de ler no máximo 1 bilhão de linhas (dados de~1,05 TB no disco) de dados não-XDM em cerca de 18 minutos.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5 M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Tamanho no disco | 1,12 MB | 11,24 MB | 109,48 MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1,05 TB |
| Modo interativo do SDK (em segundos) | 28,2 s | 18,6 s | 20,8 s | 20.9s | 23,8 s | 21,7 s | 24,7 s | - | - | - | - | - |
| Modo de lote do SDK (em segundos) | 428,8 s | 578,8 s | 641,4 s | 538,5 s | 630,9 s | 467,3 s | 411s | 675s | 702s | 719,2 s | 1022.1s | 1122.3s |

### [!DNL Spark] Limites de dados do notebook (kernel Scala):  {#scala-data-limits}

**Esquema XDM ExperienceEvent:** no modo interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~13,42 GB de dados no disco) dos dados XDM em cerca de 18 minutos. O modo interativo suporta apenas até 5 milhões de linhas. Caso deseje ler conjuntos de dados maiores, sugerimos que você alterne para o modo de lote. No modo de lote, é possível ler no máximo 500 milhões de linhas (~1,31 TB de dados no disco) de dados XDM em cerca de 14 horas.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5 M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamanho no disco | 2,93 MB | 4,38 MB | 29,02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1,31 TB |
| Modo interativo do SDK (em segundos) | 37,9 s | 22,7 s | 45,6 s | 231,7 s | 44,7 s | 660,6 s | 1100s | - | - | - | - |
| Modo de lote do SDK (em segundos) | 374,4 s | 398,5 s | 527 s | 487,9 s | 588,9s | 829s | 939.1s | 1441s | 5473,2 s | 10118,8 | 49207,6 |

**esquema ad-hoc:** no modo interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~5,36 GB de dados no disco) de dados não-XDM em menos de 3 minutos. No modo de lote, você deve ser capaz de ler no máximo 1 bilhão de linhas (~1,05 TB de dados no disco) de dados não-XDM em cerca de 16 minutos.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5 M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Tamanho no disco | 1,12 MB | 11,24 MB | 109,48 MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1,05 TB |
| Modo interativo do SDK (em segundos) | 35,7 s | 31s | 19,5 s | 25,3 s | 23s | 33,2 s | 25,5 s | - | - | - | - | - |
| Modo de lote do SDK (em segundos) | 448,8 s | 459,7 s | 519s | 475,8 s | 599,9 s | 347,6 s | 407,8 s | 397 s | 518,8 s | 487,9 s | 760,2 s | 975,4 s |

## Notebooks Python {#python-notebook}

[!DNL Python] os blocos de notas permitem paginar dados ao acessar conjuntos de dados. O código de amostra para ler dados com e sem paginação é mostrado abaixo. Para obter mais informações sobre os blocos de anotações iniciais disponíveis do Python, visite a seção [[!DNL JupyterLab] Launcher](./overview.md#launcher) no guia do usuário do JupyterLab.

A documentação de Python abaixo descreve os seguintes conceitos:

- [Ler a partir de um conjunto de dados](#python-read-dataset)
- [Gravar em um conjunto de dados](#write-python)
- [Consultar dados](#query-data-python)
- [Filtrar dados do ExperienceEvent](#python-filter)

### Ler de um conjunto de dados em Python {#python-read-dataset}

**Sem paginação:**

A execução do código a seguir lerá todo o conjunto de dados. Se a execução for bem-sucedida, os dados serão salvos como um dataframe de Paindas referenciado pela variável `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Com paginação:**

A execução do código a seguir lerá os dados do conjunto de dados especificado. A paginação é alcançada limitando e compensando dados por meio das funções `limit()` e `offset()`, respectivamente. A limitação de dados refere-se ao número máximo de pontos de dados a serem lidos, enquanto a compensação refere-se ao número de pontos de dados a serem ignorados antes da leitura dos dados. Se a operação de leitura for executada com êxito, os dados serão salvos como um dataframe de Pandas referenciado pela variável `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Gravar em um conjunto de dados em Python {#write-python}

Para gravar em um conjunto de dados no bloco de dados JupyterLab, selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. Os diretórios **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** são exibidos. Selecione **[!UICONTROL Datasets]** e clique com o botão direito do mouse e selecione a opção **[!UICONTROL Write Data in Notebook]** no menu suspenso do conjunto de dados que deseja usar. Uma entrada de código executável é exibida na parte inferior do notebook.

![](../images/jupyterlab/data-access/write-dataset.png)

- Use **[!UICONTROL Write Data in Notebook]** para gerar uma célula de gravação com o conjunto de dados selecionado.
- Use **[!UICONTROL Explorar dados no notebook]** para gerar uma célula de leitura com seu conjunto de dados selecionado.
- Use **[!UICONTROL Dados de consulta no Bloco de notas]** para gerar uma célula de consulta básica com o conjunto de dados selecionado.

Como alternativa, você pode copiar e colar a seguinte célula de código. Substitua o `{DATASET_ID}` e o `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Consultar dados usando [!DNL Query Service] em [!DNL Python] {#query-data-python}

[!DNL JupyterLab] O on  [!DNL Platform] permite usar o SQL em um  [!DNL Python] notebook para acessar dados por meio do  [Adobe Experience Platform Query Service](https://www.adobe.com/go/query-service-home-en). O acesso aos dados por meio de [!DNL Query Service] pode ser útil para lidar com grandes conjuntos de dados devido aos tempos de execução superiores. Observe que a consulta de dados usando [!DNL Query Service] tem um limite de tempo de processamento de dez minutos.

Antes de usar [!DNL Query Service] em [!DNL JupyterLab], certifique-se de ter uma compreensão funcional da [[!DNL Query Service] sintaxe SQL](https://www.adobe.com/go/query-service-sql-syntax-en).

Consultar dados usando [!DNL Query Service] requer que você forneça o nome do conjunto de dados de destino. Você pode gerar as células de código necessárias localizando o conjunto de dados desejado usando o **[!UICONTROL Data Explorer]**. Clique com o botão direito na listagem do conjunto de dados e clique em **[!UICONTROL Consultar dados no bloco de notas]** para gerar duas células de código no bloco de notas. Essas duas células são descritas com mais detalhes abaixo.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Para utilizar [!DNL Query Service] em [!DNL JupyterLab], primeiro você deve criar uma conexão entre o seu notebook de trabalho [!DNL Python] e [!DNL Query Service]. Isso pode ser feito executando-se a primeira célula gerada.

```python
qs_connect()
```

Na segunda célula gerada, a primeira linha deve ser definida antes da consulta SQL. Por padrão, a célula gerada define uma variável opcional (`df0`) que salva os resultados da consulta como um dataframe de Pandas. <br>O  `-c QS_CONNECTION` argumento é obrigatório e informa ao kernel para executar a consulta SQL no  [!DNL Query Service]. Consulte o [apêndice](#optional-sql-flags-for-query-service) para obter uma lista de argumentos adicionais.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

As variáveis Python podem ser referenciadas diretamente em uma consulta SQL usando uma sintaxe formatada em sequência e envolvendo as variáveis entre colchetes (`{}`), conforme mostrado no exemplo a seguir:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrar dados [!DNL ExperienceEvent] {#python-filter}

Para acessar e filtrar um conjunto de dados [!DNL ExperienceEvent] em um bloco de notas [!DNL Python], você deve fornecer a ID do conjunto de dados (`{DATASET_ID}`) juntamente com as regras de filtro que definem um intervalo de tempo específico usando operadores lógicos. Quando um intervalo de tempo é definido, qualquer paginação especificada é ignorada e todo o conjunto de dados é considerado.

Uma lista de operadores de filtragem é descrita abaixo:

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
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

## R blocos de anotações {#r-notebooks}

Os blocos de notas R permitem paginar dados ao acessar conjuntos de dados. O código de amostra para ler dados com e sem paginação é mostrado abaixo. Para obter mais informações sobre os blocos de anotações R disponíveis, visite a seção [[!DNL JupyterLab] Launcher](./overview.md#launcher) no guia do usuário do JupyterLab.

A documentação R abaixo descreve os seguintes conceitos:

- [Ler a partir de um conjunto de dados](#r-read-dataset)
- [Gravar em um conjunto de dados](#write-r)
- [Filtrar dados do ExperienceEvent](#r-filter)

### Ler de um conjunto de dados em R {#r-read-dataset}

**Sem paginação:**

A execução do código a seguir lerá todo o conjunto de dados. Se a execução for bem-sucedida, os dados serão salvos como um dataframe de Paindas referenciado pela variável `df0`.

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

A execução do código a seguir lerá os dados do conjunto de dados especificado. A paginação é alcançada limitando e compensando dados por meio das funções `limit()` e `offset()`, respectivamente. A limitação de dados refere-se ao número máximo de pontos de dados a serem lidos, enquanto a compensação refere-se ao número de pontos de dados a serem ignorados antes da leitura dos dados. Se a operação de leitura for executada com êxito, os dados serão salvos como um dataframe de Pandas referenciado pela variável `df0`.

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

### Gravar em um conjunto de dados em R {#write-r}

Para gravar em um conjunto de dados no bloco de dados JupyterLab, selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. Os diretórios **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** são exibidos. Selecione **[!UICONTROL Datasets]** e clique com o botão direito do mouse e selecione a opção **[!UICONTROL Write Data in Notebook]** no menu suspenso do conjunto de dados que deseja usar. Uma entrada de código executável é exibida na parte inferior do notebook.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Use **[!UICONTROL Write Data in Notebook]** para gerar uma célula de gravação com o conjunto de dados selecionado.
- Use **[!UICONTROL Explorar dados no notebook]** para gerar uma célula de leitura com seu conjunto de dados selecionado.

Como alternativa, você pode copiar e colar a seguinte célula de código:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtrar dados [!DNL ExperienceEvent] {#r-filter}

Para acessar e filtrar um conjunto de dados [!DNL ExperienceEvent] em um bloco de dados R, você deve fornecer a ID do conjunto de dados (`{DATASET_ID}`) juntamente com as regras de filtro que definem um intervalo de tempo específico usando operadores lógicos. Quando um intervalo de tempo é definido, qualquer paginação especificada é ignorada e todo o conjunto de dados é considerado.

Uma lista de operadores de filtragem é descrita abaixo:

- `eq()`: Igual a
- `gt()`: Maior que
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
- [Criar um dataframe local](#pyspark-create-dataframe)
- [Filtrar dados do ExperienceEvent](#pyspark-filter-experienceevent)

### Inicializando sparkSession {#spark-initialize}

Todos os notebooks [!DNL Spark] 2.4 exigem que você inicialize a sessão com o seguinte código estereotipado.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Utilizando %dataset para ler e escrever com um bloco de notas PySpark 3 {#magic}

Com a introdução de [!DNL Spark] 2.4, `%dataset` mágica personalizada é fornecida para uso em notebooks PySpark 3 ([!DNL Spark] 2.4). Para obter mais detalhes sobre comandos mágicos disponíveis no kernel do IPython, visite a [documentação mágica do IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Uso**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Descrição**

Um comando mágico [!DNL Data Science Workspace] personalizado para ler ou gravar um conjunto de dados de um bloco de anotações [!DNL PySpark] ([!DNL Python] 3 kernel).

| Nome | Descrição | Obrigatório |
| --- | --- | --- |
| `{action}` | O tipo de ação a ser executada no conjunto de dados. Duas ações estão disponíveis &quot;ler&quot; ou &quot;gravar&quot;. | Sim |
| `--datasetId {id}` | Usado para fornecer a ID do conjunto de dados para ler ou gravar. | Sim |
| `--dataFrame {df}` | Os pandas dataframe. <ul><li> Quando a ação é &quot;lida&quot;, {df} é a variável na qual os resultados da operação de leitura do conjunto de dados estão disponíveis (como um dataframe). </li><li> Quando a ação é &quot;gravar&quot;, esse dataframe {df} é gravado no conjunto de dados. </li></ul> | Sim |
| `--mode` | Um parâmetro adicional que altera a forma como os dados são lidos. Os parâmetros permitidos são &quot;batch&quot; e &quot;interativos&quot;. Por padrão, o modo é definido como &quot;batch&quot;.<br> É recomendável que você use o modo &quot;interativo&quot; para aumentar o desempenho da consulta em conjuntos de dados menores. | Sim |

>[!TIP]
>
>Revise as tabelas do PySpark na seção [limites de dados do bloco de notas](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

**Exemplos**

- **Exemplo** de leitura:  `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Exemplo** de gravação:  `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> Armazenar dados em cache usando `df.cache()` antes de gravar dados pode melhorar muito o desempenho do notebook. Isso pode ajudar se você estiver recebendo um dos seguintes erros:
> 
> - Trabalho anulado devido a falha de estágio ... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Mau desempenho ao ler e gravar conjuntos de dados.

> 
> 
Consulte o [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

Você pode gerar automaticamente os exemplos acima na compra do JupyterLab usando o seguinte método:

Selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. Os diretórios **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** são exibidos. Selecione **[!UICONTROL Datasets]** e clique com o botão direito do mouse e selecione a opção **[!UICONTROL Write Data in Notebook]** no menu suspenso do conjunto de dados que deseja usar. Uma entrada de código executável é exibida na parte inferior do notebook.

- Use **[!UICONTROL Explorar dados no notebook]** para gerar uma célula de leitura.
- Use **[!UICONTROL Write Data in Notebook]** para gerar uma célula de gravação.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Criar um dataframe local {#pyspark-create-dataframe}

Para criar um dataframe local usando PySpark 3, use queries SQL. Por exemplo:

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
>Também é possível especificar uma amostra de seed opcional, como um booleano com Replacement, fração dupla ou uma semente longa.

### Filtrar dados [!DNL ExperienceEvent] {#pyspark-filter-experienceevent}

Acessar e filtrar um conjunto de dados [!DNL ExperienceEvent] em um notebook PySpark requer que você forneça a identidade do conjunto de dados (`{DATASET_ID}`), a identidade IMS de sua organização e as regras de filtro que definem um intervalo de tempo específico. Um intervalo de tempo de filtragem é definido usando a função `spark.sql()`, onde o parâmetro da função é uma string de consulta SQL.

As células a seguir filtram um conjunto de dados [!DNL ExperienceEvent] para dados existentes exclusivamente entre 1 de janeiro de 2019 e o final de 31 de dezembro de 2019.

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

## Blocos de anotações escaláveis {#scala-notebook}

A documentação abaixo contém exemplos para os seguintes conceitos:

- [Inicializar sparkSession](#scala-initialize)
- [Ler um conjunto de dados](#read-scala-dataset)
- [Gravar em um conjunto de dados](#scala-write-dataset)
- [Criar um dataframe local](#scala-create-dataframe)
- [Filtrar dados do ExperienceEvent](#scala-experienceevent)

### Inicializando SparkSession {#scala-initialize}

Todos os notebooks Scala exigem que você inicialize a sessão com o seguinte código estereotipado:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Ler um conjunto de dados {#read-scala-dataset}

No Scala, é possível importar `clientContext` para obter e retornar valores da Plataforma, isso elimina a necessidade de definir variáveis como `var userToken`. No exemplo Scala abaixo, `clientContext` é usado para obter e retornar todos os valores necessários para ler um conjunto de dados.

>[!IMPORTANT]
>
> Armazenar dados em cache usando `df.cache()` antes de gravar dados pode melhorar muito o desempenho do notebook. Isso pode ajudar se você estiver recebendo um dos seguintes erros:
> 
> - Trabalho anulado devido a falha de estágio ... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Mau desempenho ao ler e gravar conjuntos de dados.

> 
> 
Consulte o [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

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
| df1 | Uma variável que representa o dataframe de Pandas usado para ler e gravar dados. |
| user-token | O token de usuário que é buscado automaticamente usando `clientContext.getUserToken()`. |
| service-token | O token de serviço que é buscado automaticamente usando `clientContext.getServiceToken()`. |
| ims-org | Sua ID da Org IMS que é buscada automaticamente usando `clientContext.getOrgId()`. |
| api-key | Sua chave de API que é buscada automaticamente usando `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise as tabelas do Scala na seção [limites de dados do notebook](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

Você pode gerar automaticamente o exemplo acima na compra do JupyterLab usando o seguinte método:

Selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. Os diretórios **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** são exibidos. Selecione **[!UICONTROL Datasets]** e clique com o botão direito do mouse e selecione a opção **[!UICONTROL Explorar dados no notebook]** no menu suspenso do conjunto de dados que deseja usar. Uma entrada de código executável é exibida na parte inferior do notebook.
E
- Use **[!UICONTROL Explorar dados no notebook]** para gerar uma célula de leitura.
- Use **[!UICONTROL Write Data in Notebook]** para gerar uma célula de gravação.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Gravar em um conjunto de dados {#scala-write-dataset}

No Scala, é possível importar `clientContext` para obter e retornar valores da Plataforma, isso elimina a necessidade de definir variáveis como `var userToken`. No exemplo Scala abaixo, `clientContext` é usado para definir e retornar todos os valores necessários para gravar em um conjunto de dados.

>[!IMPORTANT]
>
> Armazenar dados em cache usando `df.cache()` antes de gravar dados pode melhorar muito o desempenho do notebook. Isso pode ajudar se você estiver recebendo um dos seguintes erros:
> 
> - Trabalho anulado devido a falha de estágio ... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Mau desempenho ao ler e gravar conjuntos de dados.

> 
> 
Consulte o [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

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

| direcionado | descrição |
| ------- | ----------- |
| df1 | Uma variável que representa o dataframe de Pandas usado para ler e gravar dados. |
| user-token | O token de usuário que é buscado automaticamente usando `clientContext.getUserToken()`. |
| service-token | O token de serviço que é buscado automaticamente usando `clientContext.getServiceToken()`. |
| ims-org | Sua ID da Org IMS que é buscada automaticamente usando `clientContext.getOrgId()`. |
| api-key | Sua chave de API que é buscada automaticamente usando `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise as tabelas do Scala na seção [limites de dados do notebook](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

### criar um dataframe local {#scala-create-dataframe}

Para criar um dataframe local usando Scala, são necessárias consultas SQL. Por exemplo:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtrar dados [!DNL ExperienceEvent] {#scala-experienceevent}

Acessar e filtrar um conjunto de dados [!DNL ExperienceEvent] em um notebook Scala requer que você forneça a identidade do conjunto de dados (`{DATASET_ID}`), a identidade IMS de sua organização e as regras de filtro que definem um intervalo de tempo específico. Um intervalo de tempo Filtering é definido usando a função `spark.sql()`, onde o parâmetro de função é uma string de consulta SQL.

As células a seguir filtram um conjunto de dados [!DNL ExperienceEvent] para dados existentes exclusivamente entre 1 de janeiro de 2019 e o final de 31 de dezembro de 2019.

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

Este documento cobriu as diretrizes gerais para acessar conjuntos de dados usando notebooks JupyterLab. Para obter exemplos mais aprofundados sobre como consultar conjuntos de dados, visite a documentação [Serviço de query nos notebooks JupyterLab](./query-service.md). Para obter mais informações sobre como explorar e visualizar seus conjuntos de dados, visite o documento em [analisar seus dados usando notebooks](./analyze-your-data.md).

## Sinalizadores SQL opcionais para [!DNL Query Service] {#optional-sql-flags-for-query-service}

Esta tabela descreve os sinalizadores SQL opcionais que podem ser usados para [!DNL Query Service].

| **Sinalizador** | **Descrição** |
| --- | --- |
| `-h`, `--help` | Mostrar a mensagem de ajuda e sair. |
| `-n`,  `--notify` | Alterne a opção para notificar os resultados da consulta. |
| `-a`,  `--async` | O uso desse sinalizador executa a consulta de forma assíncrona e pode liberar o kernel enquanto a consulta está em execução. Tenha cuidado ao atribuir resultados da consulta a variáveis, pois eles podem estar indefinidos se a consulta não estiver concluída. |
| `-d`,  `--display` | O uso desse sinalizador impede que os resultados sejam exibidos. |
