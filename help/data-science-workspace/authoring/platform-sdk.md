---
keywords: Experience Platform;guia do desenvolvedor;SDK;Data Access SDK;Data Science Workspace;tópicos populares;;developer guide;SDK;Data Access SDK;Data Science;popular topics
solution: Experience Platform
title: Criação de modelo usando o SDK da plataforma Adobe Experience Platform
description: Este tutorial fornece informações sobre a conversão de data_access_sdk_python para o novo Python platform_sdk no Python e no R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# Criação de modelo usando o Adobe Experience Platform [!DNL Platform] SDK

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial fornece informações sobre como converter `data_access_sdk_python` para o novo Python `platform_sdk` em Python e R. Este tutorial fornece informações sobre as seguintes operações:

- [Compilar autenticação](#build-authentication)
- [Leitura básica de dados](#basic-reading-of-data)
- [Gravação básica de dados](#basic-writing-of-data)

## Autenticação de compilação {#build-authentication}

Authentication é necessário fazer chamadas [!DNL Adobe Experience Platform]e é composto por chave de API, ID da organização, um token de usuário e um token de serviço.

### Python

Se você estiver usando o Notebook Jupyter, use o código abaixo para build:`client_context`

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Se você não estiver usando o Notebook Jupyter ou precisar alterar a organização, use a amostra de código abaixo:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Se você estiver usando o Notebook Jupyter, use o código abaixo para build:`client_context`

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Se você não estiver usando o Notebook Jupyter ou precisar alterar a organização, use a amostra de código abaixo:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Leitura básica dos dados {#basic-reading-of-data}

Com o novo [!DNL Platform] SDK, o tamanho máximo de leitura é de 32 GB, com tempo máximo de leitura de 10 minutos.

Se o tempo de leitura estiver demorando muito, você pode tentar usar uma das seguintes opções de filtragem:

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

O novo [!DNL Platform] SDK suporta as seguintes operações:

| Operação | Função |
| --------- | -------- |
| Igual a (`=`) | `eq()` |
| Maior que (`>`) | `gt()` |
| Maior ou igual a (`>=`) | `ge()` |
| Menor que (`<`) | `lt()` |
| Menor que ou igual a (`<=`) | `le()` |
| E (`&`) | `And()` |
| Ou (`|`) | `Or()` |

## Filtrar por colunas selecionadas {#filter-by-selected-columns}

Para refinar ainda mais sua leitura de dados, também é possível filtrar por nome de coluna.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Obter resultados classificados {#get-sorted-results}

Os resultados recebidos podem ser classificados por colunas especificadas da Direcionamento conjunto de dados e em suas solicitar (asc/desc), respectivamente.

No exemplo a seguir, o período de dados é classificado por &quot;column-a&quot; primeiro em solicitar crescentes. As linhas que tiverem os mesmos valores para &quot;column-a&quot; são classificadas por &quot;column-b&quot; em solicitar decrescente.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Escrita básica de dados {#basic-writing-of-data}

>[!NOTE]
>
>A organização está definida na variável `client_context`.

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

Depois de configurar o carregador de dados `platform_sdk`, os dados serão preparados e divididos nos conjuntos de dados `train` e `val`. Para saber mais sobre preparação de dados e engenharia de recursos, visita a seção sobre [preparação de dados e engenharia](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) de recursos no tutorial de criação de fórmula uso de [!DNL JupyterLab] notebooks.
