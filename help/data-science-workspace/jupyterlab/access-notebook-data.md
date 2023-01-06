---
keywords: Experience Platform; JupyterLab; blocos de anotações; Data Science Workspace; tópicos populares;%conjunto de dados; modo interativo; modo de lote; Spark sdk; python sdk; dados de acesso; acesso a dados do notebook
solution: Experience Platform
title: Acesso a dados em notebooks Jupyterlab
description: Este guia tem como foco o uso de notebooks Júpiter, criados no Data Science Workspace para acessar seus dados.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 8%

---

# Acesso aos dados em [!DNL Jupyterlab] notebooks

Cada kernel suportado fornece funcionalidades integradas que permitem ler os dados da plataforma a partir de um conjunto de dados dentro de um notebook. Atualmente, o JupyterLab no Adobe Experience Platform Data Science Workspace oferece suporte a notebooks para [!DNL Python], R, PySpark e Scala. No entanto, o suporte para paginação de dados está limitado a [!DNL Python] e R notebooks. Este guia tem como foco o uso de notebooks JupyterLab para acessar seus dados.

## Introdução

Antes de ler este guia, reveja o [[!DNL JupyterLab] guia do usuário](./overview.md) para uma introdução de alto nível ao [!DNL JupyterLab] e seu papel no Data Science Workspace.

## Limites de dados do notebook {#notebook-data-limits}

>[!IMPORTANT]
>
>Para blocos de anotações PySpark e Scala, se você estiver recebendo um erro com o motivo &quot;Cliente RPC remoto desassociado&quot;. Isso normalmente significa que o driver ou um executor está ficando sem memória. Tente alternar para [modo &quot;batch&quot;](#mode) para resolver esse erro.

As informações a seguir definem a quantidade máxima de dados que podem ser lidos, o tipo de dados usado e o período estimado de leitura dos dados.

Para [!DNL Python] e R, um servidor de notebook configurado com 40 GB de RAM foi usado para os benchmarks. Para PySpark e Scala, um cluster de databricks configurado em 64 GB de RAM, 8 núcleos, 2 DBU com no máximo 4 trabalhadores foi usado para os benchmarks descritos abaixo.

Os dados de esquema ExperienceEvent usados variaram em tamanho começando em mil (1K) linhas que variam de até um bilhão (1B) de linhas. Observe que para o PySpark e [!DNL Spark] , um período de 10 dias foi usado para os dados XDM.

Os dados do esquema ad-hoc foram pré-processados usando [!DNL Query Service] Criar tabela como seleção (CTAS). Esses dados também variaram em tamanho a partir de mil linhas (1.000) que variam de até um bilhão (1B) de linhas.

### Quando usar o modo de lote vs. o modo interativo {#mode}

Ao ler conjuntos de dados com blocos de dados PySpark e Scala, você tem a opção de usar o modo interativo ou o modo de lote para ler o conjunto de dados. Interativo é feito para resultados rápidos, enquanto o modo de lote é para grandes conjuntos de dados.

- Para notebooks PySpark e Scala, o modo de lote deve ser usado quando 5 milhões de linhas de dados ou mais estão sendo lidas. Para obter mais informações sobre a eficiência de cada modo, consulte o [PySpark](#pyspark-data-limits) ou [Scala](#scala-data-limits) tabelas de limites de dados abaixo.

### [!DNL Python] limites de dados do notebook

**Esquema XDM ExperienceEvent:** Você deve conseguir ler no máximo 2 milhões de linhas (~6,1 GB de dados no disco) de dados XDM em menos de 22 minutos. A adição de linhas adicionais pode resultar em erros.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Tamanho no disco (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (em segundos) | 20.3 | 86.8 | 63 | 659 | 1315 |

**esquema ad-hoc:** Você deve conseguir ler no máximo 5 milhões de linhas (~5,6 GB de dados no disco) de dados não-XDM (ad-hoc) em menos de 14 minutos. A adição de linhas adicionais pode resultar em erros.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Tamanho no disco (em MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (em segundos) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### Limites de dados do notebook R

**Esquema XDM ExperienceEvent:** Você deve ser capaz de ler no máximo 1 milhão de linhas de dados XDM (dados de 3 GB no disco) em menos de 13 minutos.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Tamanho no disco (MB) | 18.73 | 187.5 | 308 | 3000 |
| R Kernel (em segundos) | 14.03 | 69.6 | 86.8 | 775 |

**esquema ad-hoc:** Você deve conseguir ler no máximo 3 milhões de linhas de dados ad hoc (dados de 293 MB em disco) em aproximadamente 10 minutos.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Tamanho no disco (em MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| SDK R (em segundos) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark ([!DNL Python] kernel) limites de dados do notebook: {#pyspark-data-limits}

**Esquema XDM ExperienceEvent:** No modo interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~13,42 GB de dados no disco) de dados XDM em aproximadamente 20 minutos. O modo interativo suporta apenas até 5 milhões de linhas. Caso deseje ler conjuntos de dados maiores, sugerimos que você alterne para o modo de lote. No modo de lote, é possível ler no máximo 500 milhões de linhas (~1,31 TB de dados no disco) de dados XDM em cerca de 14 horas.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamanho no disco | 2.93MB | 4.38MB | 29.02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1.31TB |
| SDK (Modo interativo) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (Modo de lote) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**esquema ad-hoc:** No modo Interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~5,36 GB de dados no disco) de dados não-XDM em menos de 3 minutos. No modo Lote, você deve ser capaz de ler no máximo 1 bilhão de linhas (dados de~1,05 TB no disco) de dados não-XDM em cerca de 18 minutos.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Tamanho no disco | 1.12MB | 11.24MB | 109.48MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1.05TB |
| Modo interativo do SDK (em segundos) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| Modo de lote do SDK (em segundos) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] Limites de dados do notebook (kernel Scala): {#scala-data-limits}

**Esquema XDM ExperienceEvent:** No modo interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~13,42 GB de dados no disco) de dados XDM em cerca de 18 minutos. O modo interativo suporta apenas até 5 milhões de linhas. Caso deseje ler conjuntos de dados maiores, sugerimos que você alterne para o modo de lote. No modo de lote, é possível ler no máximo 500 milhões de linhas (~1,31 TB de dados no disco) de dados XDM em cerca de 14 horas.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamanho no disco | 2.93MB | 4.38MB | 29.02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1.31TB |
| Modo interativo do SDK (em segundos) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| Modo de lote do SDK (em segundos) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**esquema ad-hoc:** No modo interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~5,36 GB de dados no disco) de dados não-XDM em menos de 3 minutos. No modo de lote, você deve ser capaz de ler no máximo 1 bilhão de linhas (~1,05 TB de dados no disco) de dados não-XDM em cerca de 16 minutos.

| Número de linhas | 1 mil | 10 mil | 100 mil | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Tamanho no disco | 1.12MB | 11.24MB | 109.48MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1.05TB |
| Modo interativo do SDK (em segundos) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | - | - | - | - | - |
| Modo de lote do SDK (em segundos) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

## Notebooks Python {#python-notebook}

[!DNL Python] os blocos de notas permitem paginar dados ao acessar conjuntos de dados. O código de amostra para ler dados com e sem paginação é mostrado abaixo. Para obter mais informações sobre os notebooks Python disponíveis, visite o [[!DNL JupyterLab] Iniciador](./overview.md#launcher) no guia do usuário do JupyterLab.

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

A execução do código a seguir lerá os dados do conjunto de dados especificado. A paginação é realizada limitando e compensando dados por meio das funções `limit()` e `offset()` respectivamente. A limitação de dados refere-se ao número máximo de pontos de dados a serem lidos, enquanto a compensação refere-se ao número de pontos de dados a serem ignorados antes da leitura dos dados. Se a operação de leitura for executada com êxito, os dados serão salvos como um dataframe de Pandas referenciado pela variável `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Gravar em um conjunto de dados em Python {#write-python}

Para gravar em um conjunto de dados no bloco de dados JupyterLab, selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. O **[!UICONTROL Conjuntos de dados]** e **[!UICONTROL Esquemas]** diretórios são exibidos. Selecionar **[!UICONTROL Conjuntos de dados]** e clique com o botão direito do mouse, em seguida, selecione o **[!UICONTROL Gravar dados no notebook]** no menu suspenso do conjunto de dados que você deseja usar. Uma entrada de código executável é exibida na parte inferior do notebook.

![](../images/jupyterlab/data-access/write-dataset.png)

- Use **[!UICONTROL Gravar dados no notebook]** para gerar uma célula de gravação com o conjunto de dados selecionado.
- Use **[!UICONTROL Explorar dados no notebook]** para gerar uma célula de leitura com o conjunto de dados selecionado.
- Use **[!UICONTROL Dados de consulta no notebook]** para gerar uma célula de consulta básica com o conjunto de dados selecionado.

Como alternativa, você pode copiar e colar a seguinte célula de código. Substitua as duas `{DATASET_ID}` e `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Consultar dados usando [!DNL Query Service] em [!DNL Python] {#query-data-python}

[!DNL JupyterLab] on [!DNL Platform] permite usar o SQL em um [!DNL Python] notebook para acessar os dados por meio de [Serviço de query Adobe Experience Platform](https://www.adobe.com/go/query-service-home-en). Acesso aos dados por meio do [!DNL Query Service] pode ser útil para lidar com conjuntos de dados grandes devido a seus tempos de execução superiores. Observe que consultar dados usando [!DNL Query Service] O tem um limite de tempo de processamento de dez minutos.

Antes de utilizar [!DNL Query Service] em [!DNL JupyterLab], certifique-se de ter um entendimento prático do [[!DNL Query Service] Sintaxe SQL](https://www.adobe.com/go/query-service-sql-syntax-en).

Consulta de dados usando [!DNL Query Service] exige que você forneça o nome do conjunto de dados de destino. Você pode gerar as células de código necessárias localizando o conjunto de dados desejado usando o **[!UICONTROL Data Explorer]**. Clique com o botão direito na listagem do conjunto de dados e clique em **[!UICONTROL Dados de consulta no notebook]** para gerar duas células de código no bloco de notas. Essas duas células são descritas com mais detalhes abaixo.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Para utilizar [!DNL Query Service] em [!DNL JupyterLab], você deve primeiro criar uma conexão entre o seu trabalho [!DNL Python] notebook e [!DNL Query Service]. Isso pode ser feito executando-se a primeira célula gerada.

```python
qs_connect()
```

Na segunda célula gerada, a primeira linha deve ser definida antes da consulta SQL. Por padrão, a célula gerada define uma variável opcional (`df0`), que salva os resultados da consulta como um dataframe de Pandas. <br>O `-c QS_CONNECTION` O argumento é obrigatório e informa ao kernel para executar a consulta SQL em [!DNL Query Service]. Consulte a [apêndice](#optional-sql-flags-for-query-service) para obter uma lista de argumentos adicionais.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

As variáveis Python podem ser referenciadas diretamente em uma consulta SQL, usando uma sintaxe formatada em sequência e vinculando as variáveis entre colchetes (`{}`), conforme mostrado no exemplo a seguir:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtro [!DNL ExperienceEvent] dados {#python-filter}

Para acessar e filtrar um [!DNL ExperienceEvent] conjunto de dados em um [!DNL Python] , você deve fornecer a ID do conjunto de dados (`{DATASET_ID}`) juntamente com as regras de filtro que definem um intervalo de tempo específico usando operadores lógicos. Quando um intervalo de tempo é definido, qualquer paginação especificada é ignorada e todo o conjunto de dados é considerado.

Uma lista de operadores de filtragem é descrita abaixo:

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Maior que ou igual a
- `lt()`: Menos que
- `le()`: Less than or equal to
- `And()`: Operador AND lógico
- `Or()`: Operador OR lógico

A célula a seguir filtra e [!DNL ExperienceEvent] conjunto de dados para dados existentes exclusivamente entre 1 de janeiro de 2019 e o final de 31 de dezembro de 2019.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R notebooks {#r-notebooks}

Os blocos de notas R permitem paginar dados ao acessar conjuntos de dados. O código de amostra para ler dados com e sem paginação é mostrado abaixo. Para obter mais informações sobre os blocos de anotações R disponíveis, visite o [[!DNL JupyterLab] Iniciador](./overview.md#launcher) no guia do usuário do JupyterLab.

A documentação R abaixo descreve os seguintes conceitos:

- [Ler a partir de um conjunto de dados](#r-read-dataset)
- [Gravar em um conjunto de dados](#write-r)
- [Filtrar dados do ExperienceEvent](#r-filter)

### Ler a partir de um conjunto de dados em R {#r-read-dataset}

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

A execução do código a seguir lerá os dados do conjunto de dados especificado. A paginação é realizada limitando e compensando dados por meio das funções `limit()` e `offset()` respectivamente. A limitação de dados refere-se ao número máximo de pontos de dados a serem lidos, enquanto a compensação refere-se ao número de pontos de dados a serem ignorados antes da leitura dos dados. Se a operação de leitura for executada com êxito, os dados serão salvos como um dataframe de Pandas referenciado pela variável `df0`.

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

Para gravar em um conjunto de dados no bloco de dados JupyterLab, selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. O **[!UICONTROL Conjuntos de dados]** e **[!UICONTROL Esquemas]** diretórios são exibidos. Selecionar **[!UICONTROL Conjuntos de dados]** e clique com o botão direito do mouse, em seguida, selecione o **[!UICONTROL Gravar dados no notebook]** no menu suspenso do conjunto de dados que você deseja usar. Uma entrada de código executável é exibida na parte inferior do notebook.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Use **[!UICONTROL Gravar dados no notebook]** para gerar uma célula de gravação com o conjunto de dados selecionado.
- Use **[!UICONTROL Explorar dados no notebook]** para gerar uma célula de leitura com o conjunto de dados selecionado.

Como alternativa, você pode copiar e colar a seguinte célula de código:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtro [!DNL ExperienceEvent] dados {#r-filter}

Para acessar e filtrar um [!DNL ExperienceEvent] conjunto de dados em um notebook R, é necessário fornecer a ID do conjunto de dados (`{DATASET_ID}`) juntamente com as regras de filtro que definem um intervalo de tempo específico usando operadores lógicos. Quando um intervalo de tempo é definido, qualquer paginação especificada é ignorada e todo o conjunto de dados é considerado.

Uma lista de operadores de filtragem é descrita abaixo:

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Maior que ou igual a
- `lt()`: Menos que
- `le()`: Less than or equal to
- `And()`: Operador AND lógico
- `Or()`: Operador OR lógico

A célula a seguir filtra e [!DNL ExperienceEvent] conjunto de dados para dados existentes exclusivamente entre 1 de janeiro de 2019 e o final de 31 de dezembro de 2019.

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

Todos [!DNL Spark] Os notebooks 2.4 exigem que você inicialize a sessão com o seguinte código estereotipado.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Utilizando %dataset para ler e escrever com um bloco de notas PySpark 3 {#magic}

Com a introdução do [!DNL Spark] 2.4. `%dataset` a mágica personalizada é fornecida para uso no PySpark 3 ([!DNL Spark] 2.4) notebooks. Para obter mais detalhes sobre comandos mágicos disponíveis no kernel IPython, visite o [Documentação mágica de IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Uso**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Descrição**

Um personalizado [!DNL Data Science Workspace] comando mágico para ler ou gravar um conjunto de dados de um [!DNL PySpark] notebook ([!DNL Python] 3 kernel).

| Nome | Descrição | Obrigatório |
| --- | --- | --- |
| `{action}` | O tipo de ação a ser executada no conjunto de dados. Duas ações estão disponíveis &quot;ler&quot; ou &quot;gravar&quot;. | Sim |
| `--datasetId {id}` | Usado para fornecer a ID do conjunto de dados para ler ou gravar. | Sim |
| `--dataFrame {df}` | Os pandas dataframe. <ul><li> Quando a ação é &quot;lida&quot;, {df} é a variável na qual os resultados da operação de leitura do conjunto de dados estão disponíveis (como um dataframe). </li><li> Quando a ação é &quot;gravar&quot;, esse dataframe {df} é gravado no conjunto de dados. </li></ul> | Sim |
| `--mode` | Um parâmetro adicional que altera a forma como os dados são lidos. Os parâmetros permitidos são &quot;batch&quot; e &quot;interativos&quot;. Por padrão, o modo é definido como &quot;batch&quot;.<br> É recomendável que você use o modo &quot;interativo&quot; para aumentar o desempenho da consulta em conjuntos de dados menores. | Sim |

>[!TIP]
>
>Revise as tabelas do PySpark no [limites de dados do notebook](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

**Exemplos**

- **Exemplo de leitura**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Exemplo de gravação**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> Armazenamento de dados em cache usando `df.cache()` antes de gravar dados, é possível melhorar bastante o desempenho do notebook. Isso pode ajudar se você estiver recebendo um dos seguintes erros:
> 
> - Trabalho anulado devido a falha de estágio ... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Mau desempenho ao ler e gravar conjuntos de dados.
> 
> Consulte a [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

Você pode gerar automaticamente os exemplos acima na compra do JupyterLab usando o seguinte método:

Selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. O **[!UICONTROL Conjuntos de dados]** e **[!UICONTROL Esquemas]** diretórios são exibidos. Selecionar **[!UICONTROL Conjuntos de dados]** e clique com o botão direito do mouse, em seguida, selecione o **[!UICONTROL Gravar dados no notebook]** no menu suspenso do conjunto de dados que você deseja usar. Uma entrada de código executável é exibida na parte inferior do notebook.

- Use **[!UICONTROL Explorar dados no notebook]** para gerar uma célula de leitura.
- Use **[!UICONTROL Gravar dados no notebook]** para gerar uma célula de gravação.

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

### Filtro [!DNL ExperienceEvent] dados {#pyspark-filter-experienceevent}

Acessar e filtrar uma [!DNL ExperienceEvent] o conjunto de dados em um notebook PySpark requer que você forneça a identidade do conjunto de dados (`{DATASET_ID}`), a identidade IMS da organização e as regras de filtro que definem um intervalo de tempo específico. Um intervalo de tempo de filtragem é definido usando a função `spark.sql()`, onde o parâmetro da função é uma string de consulta SQL.

As células a seguir filtram um [!DNL ExperienceEvent] conjunto de dados para dados existentes exclusivamente entre 1 de janeiro de 2019 e o final de 31 de dezembro de 2019.

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

## Notebooks escaláveis {#scala-notebook}

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

No Scala, você pode importar `clientContext` para obter e retornar valores da Platform, isso elimina a necessidade de definir variáveis como `var userToken`. No exemplo Scala abaixo, `clientContext` é usada para obter e retornar todos os valores necessários para ler um conjunto de dados.

>[!IMPORTANT]
>
> Armazenamento de dados em cache usando `df.cache()` antes de gravar dados, é possível melhorar bastante o desempenho do notebook. Isso pode ajudar se você estiver recebendo um dos seguintes erros:
> 
> - Trabalho anulado devido a falha de estágio ... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Mau desempenho ao ler e gravar conjuntos de dados.
> 
> Consulte a [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

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
| ims-org | A ID da organização IMS que é buscada automaticamente usando `clientContext.getOrgId()`. |
| api-key | Sua chave de API que é buscada automaticamente usando `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise as tabelas do Scala no [limites de dados do notebook](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

Você pode gerar automaticamente o exemplo acima na compra do JupyterLab usando o seguinte método:

Selecione a guia Data icon (destacada abaixo) na navegação à esquerda do JupyterLab. O **[!UICONTROL Conjuntos de dados]** e **[!UICONTROL Esquemas]** diretórios são exibidos. Selecionar **[!UICONTROL Conjuntos de dados]** e clique com o botão direito do mouse, em seguida, selecione o **[!UICONTROL Explorar dados no notebook]** no menu suspenso do conjunto de dados que você deseja usar. Uma entrada de código executável é exibida na parte inferior do notebook.
E
- Use **[!UICONTROL Explorar dados no notebook]** para gerar uma célula de leitura.
- Use **[!UICONTROL Gravar dados no notebook]** para gerar uma célula de gravação.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Gravar em um conjunto de dados {#scala-write-dataset}

No Scala, você pode importar `clientContext` para obter e retornar valores da Platform, isso elimina a necessidade de definir variáveis como `var userToken`. No exemplo Scala abaixo, `clientContext` é usada para definir e retornar todos os valores necessários para gravar em um conjunto de dados.

>[!IMPORTANT]
>
> Armazenamento de dados em cache usando `df.cache()` antes de gravar dados, é possível melhorar bastante o desempenho do notebook. Isso pode ajudar se você estiver recebendo um dos seguintes erros:
> 
> - Trabalho anulado devido a falha de estágio ... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
> - Cliente RPC remoto desassociado e outros erros de memória.
> - Mau desempenho ao ler e gravar conjuntos de dados.
> 
> Consulte a [guia de solução de problemas](../troubleshooting-guide.md) para obter mais informações.

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
| df1 | Uma variável que representa o dataframe de Pandas usado para ler e gravar dados. |
| user-token | O token de usuário que é buscado automaticamente usando `clientContext.getUserToken()`. |
| service-token | O token de serviço que é buscado automaticamente usando `clientContext.getServiceToken()`. |
| ims-org | A ID da organização IMS que é buscada automaticamente usando `clientContext.getOrgId()`. |
| api-key | Sua chave de API que é buscada automaticamente usando `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise as tabelas do Scala no [limites de dados do notebook](#notebook-data-limits) para determinar se `mode` deve ser definido como `interactive` ou `batch`.

### criar um dataframe local {#scala-create-dataframe}

Para criar um dataframe local usando Scala, são necessárias consultas SQL. Por exemplo:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtro [!DNL ExperienceEvent] dados {#scala-experienceevent}

Acessar e filtrar uma [!DNL ExperienceEvent] o conjunto de dados em um notebook Scala requer que você forneça a identidade do conjunto de dados (`{DATASET_ID}`), a identidade IMS da organização e as regras de filtro que definem um intervalo de tempo específico. Um intervalo de tempo Filtering é definido usando a função `spark.sql()`, onde o parâmetro da função é uma string de consulta SQL.

As células a seguir filtram um [!DNL ExperienceEvent] conjunto de dados para dados existentes exclusivamente entre 1 de janeiro de 2019 e o final de 31 de dezembro de 2019.

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

Este documento cobriu as diretrizes gerais para acessar conjuntos de dados usando notebooks JupyterLab. Para obter exemplos mais aprofundados sobre consultas de conjuntos de dados, visite o [Serviço de query em notebooks JupyterLab](./query-service.md) documentação. Para obter mais informações sobre como explorar e visualizar seus conjuntos de dados, visite o documento em [análise de seus dados usando blocos de anotações](./analyze-your-data.md).

## Sinalizadores SQL opcionais para [!DNL Query Service] {#optional-sql-flags-for-query-service}

Esta tabela descreve os sinalizadores SQL opcionais que podem ser usados para [!DNL Query Service].

| **Sinalizador** | **Descrição** |
| --- | --- |
| `-h`, `--help` | Mostrar a mensagem de ajuda e sair. |
| `-n`, `--notify` | Alterne a opção para notificar os resultados da consulta. |
| `-a`, `--async` | O uso desse sinalizador executa a consulta de forma assíncrona e pode liberar o kernel enquanto a consulta está em execução. Tenha cuidado ao atribuir resultados da consulta a variáveis, pois eles podem estar indefinidos se a consulta não estiver concluída. |
| `-d`, `--display` | O uso desse sinalizador impede que os resultados sejam exibidos. |
