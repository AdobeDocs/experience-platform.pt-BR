---
keywords: Experience Platform;guia do desenvolvedor;Data Science Workspace;tópicos populares;Aprendizado de máquina em tempo real;referência de nó;
solution: Experience Platform
title: Gerenciar notebooks de aprendizado de máquina em tempo real
description: O guia a seguir descreve as etapas necessárias para criar um aplicativo de aprendizado de máquina em tempo real no Adobe Experience Platform JupyterLab.
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 0%

---

# Gerenciar blocos de anotações do Aprendizado de Máquina em Tempo Real (Alpha)

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

>[!IMPORTANT]
>
>O Machine Learning em tempo real ainda não está disponível para todos os usuários. Esse recurso está na alfa e ainda está sendo testado. Esta documento está sujeita a mudanças.

O guia a seguir descreve as etapas necessárias para build um aplicativo de Aprendizagem de máquina em tempo real. Usando o Adobe Systems notebook ML ]**Python em tempo real fornecido**[!UICONTROL  modelo, este guia aborda treinamento um modelo, a criação de um DSL, a publicação de DSL para o Edge e a pontuação da solicitação. Conforme você avança na implementação do seu modelo de Aprendizado de máquina em tempo real, espera-se modificar o modelo para atender às necessidades do seu conjunto de dados.

## Criar um bloco de anotações do Aprendizado de Máquina em Tempo Real

Na interface do usuário do Adobe Experience Platform, selecione **[!UICONTROL Blocos de Anotações]** em **Ciência de Dados**. Em seguida, selecione **[!UICONTROL JupyterLab]** e aguarde algum tempo para o ambiente ser carregado.

![abrir JupyterLab](../images/rtml/open-jupyterlab.png)

A [!DNL JupyterLab] iniciador é exibida. Role para baixo até *Aprendizado de Máquina em Tempo Real* e selecione o bloco de anotações **[!UICONTROL Aprendizado de Máquina em Tempo Real]**. Um modelo é aberto contendo exemplos de células do bloco de anotações com um exemplo de conjunto de dados.

![Python em branco](../images/rtml/authoring-notebook.png)

## Importar e descobrir nós

Comece importando todos os pacotes necessários para seu modelo. Certifique-se de que qualquer pacote que você planeja usar para a criação de nó seja importado.

>[!NOTE]
>
>A lista de importações pode diferir com base no modelo que você deseja fazer. Essa lista será alterada à medida que novos nós forem adicionados ao longo do tempo. Consulte o [guia de referência do nó](./node-reference.md) para obter uma lista completa dos nós disponíveis.

```python
from pprint import pprint
import pandas as pd
import numpy as np
import json
import uuid
from shutil import copyfile
from pathlib import Path
from datetime import date, datetime, timedelta
from platform_sdk.dataset_reader import DatasetReader

from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_sdk.edge.utils import EdgeUtils
from rtml_sdk.graph.utils import GraphBuilder
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.preprocessing.one_hot_encoder import OneHotEncoder
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.core.datamsg import DataMsg
```

A célula de código a seguir imprime uma lista de nós disponíveis.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![lista de notas](../images/rtml/node-list.png)

## Treinando um modelo de aprendizado de máquina em tempo real

Usando uma das opções a seguir, você gravará o código [!DNL Python] para ler, pré-processar e analisar dados. Em seguida, você precisa treinar seu próprio modelo de ML, serializá-lo no formato ONNX e carregá-lo na loja de modelos do Real-time Machine Learning.

- [Treinando seu próprio modelo em notebooks JupyterLab](#training-your-own-model)
- [Fazer upload de seu próprio modelo ONNX pré-treinado para notebooks JupyterLab](#pre-trained-model-upload)

### Treinando seu próprio modelo {#training-your-own-model}

Comece carregando seus dados de treinamento.

>[!NOTE]
>
>No modelo **ML** em tempo real, o [conjunto de dados CSV de seguro de carro](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) é obtido de [!DNL Github].

![Carregar dados de treinamento](../images/rtml/load_training.png)

Se quiser usar um conjunto de dados dentro do Adobe Experience Platform, remova o comentário da célula abaixo. Em seguida, você precisa substituir `DATASET_ID` pelo valor apropriado.

![conjunto de dados rtml](../images/rtml/rtml-dataset.png)

Para acessar um conjunto de dados no bloco de anotações [!DNL JupyterLab], selecione a guia **Dados** no menu de navegação esquerdo de [!DNL JupyterLab]. Os **[!UICONTROL diretórios Conjuntos]** de dados e **[!UICONTROL Schemas]** são exibidos. Selecione Conjuntos ]**de dados e clique com o botão direito do mouse e selecione**[!UICONTROL  a opção **[!UICONTROL Explorar dados em notebook]** no menu suspenso na conjunto de dados que deseja usar. Uma entrada de código executável aparece na parte inferior do notebook. Essa célula tem o seu `dataset_id`.

![acesso ao conjunto de dados](../images/rtml/access-dataset.png)

Depois de concluído, clique com o botão direito do mouse e exclua a célula gerada na parte inferior do bloco de anotações.

### Propriedades de treinamento

Usando o modelo fornecido, modifique qualquer propriedade de treinamento em `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Preparar seu modelo

Usando o modelo de ML ]**em tempo real**[!UICONTROL  você precisa analisar, pré-processar, treinar e avaliar seu modelo de ML. Isso é feito aplicando transformações de dados e criando um pipeline de treinamento.

**Transformações de dados**

A célula **[!UICONTROL ML]** em tempo real **Transformações de dados** precisa ser modificada para funcionar com seu próprio conjunto de dados. Normalmente, isso envolve renomear colunas, rollup de dados e preparação de dados/engenharia de recursos.

>[!NOTE]
>
>O exemplo a seguir foi condensado para fins de legibilidade usando `[ ... ]`. Exiba e expanda a seção de transformações de dados de modelos de *ML em tempo real* para a célula de código completa.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid': 'ecid',
                     [ ... ]}, inplace=True)
df1 = df1[['ecid', 'km', 'cartype', 'age', 'gender', 'carbrand', 'leasing', 'city', 
       'country', 'nationality', 'primaryuser', 'purchase', 'pricequote', 'timestamp']]
print("df1 shape 1", df1.shape)
#########################################
# Data Rollup
######################################### 
df1['timestamp'] = pd.to_datetime(df1.timestamp)
df1['hour'] = df1['timestamp'].dt.hour.astype(int)
df1['dayofweek'] = df1['timestamp'].dt.dayofweek

df1.loc[(df1['purchase'] == 'yes'), 'purchase'] = 1
df1.purchase.fillna(0, inplace=True)
df1['purchase'] = df1['purchase'].astype(int)

[ ... ]

print("df1 shape 2", df1.shape)

#########################################
# Data Preparation/Feature Engineering
#########################################      

df1['carbrand'] = df1['carbrand'].str.lower()
df1['country'] = df1['country'].str.lower()
df1.loc[(df1['carbrand'] == 'vw'), 'carbrand'] = 'volkswagen'

[ ... ]

df1['age'].fillna(df1['age'].median(), inplace=True)
df1['gender'].fillna('notgiven', inplace=True)

[ ... ]

df1['city'] = df1.groupby('country')['city'].transform(lambda x: x.fillna(x.mode()))
df1.dropna(subset = ['pricequote'], inplace=True)
print("df1 shape 3", df1.shape)
print(df1)

#grouping
grouping_cols = ['carbrand', 'cartype', 'city', 'country']

for col in grouping_cols:
    df_idx = pd.DataFrame(df1[col].value_counts().head(6))

    def grouping(x):
        if x in df_idx.index:
            return x
        else:
            return "Others"
    df1[col] = df1[col].apply(lambda x: grouping(x))

def age(x):
    if x < 20:
        return "u20"
    elif x > 19 and x < 29:
    [ ... ]
    else: 
        return "Others"

df1['age'] = df1['age'].astype(int)
df1['age_bucket'] = df1['age'].apply(lambda x: age(x))

df_final = df1[['hour', 'dayofweek','age_bucket', 'gender', 'city',  
   'country', 'carbrand', 'cartype', 'leasing', 'pricequote', 'purchase']]
print("df final", df_final.shape)

cat_cols = ['age_bucket', 'gender', 'city', 'dayofweek', 'country', 'carbrand', 'cartype', 'leasing']
df_final = pd.get_dummies(df_final, columns = cat_cols)
```

Execute a célula fornecida para ver um resultado de exemplo. A tabela de saída retornada do conjunto de dados `carinsurancedataset.csv` retorna as modificações definidas.

![Exemplo de transformações de dados](../images/rtml/table-return.png)

**Pipeline de treinamento**

Em seguida, é necessário criar o pipeline de treinamento. Isso será semelhante a qualquer outro arquivo de pipeline de treinamento, exceto que você precisa converter e gerar um arquivo ONX.

Usando as transformações de dados definidas na célula anterior, modifique o modelo. O código a seguir destacado abaixo é usado para gerar um arquivo ONNX no pipeline de recursos. Exiba o modelo de *ML em tempo real* para a célula completa do código de pipeline.

```python
#for generating onnx
def generate_onnx_resources(self):        
    install_dir = os.path.expanduser('~/my-workspace')
    print("Generating Onnx")
        
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
        
    # ONNX-ification
    initial_type = [('float_input', FloatTensorType([None, self.feature_len]))]

    print("Converting Model to Onnx")
    onx = convert_sklearn(self.model, initial_types=initial_type)
             
    with open("model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
            
    print("Model onnx created")
```

Depois de concluir seu pipeline de treinamento e modificar seus dados por meio de transformações de dados, use a seguinte célula para executar o treinamento.

```python
model = train(config_properties, df_final)
```

### Gerar e fazer upload de um modelo ONX

Depois de concluir um treinamento bem-sucedido, você precisará gerar um modelo ONX e fazer upload do modelo treinado para a loja de modelos do Real-time Machine Learning. Depois de executar as células a seguir, o modelo ONNX aparecerá no painel esquerdo ao lado de todos os outros notebooks.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>Altere o valor da cadeia de caracteres `model_path` (`model.onnx`) para alterar o nome do seu modelo.

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>A célula a seguir não é editável nem excluível e é necessária para que seu aplicativo de Aprendizado de máquina em tempo real funcione.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![Modelo ONNX](../images/rtml/onnx-model-rail.png)

### Fazer upload de seu próprio modelo ONNX pré-treinado {#pre-trained-model-upload}

Usando o botão de carregamento localizado em blocos de anotações [!DNL JupyterLab], carregue seu modelo ONX pré-treinado para o ambiente de blocos de anotações [!DNL Data Science Workspace].

![ícone de carregamento](../images/rtml/upload.png)

Próximo, altere o valor da `model_path` sequência de caracteres no notebook ML em *tempo real* para corresponder ao nome do seu modelo ONNX. Após a conclusão, execute a célula Definir caminho *do* modelo e execute o Upload do *modelo para a célula Armazenamento* de modelo RTML. A localização do modelo e a ID do modelo são retornadas na resposta quando bem-sucedidas.

![fazer upload do próprio modelo](../images/rtml/upload-own-model.png)

## Criação de idioma específico de domínio (DSL)

Esta seção descreve a criação de um DSL. Você criará os nós que incluem qualquer pré-processamento de dados junto com o ONNX nó. Próximo, um gráfico DSL é criado usando nós e bordas. As bordas conectam nós usando o formato baseado em tupla (node_1, node_2). O gráfico não deve ter ciclos.

>[!IMPORTANT]
>
>O uso do nó ONX é obrigatório. Sem o nó ONX, o aplicativo não terá êxito.

### Criação de nós

>[!NOTE]
>
> É provável que você tenha vários nós com base no tipo de dados que está sendo usado. O exemplo a *seguir descreve apenas uma única nó na modelo ML* em tempo real. Visualização a *seção Criação de nós de modelos**ML* em tempo real para a célula de código completa.

O nó Pandas abaixo usa `"import": "map"` para importar o nome do método como uma cadeia de caracteres nos parâmetros, seguido pela inserção dos parâmetros como uma função de mapa. O exemplo abaixo faz isso usando `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. Depois de colocar o mapa no lugar, você tem a opção de definir `inplace` como `True` ou `False`. Defina `inplace` como `True` ou `False` com base no fato de você querer aplicar ou não a transformação local. Por padrão, `"inplace": False` cria uma nova coluna. O suporte para fornecer um novo nome de coluna está definido para ser adicionado em uma versão subsequente. A última linha `cols` pode ser um único nome de coluna ou uma lista de colunas. Especifique as colunas nas quais deseja aplicar a transformação. Neste exemplo, `leasing` está especificado. Para obter mais informações sobre os nós disponíveis e como usá-los, consulte o [manual de referência do nó](./node-reference.md).

```python
# Renaming leasing column using Pandas Node
leasing_mapper_node = Pandas(params={'import': 'map',
                                'kwargs': {'arg': {
                                    'dataLayerNull': 'notgiven', 
                                    'no': 'no', 
                                    'yes': 'yes', 
                                    'notgiven': 'notgiven'}},
                                'inplace': True,
                                'cols': 'leasing'})
```

### Criar o gráfico DSL

Com os nós criados, a próxima etapa é encadear os nós para criar um gráfico.

Comece listando todos os nós que fazem parte do gráfico criando uma matriz.

```python
nodes = [json_df_node, 
        to_datetime_node,
        hour_node,
        dayofweek_node,
        age_fillna_node,
        carbrand_fillna_node,
        country_fillna_node,
        cartype_primary_nationality_km_fillna_node,
        carbrand_mapper_node,
        cartype_mapper_node,
        country_mapper_node,
        gender_mapper_node,
        leasing_mapper_node,
        age_to_int_node,
        age_bins_node,
        dummies_node, 
        onnx_node]
```

Em seguida, conecte os nós com bordas. Cada tupla é uma conexão [!DNL Edge].

>[!TIP]
>
> Como os nós são linearmente dependentes uns dos outros (cada nó depende da saída do nó anterior), você pode criar links usando uma compreensão de lista Python simples. Adicione suas próprias conexões se um nó depender de várias entradas.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

Depois que os nós estiverem conectados, crie o gráfico. A célula abaixo é obrigatória e não pode ser editada ou excluída.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

Uma vez concluído, um objeto `edge` é retornado contendo cada um dos nós e os parâmetros que foram mapeados para eles.

![retorno de borda](../images/rtml/edge-return.png)

## Publish para Edge (Hub)

>[!NOTE]
>
>O Aprendizado de máquina em tempo real é temporariamente implantado e gerenciado pelo Hub do Adobe Experience Platform. Para obter detalhes adicionais, visite a seção de visão geral sobre a [Arquitetura do Real-time Machine Learning](./home.md#architecture).

Agora que você criou um gráfico DSL, é possível implantar seu gráfico no [!DNL Edge].

>[!IMPORTANT]
>
>Não publique no [!DNL Edge] com frequência. Isso pode sobrecarregar os nós [!DNL Edge]. Não é recomendável publicar o mesmo modelo várias vezes.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### Atualizando seu DSL e republicando para o Edge (opcional)

Se não precisar atualizar seu DSL, você pode pular para [pontuação](#scoring).

>[!NOTE]
>
>As células a seguir serão necessárias somente se você desejar atualizar uma DSL existente que foi publicada no Edge.

Seus modelos provavelmente continuarão a se desenvolver. Em vez de criar um serviço totalmente novo, é possível atualizar um serviço existente com o novo modelo. Você pode definir um nó que deseja atualizar, atribuir uma nova ID a ele e, em seguida, recarregar o novo DSL para o [!DNL Edge].

No exemplo abaixo, o nó 0 é atualizado com uma nova ID.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![Nó atualizado](../images/rtml/updated-node.png)

Depois de atualizar a ID do nó, você poderá republicar uma DSL atualizada na Edge.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

Você receberá o DSL atualizado.

![DSL](../images/rtml/updated-dsl.png) atualizado

## Pontuação {#scoring}

Depois de publicar em [!DNL Edge], a pontuação é feita por uma solicitação POST de um cliente. Normalmente, isso pode ser feito a partir de um aplicativo cliente que precisa de pontuações de ML. Também é possível fazer isso no Postman. O modelo **[!UICONTROL ML]** em tempo real usa EdgeUtils para demonstrar esse processo.

>[!NOTE]
>
>É necessário um pequeno tempo de processamento antes de iniciar a pontuação.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Usando o mesmo schema usado no treinamento, são gerados dados de pontuação de amostra. Esses dados são usados para criar um quadro de dados de pontuação e, em seguida, convertidos em um dicionário de pontuação. Exiba o modelo de *ML em tempo real* para a célula de código completa.

![Dados de pontuação](../images/rtml/generate-score-data.png)

### Pontuação em relação ao endpoint do Edge

Use a seguinte célula no modelo de *ML* em tempo real para pontuar em relação ao serviço [!DNL Edge].

![Pontuação em relação à borda](../images/rtml/scoring-edge.png)

Quando a pontuação for concluída, a URL, a Carga e a saída pontuada de [!DNL Edge] de [!DNL Edge] serão retornadas.

## Listar os aplicativos implantados no [!DNL Edge]

Para gerar uma lista de aplicativos implantados no momento no [!DNL Edge], execute a seguinte célula de código. Esta célula não pode ser editada ou excluída.

```python
services = edge_utils.list_deployed_services()
print(services)
```

A resposta retornada é uma matriz dos serviços implantados.

```json
[
    {
        "created": "2020-05-25T19:18:52.731Z",
        "deprecated": false,
        "id": "40eq76c0-1c6f-427a-8f8f-54y9cdf041b7",
        "type": "edge",
        "updated": "2020-05-25T19:18:52.731Z"
    }
]
```

## Excluir um aplicativo ou ID de serviço implantado de [!DNL Edge] (opcional)

>[!CAUTION]
>
>Essa célula é usada para excluir o aplicativo Edge implantado. Não use a seguinte célula, a menos que precise excluir um aplicativo [!DNL Edge] implantado.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Próximas etapas

Ao seguir o tutorial acima, você treinou e carregou com sucesso um modelo ONX para a loja de modelos do Real-time Machine Learning. Além disso, você pontuou e implantou seu modelo de Aprendizagem de máquina em tempo real. Se quiser saber mais sobre os nós disponíveis para criação de modelos, visita o [guia](./node-reference.md) de referência nó.
