---
keywords: Experience Platform;página inicial;tópicos populares;acesso a dados;python sdk;api de acesso a dados;read python;write python
solution: Experience Platform
title: Acesso a dados usando o Python no Data Science Workspace
type: Tutorial
description: O documento a seguir contém exemplos sobre como acessar dados no Python para usar no Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Acesso a dados usando o Python no Data Science Workspace

O documento a seguir contém exemplos de como acessar dados usando o Python para usar no Data Science Workspace. Para obter informações sobre como acessar dados usando notebooks JupyterLab, visite o [Acesso aos dados de notebooks JupyterLab](../jupyterlab/access-notebook-data.md) documentação.

## Ler um conjunto de dados

Depois de definir as variáveis de ambiente e concluir a instalação, seu conjunto de dados agora pode ser lido no quadro de dados pandas.

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

A cláusula DISTINCT permite buscar todos os valores distintos em nível de linha/coluna, removendo todos os valores duplicados da resposta.

Um exemplo de uso da variável `distinct()` pode ser vista abaixo:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### Cláusula WHERE

Você pode usar determinados operadores no Python para ajudar a filtrar seu conjunto de dados.

>[!NOTE]
>
>As funções usadas para filtragem diferenciam maiúsculas de minúsculas.

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

A cláusula ORDER BY permite que os resultados recebidos sejam classificados por uma coluna especificada em uma ordem específica (crescente ou decrescente). Isso é feito usando o `sort()` função.

Um exemplo de uso da variável `sort()` pode ser vista abaixo:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Cláusula LIMIT

A cláusula LIMIT permite limitar o número de registros recebidos do conjunto de dados.

Um exemplo de uso da variável `limit()` pode ser vista abaixo:

```python
df = dataset_reader.limit(100).read()
```

### cláusula OFFSET

A cláusula OFFSET permite que você ignore linhas, desde o início, para começar a retornar linhas de um ponto posterior. Em combinação com LIMIT, pode ser usado para iterar linhas em blocos.

Um exemplo de uso da variável `offset()` pode ser vista abaixo:

```python
df = dataset_reader.offset(100).read()
```

## Gravação de um conjunto de dados

Para gravar em um conjunto de dados, você precisa fornecer o quadro de dados pandas ao seu conjunto de dados.

### Gravação do quadro de dados dos pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Diretório do espaço de usuário (Checkpoint)

Para jobs de execução mais longa, talvez seja necessário armazenar etapas intermediárias. Em instâncias como essa, você pode ler e gravar em um espaço de usuário.

>[!NOTE]
>
>Os caminhos para os dados são **não** armazenados. Você precisa armazenar o caminho correspondente para seus respectivos dados.

### Gravar no espaço de usuário

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

O Espaço de trabalho de ciência de dados da Adobe Experience Platform fornece uma amostra de fórmula que usa as amostras de código acima para ler e gravar dados. Se quiser saber mais sobre como usar o Python para acessar seus dados, reveja o [Repositório GitHub do Python do Espaço de trabalho de ciência de dados](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
