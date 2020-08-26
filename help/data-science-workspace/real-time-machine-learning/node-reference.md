---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real-time Machine Learning;node reference;
solution: Experience Platform
title: Guia de referência dos nós de aprendizado de máquina em tempo real
topic: Nodes reference
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# Guia de referência dos nós de aprendizado de máquina em tempo real (Alpha)

>[!IMPORTANT]
>
>O aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a mudanças.

Um nó é a unidade fundamental da qual os gráficos são formados. Cada nó executa uma tarefa específica e eles podem ser encadeados juntos usando links para formar um gráfico que representa um pipeline ML. A tarefa executada por um nó representa uma operação em dados de entrada, como uma transformação de dados ou schema, ou uma inferência de aprendizado de máquina. O nó gera o valor transformado ou inferido para os próximos nós.

O guia a seguir descreve as bibliotecas de nós compatíveis para o aprendizado de máquina em tempo real.

## Descobrindo nós para uso em seu pipeline ML

Copie o seguinte código em um [!DNL Python] notebook para visualização de todos os nós disponíveis para uso.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Exemplo de resposta**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## Nós padrão

Os nós padrão baseiam-se em bibliotecas de dados de código aberto, como Pandas e ScikitLearn.

### ModelUpload

O nó ModelUpload é um nó Adobe interno que pega um model_path e carrega o modelo do caminho do modelo local para a loja de blob de aprendizado de máquina em tempo real.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

O ONNXNode é um nó Adobe interno que utiliza uma ID de modelo para obter o modelo ONNX pré-treinado e o usa para pontuar nos dados recebidos.

>[!TIP]
>
>Especifique as colunas na mesma ordem em que deseja que os dados sejam enviados para o modelo ONNX para pontuação.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

O nó Paindas a seguir permite importar qualquer `pd.DataFrame` método ou qualquer função de nível superior de painéis gerais. Para saber mais sobre os métodos do Pandas, visite a documentação [dos métodos do](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)Pandas. Para obter mais informações sobre as funções de nível superior, visite o guia de referência da API [Pandas para obter funções](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)gerais.

O nó abaixo usa `"import": "map"` para importar o nome do método como uma string nos parâmetros, seguido de inserir os parâmetros como uma função de mapa. O exemplo abaixo faz isso usando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Depois de colocar o mapa no lugar, você tem a opção de definir `inplace` como `True` ou `False`. Defina `inplace` como `True` ou `False` com base em se deseja aplicar a transformação no local ou não. Por padrão, `"inplace": False` cria uma nova coluna. O suporte para fornecer um novo nome de coluna está definido para ser adicionado em uma versão subsequente. A última linha `cols` pode ser um nome de coluna único ou uma lista de colunas. Especifique as colunas nas quais deseja aplicar a transformação. Neste exemplo, `device` é especificado.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

O nó ScikitLearn permite importar qualquer modelo ou escalador ScikitLearn ML. Use a tabela abaixo para obter mais informações sobre qualquer um dos valores usados no exemplo:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valor | Descrição |
| --- | --- |
| feições | Recursos de entrada no modelo (lista de strings). <br> Por exemplo: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Nome da coluna do público alvo (string). |
| modo | Comboio/ensaio (corda). |
| model_path | Caminho para o modelo salvo localmente no formato onnx. |
| params.model | Caminho de importação absoluto para o modelo (string), por exemplo: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Modelos de hiperparâmetros, consulte a documentação da API [sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) para obter mais informações. |
| node_instance.process(data_message_from_previous_node) | O método `process()` pega DataMsg do nó anterior e aplica a transformação. Isso depende do nó atual que está sendo usado. |

### Dividir

Use o nó a seguir para dividir seu dataframe em um trem e teste, passando `train_size` ou `test_size`. Isso retorna um dataframe com um índice múltiplo. Você pode acessar os dados do trem e do teste usando o exemplo a seguir `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Próximas etapas

A próxima etapa é criar nós para uso na pontuação de um modelo de aprendizado de máquina em tempo real. Para obter mais informações, visite o guia [do usuário do notebook Aprendizagem de máquina em tempo](./rtml-authoring-notebook.md)real.
