---
keywords: Experience Platform;home;popular topics;acesso aos dados;python sdk;acesso aos dados api;read python;write python;;home;popular topics;data access;python sdk;data access api;read python;write python;write python;write python
solution: Experience Platform
title: Acessar dados usando Python na Data Science Workspace
topic: tutorial
type: Tutorial
description: O documento a seguir contém exemplos de como acessar dados no Python para uso na Data Science Workspace.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---


# Acessar dados usando Python na Data Science Workspace

O documento a seguir contém exemplos de como acessar dados usando o Python para uso na Data Science Workspace. Para obter informações sobre como acessar dados usando notebooks JupyterLab, visite a documentação [Acesso aos notebooks JupyterLab](../jupyterlab/access-notebook-data.md).

## Lendo um conjunto de dados

Depois de definir as variáveis de ambiente e concluir a instalação, seu conjunto de dados pode ser lido no dataframe dos pandas.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### SELECIONAR colunas do conjunto de dados

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Obter informações de particionamento:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Cláusula DISTINCT

A cláusula DISTINCT permite buscar todos os valores distintos em um nível de linha/coluna, removendo todos os valores de duplicado da resposta.

Um exemplo de uso da função `distinct()` pode ser visto abaixo:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### cláusula WHERE

Você pode usar determinados operadores no Python para ajudar a filtrar seu conjunto de dados.

>[!NOTE]
>
>As funções usadas para filtragem fazem distinção entre maiúsculas e minúsculas.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Um exemplo do uso dessas funções de filtragem pode ser visto abaixo:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### Cláusula ORDER BY

A cláusula ORDER BY permite que os resultados recebidos sejam classificados por uma coluna especificada em uma ordem específica (crescente ou decrescente). Isso é feito usando a função `sort()`.

Um exemplo de uso da função `sort()` pode ser visto abaixo:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Cláusula LIMIT

A cláusula LIMIT permite limitar o número de registros recebidos do conjunto de dados.

Um exemplo de uso da função `limit()` pode ser visto abaixo:

```python
df = dataset_reader.limit(100).read()
```

### Cláusula OFFSET

A cláusula OFFSET permite ignorar linhas, do início, para start de linhas que retornam de um ponto posterior. Em combinação com LIMIT, isso pode ser usado para iterar linhas em blocos.

Um exemplo de uso da função `offset()` pode ser visto abaixo:

```python
df = dataset_reader.offset(100).read()
```

## Gravando um conjunto de dados

Para gravar em um conjunto de dados, é necessário fornecer os dados dos pandas ao conjunto de dados.

### Gravando os dados dos pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Diretório do espaço de usuário (Ponto de verificação)

Para trabalhos em execução mais longa, talvez seja necessário armazenar etapas intermediárias. Em instâncias como esta, você pode ler e gravar em um espaço de usuário.

>[!NOTE]
>
>Os caminhos para os dados estão **armazenados não**. É necessário armazenar o caminho correspondente para seus respectivos dados.

### Gravar no espaço do usuário

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Ler do espaço de usuário

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Próximas etapas

A Adobe Experience Platform Data Science Workspace fornece uma amostra de fórmula que usa as amostras de código acima para ler e gravar dados. Se quiser saber mais sobre como usar o Python para acessar seus dados, consulte [Repositório do Data Science Workspace Python GitHub](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).