---
keywords: Experience Platform, guia do desenvolvedor, Data Science Workspace, tópicos populares, Aprendizagem de máquina em tempo real, referência do nó;
solution: Experience Platform
title: Referência de nó de aprendizado de máquina em tempo real
topic-legacy: Nodes reference
description: Um nó é a unidade fundamental da formação dos gráficos. Cada nó executa uma tarefa específica e pode ser encadeado usando links para formar um gráfico que representa um pipeline ML. A tarefa executada por um nó representa uma operação em dados de entrada, como uma transformação de dados ou esquema ou uma inferência de aprendizado de máquina. O nó gera o valor transformado ou inferido para o(s) próximo(s) nó(s).
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# Referência do nó de aprendizado de máquina em tempo real (Alpha)

>[!IMPORTANT]
>
>O Aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a alterações.

Um nó é a unidade fundamental da formação dos gráficos. Cada nó executa uma tarefa específica e pode ser encadeado usando links para formar um gráfico que representa um pipeline ML. A tarefa executada por um nó representa uma operação em dados de entrada, como uma transformação de dados ou esquema ou uma inferência de aprendizado de máquina. O nó gera o valor transformado ou inferido para o(s) próximo(s) nó(s).

O guia a seguir descreve as bibliotecas de nós compatíveis para o Aprendizado de máquina em tempo real.

## Descobrir nós para uso em seu pipeline ML

Copie o código a seguir em um bloco de anotações [!DNL Python] para exibir todos os nós disponíveis para uso.

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

Nós padrão criados em bibliotecas de dados de código aberto como Pandas e ScikitLearn.

### ModelUpload

O nó ModelUpload é um nó Adobe interno que pega um model_path e carrega o modelo do caminho do modelo local para o repositório de blob de aprendizado de máquina em tempo real.

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

O nó Paindas a seguir permite importar qualquer método `pd.DataFrame` ou qualquer função de nível superior de painéis gerais. Para saber mais sobre os métodos do Pandas, visite a [documentação sobre métodos dos Paindas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Para obter mais informações sobre funções de nível superior, visite o [Guia de referência da API dos painéis para funções gerais](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

O nó abaixo usa `"import": "map"` para importar o nome do método como uma string nos parâmetros, seguida por inserir os parâmetros como uma função de mapa. O exemplo abaixo faz isso usando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Depois de colocar o mapa no lugar, você tem a opção de definir `inplace` como `True` ou `False`. Defina `inplace` como `True` ou `False` com base em se deseja aplicar transformação no local ou não. Por padrão, `"inplace": False` cria uma nova coluna. O suporte para fornecer um novo nome de coluna é definido para ser adicionado em uma versão subsequente. A última linha `cols` pode ser um nome de coluna único ou uma lista de colunas. Especifique as colunas em que deseja aplicar a transformação. Neste exemplo, `device` é especificado.

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
| recursos | Insira recursos no modelo (lista de cadeias de caracteres). <br> Por exemplo: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Nome da coluna de destino (sequência de caracteres). |
| modo | Comboio/ensaio (corda). |
| model_path | Caminho para o modelo salvo localmente no formato onnx. |
| params.model | Caminho de importação absoluto para o modelo (cadeia de caracteres) por exemplo: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Modelos de hiperparâmetros, consulte a documentação da [sklearn API (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) para obter mais informações. |
| node_instance.process(data_message_from_previous_node) | O método `process()` pega DataMsg do nó anterior e aplica a transformação. Depende do nó atual que está sendo usado. |

### Dividir

Use o seguinte nó para dividir o dataframe em um trem e testar passando `train_size` ou `test_size`. Isso retorna um dataframe com um índice múltiplo. Você pode acessar dados de trem e teste usando o exemplo a seguir, `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Próximas etapas

A próxima etapa é criar nós para uso na classificação de um modelo de Aprendizagem de máquina em tempo real. Para obter mais informações, visite o [Guia do usuário do notebook Aprendizagem de máquina em tempo real](./rtml-authoring-notebook.md).
