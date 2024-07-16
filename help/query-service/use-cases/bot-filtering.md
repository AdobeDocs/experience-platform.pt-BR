---
title: Filtragem de bot no Serviço de consulta com Machine Learning
description: Este documento fornece uma visão geral de como usar o Serviço de consulta e o aprendizado de máquina para determinar a atividade do bot e filtrar suas ações a partir do tráfego de visitantes genuíno do site online.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 5%

---

# Filtragem de bot no [!DNL Query Service] com aprendizado de máquina

A atividade de bot pode afetar as métricas de análise e prejudicar a integridade dos dados. O Adobe Experience Platform [!DNL Query Service] pode ser usado para manter a qualidade dos dados por meio do processo de filtragem de bot.

A filtragem de bot permite que você mantenha a qualidade dos seus dados, removendo amplamente a contaminação de dados resultante de interações não humanas com o seu site. Esse processo é obtido por meio da combinação de queries SQL e aprendizado de máquina.

A atividade de bot pode ser identificada de várias maneiras. A abordagem adotada neste documento se concentra em picos de atividade, neste caso, o número de ações executadas por um usuário em um determinado período de tempo. Inicialmente, uma consulta SQL define arbitrariamente um limite para o número de ações tomadas durante um período para se qualificar como atividade de bot. Esse limite é então refinado dinamicamente usando um modelo de aprendizado de máquina para melhorar a precisão dessas taxas.

Este documento fornece uma visão geral e exemplos detalhados das consultas de filtragem de bot SQL e dos modelos de aprendizado de máquina necessários para você configurar o processo no seu ambiente.

## Introdução

Como parte desse processo requer que você treine um modelo de aprendizado de máquina, este documento presume um conhecimento prático de um ou mais ambientes de aprendizado de máquina.

Este exemplo usa [!DNL Jupyter Notebook] como um ambiente de desenvolvimento. Embora existam muitas opções disponíveis, [!DNL Jupyter Notebook] é recomendado porque é um aplicativo web de código aberto que tem poucos requisitos computacionais. Ele pode ser [baixado do site oficial](https://jupyter.org/).

## Usar [!DNL Query Service] para definir um limite para a atividade de bot

Os dois atributos usados para extrair dados para detecção de bot são:

* ID de visitante do Experience Cloud (ECID, também conhecida como MCID): fornece uma ID contínua e universal que identifica os visitantes em todas as soluções da Adobe.
* Carimbo de data e hora: fornece a hora e a data em formato UTC quando uma atividade ocorreu no site.

>[!NOTE]
>
>O uso de `mcid` ainda é encontrado nas referências de namespace à ID de visitante do Experience Cloud, como visto no exemplo abaixo.

A instrução SQL a seguir fornece um exemplo inicial para identificar a atividade de bot. A instrução pressupõe que, se um visitante realizar 50 cliques em um minuto, o usuário será um bot.

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

A expressão filtra os ECIDs (`mcid`) de todos os visitantes que atingem o limite, mas não aborda picos no tráfego de outros intervalos.

## Melhore a detecção de bot com o aprendizado de máquina

A instrução SQL inicial pode ser refinada para se tornar uma consulta de extração de recursos para aprendizado de máquina. O query aprimorado deve produzir mais recursos para uma variedade de intervalos para treinar modelos de aprendizado de máquina com alta precisão.

A instrução de exemplo é expandida de um minuto com até 60 cliques para incluir períodos de cinco minutos e 30 minutos com contagens de cliques de 300 e 1800, respectivamente.

A instrução de exemplo coleta o número máximo de cliques para cada ECID (`mcid`) nas várias durações. A instrução inicial foi expandida para incluir períodos de um minuto (60 segundos), 5 minutos (300 segundos) e uma hora (ou seja, 1800 segundos).

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

O resultado dessa expressão pode ser semelhante à tabela fornecida abaixo.

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## Identificar novos limites de pico usando aprendizado de máquina

Em seguida, exporte o conjunto de dados da consulta resultante para o formato CSV e, em seguida, importe-o para [!DNL Jupyter Notebook]. A partir desse ambiente, você pode treinar um modelo de aprendizado de máquina usando as bibliotecas de aprendizado de máquina atuais. Consulte o guia de solução de problemas para obter mais detalhes sobre [como exportar dados de [!DNL Query Service] em formato CSV](../troubleshooting-guide.md#export-csv)

Os limites de pico ad hoc inicialmente estabelecidos não são orientados por dados e, portanto, carecem de precisão. Os modelos de aprendizado de máquina podem ser usados para treinar parâmetros como limites. Como resultado, você pode aumentar a eficiência da consulta reduzindo o número de `GROUP BY` palavras-chave, removendo recursos desnecessários.

Este exemplo usa a biblioteca de aprendizado de máquina Scikit-Learn, que é instalada por padrão com o [!DNL Jupyter Notebook]. A biblioteca &quot;pandas&quot; Python também é importada para uso aqui. Os seguintes comandos estão sendo inseridos em [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Em seguida, você deve treinar um classificador de árvore de decisão no conjunto de dados e observar a lógica resultante do modelo.

A biblioteca &quot;Matplotlib&quot; é usada para visualizar o classificador de árvore decisória no exemplo abaixo.

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

Os valores retornados de [!DNL Jupyter Notebook] para este exemplo são os seguintes.

```text
Model Accuracy: 0.99935
```

![Saída estatística do modelo de aprendizado de máquina [!DNL Jupyter Notebook].](../images/use-cases/jupiter-notebook-output.png)

Os resultados do modelo mostrado no exemplo acima têm mais de 99% de precisão.

Como o classificador da árvore de decisão pode ser treinado usando dados de [!DNL Query Service] regularmente com consultas agendadas, você pode garantir a integridade dos dados filtrando a atividade do bot com um alto grau de precisão. Usando os parâmetros derivados do modelo de aprendizado de máquina, as consultas originais podem ser atualizadas com os parâmetros altamente precisos criados pelo modelo.

O modelo de exemplo determinou com alto grau de precisão que todos os visitantes com mais de 130 interações em cinco minutos são bots. Essas informações agora podem ser usadas para refinar suas consultas SQL de filtragem de bot.

## Próximas etapas

Ao ler este documento, você terá uma melhor compreensão de como usar o [!DNL Query Service] e o aprendizado de máquina para determinar e filtrar a atividade de bot.

Outros documentos que demonstram os benefícios do [!DNL Query Service] para os insights estratégicos de negócios da sua organização são o [exemplo de uso de navegação abandonada](./abandoned-browse.md).
