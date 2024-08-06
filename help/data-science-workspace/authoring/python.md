---
keywords: Experience Platform; Casa; tópicos populares; acesso a dados; python sdk; api de acesso a dados; ler python; escrever python
solution: Experience Platform
title: Acessando dados usando Python em data science Área de trabalho
type: Tutorial
description: A documento a seguir contém exemplos sobre como acessar dados em Python para usar em Área de trabalho de ciência de dados.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Acessando dados usando Python em data science Área de trabalho

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

A documento a seguir contém exemplos sobre como acessar dados usando Python para usar em Área de trabalho de ciência de dados. Para obter informações sobre como acessar dados usando notebooks JupyterLab, visita a documentação de acesso](../jupyterlab/access-notebook-data.md) a dados dos [notebooks JupyterLab.

## Leitura de uma conjunto de dados

Depois de definir as variáveis ambiente e concluir a instalação, seus conjunto de dados agora podem ser lidos no dataframe dos pandas.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### SELECIONAR colunas no conjunto de dados

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Obtenha informações de particionamento:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Cláusula DISTINTA

A cláusula DISTINCT permite buscar todos os valores distintos em um nível de linha/coluna, removendo todos os valores duplicado da resposta.

Um exemplo do uso da `distinct()` função pode ser visto abaixo:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### CLÁUSULA ONDE

Você pode usar certos operadores em Python para ajudar a filtrar suas conjunto de dados.

>[!NOTE]
>
>As funções usadas para filtragem são diferencia maiúsculas de minúsculas.

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

### ORDEM POR cláusula

A cláusula ORDEM POR permite que os resultados recebidos sejam classificados por uma coluna especificada em uma solicitar específica (crescente ou decrescente). Isso é feito usando a `sort()` função.

Um exemplo do uso da `sort()` função pode ser visto abaixo:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Cláusula de LIMITE

A cláusula limite permite limitar o número de registros recebidos do conjunto de dados.

Um exemplo do uso da `limit()` função pode ser visto abaixo:

```python
df = dataset_reader.limit(100).read()
```

### Cláusula de DESLOCAMENTO

A cláusula OFFSET permite que você pule linhas, desde o início, para start linhas recorrentes a partir de um ponto posterior. Em combinação com o LIMITE, isso pode ser usado para iterar linhas em blocos.

Um exemplo do uso da `offset()` função pode ser visto abaixo:

```python
df = dataset_reader.offset(100).read()
```

## Escrever uma conjunto de dados

Para escrever a um conjunto de dados, você precisa fornecer o período de dados dos pandas ao seu conjunto de dados.

### Escrevendo o dataframe dos pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Diretório do userspace (Ponto de verificação)

Para trabalhos mais longos, talvez seja necessário armazenamento etapas intermediárias. Em casos curtir isso, você pode ler e gravar em um espaço de usuário.

>[!NOTE]
>
>Os caminhos para os dados não **são** armazenados. É necessário armazenamento o caminho correspondente aos seus respectivos dados.

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

Adobe Experience Platform Data Science Área de trabalho fornece uma amostra fórmula que usa as amostras de código acima para ler e gravar dados. Se você quiser saber mais sobre como usar Python para acessar seus dados, consulte o [repositório](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail) Python GitHub Área de trabalho Data Science.
