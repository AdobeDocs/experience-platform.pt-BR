---
title: Determine Uma Pontuação De Propensão Usando Um Modelo Preditivo Gerado Por Aprendizado De Máquina
description: Saiba como usar o Serviço de query para aplicar seu modelo preditivo aos dados da plataforma. Este documento demonstra como usar os dados da plataforma para prever a propensão de compra de um cliente em cada visita.
source-git-commit: af1c8f94d1758b3a4e7ea00c46b0f9a71a01c6be
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Determine uma pontuação de propensão usando um modelo preditivo gerado por aprendizado automatizado

Usando o Serviço de query, você pode aproveitar os dados do Experience Platform em suas plataformas de aprendizado de máquina para gerar modelos preditivos, como pontuações de propensão. Este guia explica como usar o Serviço de query para enviar dados para sua plataforma de aprendizado de máquina a fim de treinar um modelo em um notebook computacional. O modelo treinado pode ser aplicado aos dados usando o SQL para prever a propensão de compra de um cliente para cada visita.

## Introdução

Como parte desse processo requer o treinamento de um modelo de aprendizado de máquina, este documento assume um conhecimento funcional de um ou mais ambientes de aprendizado de máquina.

Esse exemplo usa [!DNL Jupyter Notebook] como ambiente de desenvolvimento. Embora haja muitas opções disponíveis, [!DNL Jupyter Notebook] é recomendado porque é uma aplicação Web de código aberto que tem requisitos de computação baixos. Pode ser [baixado do site oficial](https://jupyter.org/).

Se ainda não tiver feito isso, siga as etapas para [connect [!DNL Jupyter Notebook] com o Adobe Experience Platform Query Service](../clients/jupyter-notebook.md) antes de continuar com este guia.

As bibliotecas usadas neste exemplo incluem:

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## Importar tabelas de análise da Platform para [!DNL Jupyter Notebook] {#import-analytics-tables}

Para gerar um modelo de pontuação de propensão, uma projeção dos dados de análise armazenados no Platform deve ser importada para [!DNL Jupyter Notebook]. De um [!DNL Python] 3 [!DNL Jupyter Notebook] conectado ao Serviço de query, os seguintes comandos importam um conjunto de dados de comportamento do cliente do Luma, um armazenamento fictício de roupas. Como os dados da plataforma são armazenados usando o formato Experience Data Model (XDM) , um objeto JSON de amostra deve ser gerado de acordo com a estrutura do esquema. Consulte a documentação para obter instruções sobre como [gerar o objeto JSON de amostra](../../xdm/ui/sample.md).

![O [!DNL Jupyter Notebook] painel com vários comandos realçados.](../images/use-cases/jupyter-commands.png)

A saída exibe uma exibição tabularizada de todas as colunas do conjunto de dados comportamentais do Luma dentro da variável [!DNL Jupyter Notebook] painel.

![A saída tabularizada do conjunto de dados de comportamento do cliente importado do Luma no [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## Preparar os dados para aprendizagem de máquina {#prepare-data-for-machine-learning}

Uma coluna de destino deve ser identificada para treinar um modelo de aprendizado de máquina. Como a propensão a comprar é a meta para este caso de uso, a variável `analytic_action` é escolhida como a coluna target dos resultados do Luma. O valor `productPurchase` é o indicador de uma compra de cliente. O `purchase_value` e `purchase_num` também são removidas, pois estão diretamente relacionadas à ação de compra do produto.

Os comandos para executar essas ações são os seguintes:

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

Em seguida, os dados do conjunto de dados do Luma devem ser transformados em representações apropriadas. São necessárias duas etapas:

1. Transforme as colunas que representam números em colunas numéricas. Para fazer isso, converta explicitamente o tipo de dados na função `dataframe`.
1. Transforme colunas categóricas em colunas numéricas também.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

Uma técnica chamada *uma codificação ativa* é usada para converter as variáveis de dados categóricos para uso com algoritmos de máquina e de aprendizado profundo. Por sua vez, isso melhora as previsões, bem como a precisão da classificação de um modelo. Use o `Sklearn` biblioteca para representar cada valor categórico em uma coluna separada.

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

Os dados definidos como `X` O é tabularizado e aparece como abaixo:

![A saída tabularizada de X dentro de [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


Agora que os dados necessários para o aprendizado de máquina estão disponíveis, eles podem se encaixar nos modelos pré-configurados de aprendizado de máquina em [!DNL Python]&#39;s `sklearn` biblioteca. [!DNL Logistics Regression] é usada para treinar o modelo de propensão e permite ver a precisão dos dados de teste. Nesse caso, é de aproximadamente 85%.

O [!DNL Logistic Regression] O algoritmo e o método de divisão do teste de comboio, utilizados para estimar o desempenho dos algoritmos de aprendizagem de máquina, são importados no bloco de códigos abaixo:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

A precisão dos dados de teste é 0,8518518518518519.

Com o uso da Regressão de Logística, é possível visualizar os motivos de uma compra e classificar os recursos que determinam a propensão pela importância classificada em pedidos decrescentes. As primeiras colunas indicam uma causa mais alta que leva ao comportamento de compra. As últimas colunas indicam fatores que não levam ao comportamento de compra.

O código para visualizar os resultados como dois gráficos de barras é o seguinte:

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

Uma visualização dos resultados do gráfico de barras vertical é vista abaixo:

![A visualização dos 10 recursos principais que definem uma propensão para comprar ou não.](../images/use-cases/visualized-results.png)

Vários padrões podem ser detectados no gráfico de barras. Os tópicos de Ponto de venda (POS) e Chamada do canal como reembolso são os fatores mais importantes que decidem o comportamento de compra. Embora os tópicos de Chamada como reclamações e faturas sejam funções importantes para definir o comportamento de não compra. Esses são insights quantificáveis e acionáveis que os profissionais de marketing podem aproveitar para realizar campanhas de marketing para atender à propensão de compra desses clientes.

## Usar o Serviço de Consulta para aplicar o modelo treinado {#use-query-service-to-apply-trained-model}

Após a criação do modelo treinado, ele deve ser aplicado aos dados mantidos no Experience Platform. Para fazer isso, a lógica do pipeline de aprendizado de máquina deve ser convertida para SQL. Os dois componentes principais dessa transição são os seguintes:

- Primeiro, o SQL deve substituir o [!DNL Logistics Regression] para obter a probabilidade de um rótulo de previsão. O modelo criado pela Regressão de Logística produziu o modelo de regressão `y = wX + c`  em que pesos `w` e intercepto `c` são a saída do modelo. Os recursos SQL podem ser usados para multiplicar os pesos para obter uma probabilidade.

- Em segundo lugar, o processo de engenharia realizado em [!DNL Python] com uma codificação a quente também deve ser incorporada no SQL. Por exemplo, no banco de dados original, temos `geo_county` coluna para armazenar o município, mas a coluna é convertida em `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`. A instrução SQL a seguir realiza a mesma transformação, em que `w1`, `w2`e `w3` pode ser substituído pelos pesos aprendidos do modelo em [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

Para recursos numéricos, você pode multiplicar diretamente as colunas com os pesos, conforme visto na instrução SQL abaixo.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

Após os números terem sido obtidos, eles podem ser portados para uma função sigmoide na qual o algoritmo Logistics Regression produz as previsões finais. Na declaração abaixo, `intercept` é o número do intercepto na regressão.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### Um exemplo completo

Em uma situação em que há duas colunas (`c1` e `c2`), se `c1` tem duas categorias, a variável [!DNL Logistic Regression] O algoritmo é treinado com a seguinte função:
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
O equivalente em SQL é o seguinte:

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```
 
O [!DNL Python] o código para automatizar o processo de tradução é o seguinte:

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

Quando o SQL é usado para inferir o banco de dados, a saída é a seguinte:

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

Os resultados tabularizados exibem a propensão a comprar para cada sessão do cliente com `0` que não significa propensão para comprar e `1` o que significa uma tendência confirmada de compra.

![Os resultados tabularizados da inferência do banco de dados usando SQL.](../images/use-cases/inference-results.png)

## Trabalhando em dados recolhidos: Bootstrapping {#working-on-sampled-data}

No caso de os tamanhos dos dados serem muito grandes para a máquina local armazenar os dados para o treinamento do modelo, você pode fazer amostras em vez dos dados completos do Serviço de query. Para saber a quantidade de dados necessária para a amostra do Serviço de query, você pode aplicar uma técnica chamada bootstrapping. A este respeito, o bootstrapping significa que o modelo é treinado várias vezes com várias amostras e a variação da precisão do modelo entre diferentes amostras é inspecionada. Para ajustar o exemplo de modelo de propensão fornecido acima, primeiro, encapsula todo o fluxo de trabalho de aprendizado de máquina em uma função. O código é o seguinte:

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

Essa função pode ser executada várias vezes em um loop, por exemplo, 10 vezes. A diferença em relação ao código anterior é que a amostra agora não é retirada da tabela inteira, mas apenas de uma amostra de linhas. Por exemplo, o código de amostra abaixo leva apenas 1000 linhas. As precisões de cada iteração podem ser armazenadas.

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

As precisões do modelo com bootstrapped são classificadas. Depois disso, as 10ª e 90ª quantidades da precisão do modelo se tornam um Intervalo de Confiança de 95% para a precisão do modelo com o tamanho de amostra dado.

![O comando print para exibir o intervalo de confiança da pontuação de propensão.](../images/use-cases/confidence-interval.png)

A figura acima indica que se você pegar apenas 1000 linhas para treinar seus modelos, é possível esperar que as precisões estejam entre aproximadamente 84% e 88%. Pode ajustar a variável `LIMIT` em consultas do Serviço de query com base em suas necessidades para garantir o desempenho dos modelos.


