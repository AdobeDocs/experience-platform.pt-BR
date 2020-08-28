---
keywords: Experience Platform;home;popular topics;data access;python sdk;data access api
solution: Experience Platform
title: SDK seguro de acesso a dados Python
topic: tutorial
description: O Secure Python Data Access SDK é um kit de desenvolvimento de software que permite a leitura e a gravação de conjuntos de dados da Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---


# SDK seguro [!DNL Python] [!DNL Data Access]

O Secure [!DNL Python] [!DNL Data Access] SDK é um kit de desenvolvimento de software que permite a leitura e a gravação de conjuntos de dados da Adobe Experience Platform.

## Introdução

Você deve ter concluído o tutorial de [autenticação](../../tutorials/authentication.md) para ter acesso aos valores para fazer chamadas ao SDK seguro [!DNL Python][!DNL Data Access] :

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. O uso do [!DNL Python] SDK requer o nome e a ID da caixa de proteção na qual a operação ocorrerá:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

## configuração do ambiente

Por padrão, os pontos finais do serviço são definidos como pontos finais do ambiente de integração. Como resultado, para apontar para a produção, defina as seguintes variáveis de ambiente para os seguintes valores:

| Variable | Ponto final |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

Além disso, suas credenciais podem ser adicionadas como variáveis de ambiente.

| Variable | Valor |
| -------- | ----- |
| `ORG_ID` | Sua `{IMS_ORG}` ID. |
| `SERVICE_API_KEY` | Seu `{API_KEY}` valor. |
| `USER_TOKEN` | Seu `{ACCESS_TOKEN}` valor. |
| `SERVICE_TOKEN` | Seu `{SERVICE_TOKEN}`, que pode ser necessário autorizar solicitações de canal retroativo entre serviços. |
| `SANDBOX_ID` | O `{SANDBOX_ID}` valor da sua caixa de proteção. |
| `SANDBOX_NAME` | O `{SANDBOX_NAME}` valor da sua caixa de proteção. |

## Instalação

Todos os pacotes são enviados para `./dist` depois da construção.

### Roda

```python
python3 setup.py bdist_wheel --universal
```

A partir do diretório do projeto, carregue a roda no seu [!DNL Python] ambiente 3.

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### Arquivo de ovos

```python
python3 setup.py bdist_egg
```

## Lendo um conjunto de dados

Depois de definir as variáveis de ambiente e concluir a instalação, o conjunto de dados agora pode ser lido no dataframe dos pandas.

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### SELECIONAR colunas do conjunto de dados

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Obter informações de particionamento:

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Cláusula DISTINCT

A cláusula DISTINCT permite buscar todos os valores distintos em um nível de linha/coluna, removendo todos os valores de duplicado da resposta.

Um exemplo de uso da `distinct()` função pode ser visto abaixo:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### cláusula WHERE

O [!DNL Python] SDK oferece suporte a determinados operadores para ajudar a filtrar o conjunto de dados.

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

A cláusula ORDER BY permite que os resultados recebidos sejam classificados por uma coluna especificada em uma ordem específica (crescente ou decrescente). No [!DNL Python] SDK, isso é feito usando a `sort()` função.

Um exemplo de uso da `sort()` função pode ser visto abaixo:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Cláusula LIMIT

A cláusula LIMIT permite que os usuários limitem o número de registros recebidos do conjunto de dados.

Um exemplo de uso da `limit()` função pode ser visto abaixo:

```python
df = dataset_reader.limit(100).read()
```

### Cláusula OFFSET

A cláusula OFFSET permite que os usuários pulem linhas, do início, para o start de linhas que retornam de um ponto posterior. Em combinação com LIMIT, isso pode ser usado para iterar linhas em blocos.

Um exemplo de uso da `offset()` função pode ser visto abaixo:

```python
df = dataset_reader.offset(100).read()
```

## Gravando um conjunto de dados

O [!DNL Python] SDK suporta a gravação de conjuntos de dados. Os usuários precisarão fornecer os dados dos pandas que precisam ser gravados no conjunto de dados.

### Gravando os dados dos pandas

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Diretório do espaço de usuário (Ponto de verificação)

Para trabalhos em execução mais longa, os usuários podem precisar armazenar etapas intermediárias. Em instâncias como essa, o [!DNL Python] SDK fornece ao usuário a capacidade de ler e gravar em um espaço de usuário.

>[!NOTE]
>
>Os caminhos para os dados **não** são armazenados pelo SDK. Os usuários precisarão armazenar o caminho correspondente para seus respectivos dados.

### Gravar no espaço do usuário

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Ler do espaço de usuário

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
