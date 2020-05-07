---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Pontuação de um modelo de aprendizado de máquina em tempo real
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Pontuação de um modelo de aprendizado de máquina em tempo real

>[!IMPORTANT]
>O aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a mudanças.

Este tutorial mostra como usar nós de aprendizado de máquina em tempo real para pré-processar os dados recebidos e classificá-los em relação ao modelo ONNX.

>[!IMPORTANT]
> - As funções usadas em nós não podem ser serializadas. Por exemplo, uma função lambda usada em um nó de pandas.
> - Há 60 segundos de espera após a implantação da borda ser feita manualmente. Isso pode ser transferido para o método score_edge de EdgeUtils.


>[!NOTE]
>Para pontuar um modelo para uso em Tempo real em Aprendizagem de máquina, é necessário ter concluído o tutorial anterior sobre como [treinar um modelo para Aprendizado de máquina em tempo real](./training-ml-model.md)

## Criar um novo bloco de anotações

Na interface do usuário da plataforma Adobe Experience, selecione **[!UICONTROL Notebooks]** na *Data Science*. Em seguida, selecione **[!UICONTROL JupyterLab]** e aguarde algum tempo para o ambiente carregar.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Start selecionando o notebook **Python 3** em branco no iniciador JupyterLab.

![pitão em branco](../images/rtml/python-blank.png)

## Importar e descobrir nós

importando todos os pacotes necessários para o seu modelo. Certifique-se de que todos os pacotes que você planeja usar para a criação de nós sejam importados.

>[!NOTE]
>Sua lista de importações pode ser diferente com base no modelo que você fez.

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

Para ver a lista de nós disponíveis, copie e cole o exemplo a seguir no seu notebook.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

A resposta recebida é uma lista de nós.

![lista de notas](../images/rtml/node-list.png)

## Criação de nó para pontuação de borda

Em seguida, é necessário definir e criar um nó para a pontuação da borda. Substitua o `model_id` no exemplo pela ID do modelo que você recebeu ao concluir o treinamento no tutorial [](./training-ml-model.md)anterior. Este exemplo usa o nó Pandas para importar um método pd.DataDrame ou uma função de nível superior de painéis gerais. A função de mapa é importada e usada para criar dois nós. Para obter mais informações sobre os nós disponíveis e como usá-los, visite o guia [de referência do](./node-reference.md)nó.

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## Criar gráfico DSL

Com seus nós criados, a próxima etapa é encadear os nós para criar um gráfico.

Start listando todos os nós que fazem parte do gráfico.

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

Em seguida, conecte os nós com as bordas. Cada tupla é uma conexão de borda.

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

Assim que os nós estiverem conectados, crie o gráfico.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## Publicar na borda

Agora que você criou um gráfico, pode implantá-lo na borda.

>[!IMPORTANT]
>Não publicar na borda com frequência, isso pode sobrecarregar os nós da borda. Não é recomendado publicar o mesmo modelo várias vezes.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## Cliente Edge

Após a publicação para borda, a pontuação é feita por uma solicitação POST de um cliente. Normalmente, isso pode ser feito a partir de um aplicativo cliente que precisa de pontuações ML. Você também pode fazer isso do Postman. Aqui, o EdgeUtils é usado para demonstrar o processo.

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

Quando a pontuação for concluída, o URL da borda, a carga e a saída pontuada da borda serão retornados.

![pontuação concluída](../images/rtml/scoring-complete.png)

## Excluindo um aplicativo implantado da borda (opcional)

>!![CAUTION]
Esta célula é usada para excluir seu aplicativo de borda implantado. Não use a célula a seguir, a menos que seja necessário excluir um aplicativo de borda implantado.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Próximas etapas

Ao seguir o tutorial acima, você marcou e implantou com êxito seu modelo de aprendizado de máquina em tempo real. Se você quiser saber mais sobre os nós disponíveis para a criação de modelo, visite o guia [de referência de](./node-reference.md)nó.



