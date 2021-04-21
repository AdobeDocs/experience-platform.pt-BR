---
keywords: Experience Platform, guia do desenvolvedor, SDK, SDK de acesso a dados, Data Science Workspace, tópicos populares
solution: Experience Platform
title: Criação de modelos usando o SDK da plataforma Adobe Experience Platform
topic-legacy: SDK authoring
description: Este tutorial fornece informações sobre a conversão de data_access_sdk_python para a nova plataforma Python_sdk em Python e R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Criação de modelo usando o SDK [!DNL Platform] do Adobe Experience Platform

Este tutorial fornece informações sobre a conversão de `data_access_sdk_python` para o novo Python `platform_sdk` em Python e R. Este tutorial fornece informações sobre as seguintes operações:

- [Autenticação de build](#build-authentication)
- [Leitura básica dos dados](#basic-reading-of-data)
- [Escrita básica de dados](#basic-writing-of-data)

## Autenticação de compilação {#build-authentication}

A autenticação é necessária para fazer chamadas para [!DNL Adobe Experience Platform] e é composta de Chave de API, ID de Org de IMS, um token de usuário e um token de serviço.

### Python

Se você estiver usando o Bloco de Anotações do Jupyter, use o código abaixo para criar o `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Se você não estiver usando o Jupyter Notebook ou precisar alterar a IMS Org, use a amostra de código abaixo:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Se você estiver usando o Bloco de Anotações do Jupyter, use o código abaixo para criar o `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Se você não estiver usando o Jupyter Notebook ou precisar alterar a IMS Org, use a amostra de código abaixo:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Leitura básica de dados {#basic-reading-of-data}

Com o novo SDK [!DNL Platform], o tamanho máximo de leitura é de 32 GB, com um tempo máximo de leitura de 10 minutos.

Se o tempo de leitura estiver demorando muito, tente usar uma das seguintes opções de filtragem:

- [Filtrar dados por deslocamento e limite](#filter-by-offset-and-limit)
- [Filtrar dados por data](#filter-by-date)
- [Filtrar dados por coluna](#filter-by-selected-columns)
- [Obter resultados classificados](#get-sorted-results)

>[!NOTE]
>
>A Organização IMS é definida no `client_context`.

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

## Filtrar por deslocamento e limitar {#filter-by-offset-and-limit}

Como a filtragem por ID de lote não é mais suportada, para escopo da leitura de dados, é necessário usar `offset` e `limit`.

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

O novo SDK [!DNL Platform] oferece suporte às seguintes operações:

| Operação | Função |
| --------- | -------- |
| Igual a (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Greater than or equal to (`>=`) | `ge()` |
| Less than (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| E (`&`) | `And()` |
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

Os resultados recebidos podem ser classificados por colunas especificadas do conjunto de dados de destino e em sua ordem (asc/desc), respectivamente.

No exemplo a seguir, o dataframe é classificado por &quot;coluna-a&quot; primeiro em ordem crescente. As linhas que têm os mesmos valores para &quot;coluna-a&quot; são classificadas por &quot;coluna-b&quot; em ordem decrescente.

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
>A Organização IMS é definida no `client_context`.

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

Depois de configurar o carregador de dados `platform_sdk`, os dados são preparados e divididos nos conjuntos de dados `train` e `val`. Para saber mais sobre a preparação de dados e a engenharia de recursos, visite a seção sobre [preparação de dados e engenharia de recursos](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) no tutorial para criar uma fórmula usando blocos de anotações [!DNL JupyterLab].
