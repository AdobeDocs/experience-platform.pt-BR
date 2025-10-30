---
keywords: Experience Platform;guia do desenvolvedor;SDK;Acesso a dados SDK;Data Science Workspace;tópicos populares;;developer guide;;Data Access;Data Science;popular topics
solution: Experience Platform
title: Criação de modelos usando o Adobe Experience Platform SDK
description: Este tutorial fornece informações sobre a conversão de data_access_sdk_python para o novo Python platform_sdk no Python e no R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# Criação de modelo usando o SDK do Adobe [!DNL Experience Platform]

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial fornece informações sobre como converter `data_access_sdk_python` para o novo Python `platform_sdk` em Python e R. Este tutorial fornece informações sobre as seguintes operações:

- [Compilar autenticação](#build-authentication)
- [Leitura básica de dados](#basic-reading-of-data)
- [Gravação básica de dados](#basic-writing-of-data)

## Compilar autenticação {#build-authentication}

A autenticação é necessária para fazer chamadas para [!DNL Adobe Experience Platform] e é composta pela Chave de API, ID da organização, um token de usuário e um token de serviço.

### Python

Se você estiver usando o Jupyter Notebook, use o código abaixo para criar o `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Se você não estiver usando o Jupyter Notebook ou precisar alterar a organização, use a amostra de código abaixo:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Se você estiver usando o Jupyter Notebook, use o código abaixo para criar o `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Se você não estiver usando o Jupyter Notebook ou precisar alterar a organização, use a amostra de código abaixo:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Leitura básica de dados {#basic-reading-of-data}

Com o novo SDK [!DNL Experience Platform], o tamanho máximo de leitura é de 32 GB, com um tempo máximo de leitura de 10 minutos.

Se o tempo de leitura estiver demorando muito, tente usar uma das seguintes opções de filtro:

- [Filtragem de dados por deslocamento e limite](#filter-by-offset-and-limit)
- [Filtrar dados por data](#filter-by-date)
- [Filtrar dados por coluna](#filter-by-selected-columns)
- [Obtendo resultados classificados](#get-sorted-results)

>[!NOTE]
>
>A organização está definida no `client_context`.

### Python

Para ler dados em Python, use a amostra de código abaixo:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Para ler os dados em R, use a amostra de código abaixo:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtrar por deslocamento e limite {#filter-by-offset-and-limit}

Como não há mais suporte para filtragem por ID de lote, para determinar a leitura de dados, é necessário usar `offset` e `limit`.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## Filtrar por data {#filter-by-date}

A granularidade da filtragem de data agora é definida pelo carimbo de data e hora, em vez de ser definida pelo dia.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

O novo SDK [!DNL Experience Platform] oferece suporte às seguintes operações:

| Operação | Função |
| --------- | -------- |
| Igual a (`=`) | `eq()` |
| Maior que (`>`) | `gt()` |
| Maior ou igual a (`>=`) | `ge()` |
| Menor que (`<`) | `lt()` |
| Menor que ou igual a (`<=`) | `le()` |
| E (`&`) | `And()` |
| Ou ( &amp;vert; ) | `Or()` |

## Filtrar por colunas selecionadas {#filter-by-selected-columns}

Para refinar ainda mais a leitura de dados, também é possível filtrar por nome de coluna.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Obter resultados classificados {#get-sorted-results}

Os resultados recebidos podem ser classificados por colunas especificadas do conjunto de dados de destino e em sua ordem (asc/desc), respectivamente.

No exemplo a seguir, o quadro de dados é classificado pela &quot;coluna a&quot; primeiro em ordem crescente. As linhas com os mesmos valores para &quot;column-a&quot; são então classificadas por &quot;column-b&quot; em ordem decrescente.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Gravação básica de dados {#basic-writing-of-data}

>[!NOTE]
>
>A organização está definida no `client_context`.

Para escrever dados em Python e R, use um dos seguintes exemplos abaixo:

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## Próximas etapas

Depois de configurar o carregador de dados `platform_sdk`, os dados serão preparados e divididos nos conjuntos de dados `train` e `val`. Para saber mais sobre preparação de dados e engenharia de recursos, visite a seção sobre [preparação de dados e engenharia de recursos](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) no tutorial para a criação de uma fórmula usando blocos de anotações [!DNL JupyterLab].
