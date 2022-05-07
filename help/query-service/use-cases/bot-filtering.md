---
title: Filtragem de bot no Serviço de query com aprendizado de máquina
description: Este documento fornece uma visão geral de como usar o Serviço de query e o aprendizado de máquina para determinar a atividade de bot e filtrar suas ações do tráfego online de visitantes genuíno.
source-git-commit: 7b223b4917e6bdb3f4a05238cbaf66261d80660e
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 5%

---

# Filtragem de bot em [!DNL Query Service] com aprendizagem de máquina

A atividade de bot pode afetar as métricas de análise e danificar a integridade dos dados. Adobe Experience Platform [!DNL Query Service] pode ser usada para manter a qualidade dos dados por meio do processo de filtragem de bot.

A filtragem de bot permite que você mantenha sua qualidade de dados removendo amplamente a contaminação de dados resultante da interação não humana com seu site. Esse processo é obtido por meio da combinação de consultas SQL e aprendizado de máquina.

A atividade Bot pode ser identificada de várias maneiras. A abordagem adotada neste documento foca em picos de atividade, nesse caso, o número de ações tomadas por um usuário em um determinado período de tempo. Inicialmente, uma consulta SQL define arbitrariamente um limite para o número de ações realizadas durante um período para se qualificar como atividade de bot. Esse limite é então refinado dinamicamente usando um modelo de aprendizado de máquina para melhorar a precisão dessas taxas.

Este documento fornece uma visão geral e exemplos detalhados das consultas de filtragem de bot SQL e dos modelos de aprendizado de máquina necessários para você configurar o processo no seu ambiente.

## Introdução

Como parte desse processo requer o treinamento de um modelo de aprendizado de máquina, este documento assume um conhecimento funcional de um ou mais ambientes de aprendizado de máquina.

Esse exemplo usa [!DNL Jupyter Notebook] como ambiente de desenvolvimento. Embora haja muitas opções disponíveis, [!DNL Jupyter Notebook] é recomendado porque é uma aplicação Web de código aberto que tem requisitos de computação baixos. Pode ser [baixado do site oficial](https://jupyter.org/).

## Use [!DNL Query Service] para definir um limite para a atividade bot

Os dois atributos usados para extrair dados para detecção de bot são:

* ID do Marketing Cloud (MCID): Isso fornece uma ID persistente e universal que identifica os visitantes em todas as soluções do Adobe.
* Carimbo de data e hora: Isso fornece a hora e a data em formato UTC em que uma atividade ocorreu no site.

A instrução SQL a seguir fornece um exemplo inicial para identificar a atividade de bot. A instrução parte do princípio que, se um visitante executar 50 cliques em um minuto, o usuário será um bot.

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

A expressão filtra os MCIDs de todos os visitantes que alcançam o limite, mas não solucionam picos no tráfego a partir de outros intervalos.

## Melhore a detecção de bot com o aprendizado de máquina

A instrução SQL inicial pode ser refinada para se tornar uma consulta de extração de recursos para aprendizagem de máquina. A consulta aprimorada deve produzir mais recursos para uma variedade de intervalos para treinamento de modelos de aprendizado de máquina com alta precisão.

A instrução de exemplo é expandida de um minuto com até 60 cliques, para incluir períodos de cinco minutos e 30 minutos com contagens de cliques de 300 e 1800, respectivamente.

A instrução de exemplo coleta o número máximo de cliques para cada MCID durante as várias durações. A declaração inicial foi expandida para incluir períodos de um minuto (60 segundos), 5 minutos (300 segundos) e uma hora (ou seja, 1800 segundos).

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
| 504568251944554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## Identificar novos limites de pico usando aprendizagem de máquina

Em seguida, exporte o conjunto de dados de consulta resultante para o formato CSV e, em seguida, importe-o para [!DNL Jupyter Notebook]. A partir desse ambiente, você pode treinar um modelo de aprendizado de máquina usando as bibliotecas atuais de aprendizado de máquina. Consulte o guia de solução de problemas para obter mais detalhes sobre [como exportar dados de [!DNL Query Service] no formato CSV](../troubleshooting-guide.md#export-csv)

Os limiares de pico ad hoc inicialmente estabelecidos não são orientados por dados e, portanto, não têm precisão. Modelos de aprendizado de máquina podem ser usados para treinar parâmetros como limites. Como resultado, você pode aumentar a eficiência do query reduzindo o número de `GROUP BY` palavras-chave removendo recursos desnecessários.

Este exemplo usa a biblioteca de aprendizado de máquina Scikit-Learn que é instalada por padrão com [!DNL Jupyter Notebook]. A biblioteca python &quot;pandas&quot; também é importada para uso aqui. Os seguintes comandos são inseridos em [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Em seguida, você deve treinar um classificador de árvore de decisão no conjunto de dados e observar a lógica resultante do modelo.

A biblioteca &quot;Matplotlib&quot; é usada para visualizar o classificador da árvore de decisão no exemplo abaixo.

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

Os valores retornados de [!DNL Jupyter Notebook] para este exemplo, são as seguintes.

```text
Model Accuracy: 0.99935
```

![Produção estatística de [!DNL Jupyter Notebook] modelo de aprendizado de máquina.](../images/use-cases/jupiter-notebook-output.png)

Os resultados do modelo mostrado no exemplo acima são mais de 99% precisos.

Como o classificador de árvore de decisão pode ser treinado usando dados de [!DNL Query Service] em uma cadência regular usando queries agendados, você pode garantir a integridade dos dados filtrando a atividade do bot com alto grau de precisão. Ao usar os parâmetros derivados do modelo de aprendizado de máquina, as consultas originais podem ser atualizadas com os parâmetros de alta precisão criados pelo modelo.

O modelo de exemplo determinado com alto grau de precisão que qualquer visitante com mais de 130 interações em cinco minutos é um bots. Essas informações agora podem ser usadas para refinar suas queries SQL de filtragem de bot.

## Próximas etapas

Ao ler este documento, você tem uma melhor compreensão de como usar o Serviço de query e o aprendizado de máquina para determinar e filtrar a atividade de bot.

Outros documentos que demonstram os benefícios de [!DNL Query Service] os insights de negócios estratégicos de sua organização são o exemplo de caso de uso de navegação abandonado.
