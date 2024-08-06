---
keywords: Experience Platform;guia do desenvolvedor;Data Science Workspace;tópicos populares;Aprendizado de máquina em tempo real;referência de nó;
solution: Experience Platform
title: Referência do nó de aprendizado de máquina em tempo real
description: Um nó é a unidade fundamental da qual os gráficos são formados. Cada nó executa uma tarefa específica e eles podem ser encadeados usando links para formar um gráfico que representa um pipeline de ML. A tarefa executada por um nó representa uma operação nos dados de entrada, como uma transformação de dados ou esquema, ou uma inferência de aprendizado de máquina. O nó gera o valor transformado ou inferido para o(s) próximo(s) nó(s).
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 9030a5482d4ea2b54426680cef92b89e68ef5b33
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Referência de nó do Real-time Machine Learning (Alpha)

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

>[!IMPORTANT]
>
>O Aprendizado de máquina em tempo real ainda não está disponível para todos os usuários. Esse recurso está em alfa e ainda está sendo testado. Este documento está sujeito a alterações.

Uma nó é a unidade fundamental da qual os gráficos são formados. Cada nó executa uma tarefa específica e podem ser encadeadas usando links para formar um gráfico que representa um pipeline ML. O tarefa executado por uma nó representa uma operação em dados de entrada, como uma transformação de dados ou schema ou uma inferência de aprendizado de máquina. A nó envia o valor transformado ou inferido para as próximas nó(s).

O guia a seguir descreve as nó bibliotecas suportadas para aprendizagem de máquina em tempo real.

## Descobrir nós para uso no pipeline de ML

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

Os nós padrão se baseiam em bibliotecas de ciência de dados de código aberto, como Pandas e ScikitLearn.

### ModelUpload

O nó ModelUpload é um nó de Adobe interno que pega um model_path e carrega o modelo do caminho de modelo local para a loja de blob do Real-time Machine Learning.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode é um nó de Adobe interno que usa uma ID de modelo para obter o modelo ONNX pré-treinado e o usa para pontuar nos dados recebidos.

>[!TIP]
>
>Especifique as colunas na mesma ordem em que você deseja que os dados sejam enviados para o modelo ONNX para pontuação.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

O nó Pandas a seguir permite importar qualquer método `pd.DataFrame` ou qualquer função geral de nível superior de pandas. Para saber mais sobre os métodos Pandas, visite a [documentação sobre métodos Pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Para obter mais informações sobre funções de nível superior, visite o [guia de referência da API Pandas para funções gerais](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

O nó abaixo usa `"import": "map"` para importar o nome do método como uma cadeia de caracteres nos parâmetros, seguido pela inserção dos parâmetros como uma função de mapa. O exemplo abaixo faz isso usando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Depois de colocar o mapa no lugar, você tem a opção de definir `inplace` como `True` ou `False`. Defina `inplace` como `True` ou `False` com base no fato de você querer aplicar ou não a transformação local. Por padrão, `"inplace": False` cria uma nova coluna. O suporte para fornecer um novo nome de coluna está definido para ser adicionado em uma versão subsequente. A última linha `cols` pode ser um único nome de coluna ou uma lista de colunas. Especifique as colunas nas quais deseja aplicar a transformação. Neste exemplo `device` é especificado.

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

O nó ScikitLearn permite importar qualquer modelo ou scaler ScikitLearn ML. Use a tabela abaixo para obter mais informações sobre qualquer um dos valores usados no exemplo:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valor | Descrição |
| --- | --- |
| recursos | Recursos de entrada para o modelo (lista de cadeias de caracteres). <br> Por exemplo: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| rótulo | Nome da coluna de destino (sequência de caracteres). |
| modo | Treinar/testar (sequência de caracteres). |
| model_path | Caminho para o modelo salvo localmente no formato onnx. |
| params.model | Caminho de importação absoluto para o modelo (cadeia de caracteres), por exemplo: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Hiperparâmetros de modelo, consulte a documentação da [API do sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) para obter mais informações. |
| nó_instância.process(data_message_from_previous_nó) | O método `process()` utiliza o DataMsg da nó anterior e aplica-se transformação. Isso depende das nó atuais em uso. |

### Divisão

Use o nó a seguir para dividir o quadro de dados em train e testar passando `train_size` ou `test_size`. Isso retorna um quadro de dados com um índice múltiplo. Você pode acessar treinos e quadros de dados de teste usando o exemplo a seguir, `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Próximas etapas

A próxima etapa é criar nós para usar na pontuação de um modelo de Aprendizado de máquina em tempo real. Para obter mais informações, visite o [Guia do usuário do bloco de anotações de Aprendizado de Máquina em Tempo Real](./rtml-authoring-notebook.md).
