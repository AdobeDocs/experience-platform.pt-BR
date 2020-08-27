---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;popular topics
solution: Experience Platform
title: Guia do SDK da plataforma
topic: SDK authoring
description: Este tutorial fornece informações sobre a conversão de data_access_sdk_python para a nova plataforma Python_sdk em Python e R.
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 5%

---


# [!DNL Platform] Guia do SDK

Este tutorial fornece informações sobre como converter `data_access_sdk_python` para o novo Python `platform_sdk` em Python e R. Este tutorial fornece informações sobre as seguintes operações:

- [Autenticação de compilação](#build-authentication)
- [Leitura básica dos dados](#basic-reading-of-data)
- [Escrita básica dos dados](#basic-writing-of-data)

## Autenticação de compilação {#build-authentication}

A autenticação é necessária para fazer chamadas e é composta por chave de API, ID de organização IMS, um token de usuário e um token de serviço. [!DNL Adobe Experience Platform]

### Python

Se estiver usando o notebook Jupyter, use o código abaixo para criar o `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Se você não estiver usando o Notebook Jupyter ou precisar alterar a Organização IMS, use a amostra de código abaixo:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Se estiver usando o notebook Jupyter, use o código abaixo para criar o `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Se você não estiver usando o Notebook Jupyter ou precisar alterar a Organização IMS, use a amostra de código abaixo:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Leitura básica dos dados {#basic-reading-of-data}

Com o novo [!DNL Platform] SDK, o tamanho máximo de leitura é de 32 GB, com um tempo máximo de leitura de 10 minutos.

Se o tempo de leitura estiver demorando muito, tente usar uma das seguintes opções de filtragem:

- [Filtrar dados por deslocamento e limite](#filter-by-offset-and-limit)
- [Filtrar dados por data](#filter-by-date)
- [Filtrar dados por coluna](#filter-by-selected-columns)
- [Obtendo resultados classificados](#get-sorted-results)

>[!NOTE]
>
>A Organização IMS está definida dentro da `client_context`.

### Python

Para ler dados no Python, use a amostra de código abaixo:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Para ler dados em R, use a amostra de código abaixo:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtrar por deslocamento e limite {#filter-by-offset-and-limit}

Como a filtragem por ID de lote não é mais suportada, para a leitura de dados no escopo, é necessário usar `offset` e `limit`.

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

A granularidade da filtragem de datas agora é definida pelo carimbo de data e hora, em vez de ser definida pelo dia.

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

O novo [!DNL Platform] SDK oferece suporte às seguintes operações:

| Operação | Função |
| --------- | -------- |
| Igual (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Greater than or equal to (`>=`) | `ge()` |
| Less than (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| And (`&`) | `And()` |
| Ou (`|`) | `Or()` |

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

Os resultados recebidos podem ser classificados por colunas especificadas do conjunto de dados do público alvo e em sua ordem (asc/desc), respectivamente.

No exemplo a seguir, dataframe é classificado por &quot;column-a&quot; primeiro em ordem crescente. As linhas com os mesmos valores para &quot;column-a&quot; são classificadas por &quot;column-b&quot; em ordem decrescente.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Escrita básica dos dados {#basic-writing-of-data}

>[!NOTE]
>
>A Organização IMS está definida dentro da `client_context`.

Para gravar dados em Python e R, use um dos seguintes exemplos:

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

Depois de configurar o carregador de `platform_sdk` dados, os dados passam por preparação e são divididos para os conjuntos de dados `train` e `val` . Para saber mais sobre a preparação de dados e a engenharia de recursos, visite a seção sobre preparação de [dados e engenharia](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) de recursos no tutorial para criar uma fórmula usando [!DNL JupyterLab] notebooks.