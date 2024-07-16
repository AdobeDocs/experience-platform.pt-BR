---
title: Determine Uma Pontuação De Propensão Usando Um Modelo Preditivo Gerado Pelo Machine Learning
description: Saiba como usar o Serviço de consulta para aplicar seu modelo preditivo aos dados da plataforma. Este documento demonstra como usar os dados da plataforma para prever a propensão de um cliente para comprar em cada visita.
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: 40c27a52fdae2c7d38c5e244a6d1d6ae3f80f496
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# Determine uma pontuação de propensão usando um modelo preditivo gerado por aprendizado de máquina

Usando o Serviço de consulta, você pode aproveitar modelos preditivos, como pontuações de propensão, criados em sua plataforma de aprendizado de máquina para analisar dados de Experience Platform.

Este guia explica como usar o Serviço de consulta para enviar dados para sua plataforma de aprendizado de máquina para treinar um modelo em um bloco de anotações computacional. O modelo treinado pode ser aplicado aos dados usando SQL para prever a propensão de um cliente a comprar para cada visita.

## Introdução

Como parte desse processo requer que você treine um modelo de aprendizado de máquina, este documento presume um conhecimento prático de um ou mais ambientes de aprendizado de máquina.

Este exemplo usa [!DNL Jupyter Notebook] como um ambiente de desenvolvimento. Embora existam muitas opções disponíveis, [!DNL Jupyter Notebook] é recomendado porque é um aplicativo web de código aberto que tem poucos requisitos computacionais. Ele pode ser [baixado do site oficial](https://jupyter.org/).

Se você ainda não tiver feito isso, siga as etapas para [conectar [!DNL Jupyter Notebook] ao Serviço de Consulta da Adobe Experience Platform](../clients/jupyter-notebook.md) antes de continuar com este guia.

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

Para gerar um modelo de pontuação de propensão, uma projeção dos dados de análise armazenados na Plataforma deve ser importada para [!DNL Jupyter Notebook]. De um [!DNL Python] 3 [!DNL Jupyter Notebook] conectado ao Serviço de consulta, os comandos a seguir importam um conjunto de dados de comportamento do cliente da Luma, uma loja fictícia de roupas. Como os dados da Platform são armazenados usando o formato Experience Data Model (XDM), um objeto JSON de amostra deve ser gerado que esteja em conformidade com a estrutura do esquema. Consulte a documentação para obter instruções sobre como [gerar o objeto JSON de amostra](../../xdm/ui/sample.md).

![O painel [!DNL Jupyter Notebook] com vários comandos realçados.](../images/use-cases/jupyter-commands.png)

A saída exibe uma exibição tabulada de todas as colunas do conjunto de dados comportamentais do Luma no painel [!DNL Jupyter Notebook].

![A saída tabulada do conjunto de dados de comportamento do cliente importado da Luma em [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## Preparar os dados para aprendizado de máquina {#prepare-data-for-machine-learning}

Uma coluna de destino deve ser identificada para treinar um modelo de aprendizado de máquina. Como a propensão para comprar é o objetivo desse caso de uso, a coluna `analytic_action` é escolhida como a coluna de destino dos resultados da Luma. O valor `productPurchase` é o indicador de uma compra de cliente. As colunas `purchase_value` e `purchase_num` também são removidas porque estão diretamente relacionadas à ação de compra do produto.

Os comandos para executar essas ações são os seguintes:

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

Em seguida, os dados do conjunto de dados da Luma devem ser transformados em representações apropriadas. São necessárias duas etapas:

1. Transforme as colunas que representam números em colunas numéricas. Para fazer isso, converta explicitamente o tipo de dados no `dataframe`.
1. Transformar colunas categóricas em colunas numéricas também.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

Uma técnica chamada *uma codificação a quente* é usada para converter as variáveis de dados categóricas para uso com algoritmos de máquina e deep learning. Isso, por sua vez, melhora as previsões, bem como a precisão da classificação de um modelo. Use a biblioteca `Sklearn` para representar cada valor categórico em uma coluna separada.

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

Os dados definidos como `X` são tabulados e exibidos como abaixo:

![A saída tabulada de X em [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


Agora que os dados necessários para o aprendizado de máquina estão disponíveis, ele pode ajustar os modelos pré-configurados de aprendizado de máquina na biblioteca `sklearn` de [!DNL Python]. O [!DNL Logistics Regression] é usado para treinar o modelo de propensão e permite que você veja a precisão dos dados de teste. Nesse caso, é de aproximadamente 85%.

O algoritmo [!DNL Logistic Regression] e o método de divisão train-test, usados para estimar o desempenho dos algoritmos de aprendizado de máquina, são importados no bloco de código abaixo:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

A precisão dos dados de teste é 0,8518518518518519.

Com o uso da Regressão logística, você pode visualizar os motivos de uma compra e classificar os recursos que determinam a propensão pela importância classificada em ordens decrescentes. As primeiras colunas indicam um nexo de causalidade mais elevado que conduz ao comportamento de compra. Estas últimas colunas indicam fatores que não conduzem a um comportamento de compra.

O código para visualizar os resultados como gráficos de duas barras é o seguinte:

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

Uma visualização de resultados em um gráfico de barras vertical é vista abaixo:

![A visualização dos 10 principais recursos que definem uma propensão a comprar ou não.](../images/use-cases/visualized-results.png)

Vários padrões podem ser discernidos no gráfico de barras. Os tópicos de ponto de venda (POS) e chamada do canal como reembolso são os fatores mais importantes que decidem o comportamento de compra. Embora os tópicos da Chamada como reclamações e faturas sejam funções importantes para definir o comportamento de não compra. Esses são insights quantificáveis e acionáveis que os profissionais de marketing podem aproveitar para conduzir campanhas de marketing a fim de lidar com a propensão à compra desses clientes.

## Use o Serviço de consulta para aplicar o modelo treinado {#use-query-service-to-apply-trained-model}

Após a criação do modelo treinado, ele deve ser aplicado aos dados mantidos no Experience Platform. Para fazer isso, a lógica do pipeline de aprendizado de máquina deve ser convertida para SQL. Os dois principais componentes dessa transição são os seguintes:

- Primeiro, o SQL deve substituir o módulo [!DNL Logistics Regression] para obter a probabilidade de um rótulo de previsão. O modelo criado pela Regressão Logística produziu o modelo de regressão `y = wX + c` em que os pesos `w` e a interceptação `c` são a saída do modelo. Os recursos SQL podem ser usados para multiplicar os pesos para obter uma probabilidade.

- Em segundo lugar, o processo de engenharia obtido em [!DNL Python] com uma codificação a quente também deve ser incorporado ao SQL. Por exemplo, no banco de dados original, temos a coluna `geo_county` para armazenar o município, mas a coluna é convertida em `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`. A instrução SQL a seguir conduz a mesma transformação, em que `w1`, `w2` e `w3` podem ser substituídos pelos pesos aprendidos do modelo em [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

Para recursos numéricos, você pode multiplicar diretamente as colunas com os pesos, conforme visto na instrução SQL abaixo.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

Após os números serem obtidos, eles podem ser portados para uma função sigmoide onde o algoritmo de Regressão Logística produz as previsões finais. Na instrução abaixo, `intercept` é o número da interceptação na regressão.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### Um exemplo completo

Em uma situação em que você tem duas colunas (`c1` e `c2`), se `c1` tiver duas categorias, o algoritmo [!DNL Logistic Regression] será treinado com a seguinte função:
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
O equivalente no SQL é o seguinte:

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
 
O código [!DNL Python] para automatizar o processo de tradução é o seguinte:

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

Os resultados tabulados exibem a propensão a compra para cada sessão de cliente com `0`, o que significa nenhuma propensão a comprar, e `1`, a propensão confirmada para comprar.

![Os resultados tabulados da inferência do banco de dados usando SQL.](../images/use-cases/inference-results.png)

## Trabalhando em dados de amostra: Bootstrapping {#working-on-sampled-data}

Caso os tamanhos de dados sejam muito grandes para que sua máquina local armazene os dados para treinamento de modelo, você pode obter amostras em vez dos dados completos do Serviço de consulta. Para saber quantos dados são necessários para fazer amostragem do Serviço de consulta, você pode aplicar uma técnica chamada bootstrapping. A este respeito, bootstrapping significa que o modelo é treinado várias vezes com várias amostras, e a variação das precisões do modelo entre diferentes amostras é inspecionada. Para ajustar o exemplo do modelo de propensão fornecido acima, primeiro encapsule todo o fluxo de trabalho de aprendizado de máquina em uma função. O código é o seguinte:

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

Essa função pode ser executada várias vezes em um loop, por exemplo, 10 vezes. A diferença em relação ao código anterior é que a amostra agora não é retirada da tabela inteira, mas apenas uma amostra de linhas. Por exemplo, o código de amostra abaixo utiliza apenas 1000 linhas. As precisões para cada iteração podem ser armazenadas.

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

As precisões do modelo inicializado são classificadas. Depois disso, o décimo e o nonagésimo quantis das precisões do modelo tornam-se um Intervalo de confiança de 95% para as precisões do modelo com o tamanho de amostra determinado.

![O comando print para exibir o intervalo de confiança da pontuação de propensão.](../images/use-cases/confidence-interval.png)

A figura acima afirma que se você pegar apenas 1000 linhas para treinar seus modelos, você pode esperar que as exatidões fiquem entre aproximadamente 84% e 88%. Você pode ajustar a cláusula `LIMIT` em consultas do Serviço de consulta com base nas suas necessidades para garantir o desempenho dos modelos.
