---
title: Correspondência difusa no serviço de query
description: Saiba como executar uma correspondência nos dados da plataforma que combina resultados de vários conjuntos de dados, correspondendo aproximadamente a uma string de sua escolha.
source-git-commit: 633210fe5e824d8686a23b877a406db3780ebdd4
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---

# Correspondência difusa no serviço de query

Use uma correspondência &quot;difusa&quot; em seus dados do Adobe Experience Platform para retornar as correspondências mais prováveis e aproximadas sem a necessidade de pesquisar por sequências com caracteres idênticos. Isso permite uma pesquisa muito mais flexível de seus dados e torna seus dados mais acessíveis, economizando tempo e esforço.

Em vez de tentar reformatar as cadeias de caracteres de pesquisa para combiná-las, a correspondência difusa analisa a proporção de similaridade entre duas sequências e retorna a porcentagem de similaridade. [[!DNL FuzzyWuzzy]](https://pypi.org/project/fuzzywuzzy/) é recomendado para esse processo, pois suas funções são mais adequadas para ajudar a corresponder strings em situações mais complexas em comparação ao [!DNL regex] ou [!DNL difflib].

O exemplo fornecido neste caso de uso foca em corresponder atributos semelhantes de uma pesquisa em quarto de hotel em dois conjuntos de dados diferentes de agência de viagens. O documento demonstra como corresponder cadeias de caracteres por seu grau de semelhança de grandes fontes de dados separadas. Neste exemplo, a correspondência difusa compara os resultados da pesquisa pelos recursos de uma sala das agências de viagens Luma e Acme.

## Introdução {#getting-started}

Como parte desse processo requer o treinamento de um modelo de aprendizado de máquina, este documento assume um conhecimento funcional de um ou mais ambientes de aprendizado de máquina.

Esse exemplo usa [!DNL Python] e [!DNL Jupyter Notebook] ambiente de desenvolvimento. Embora haja muitas opções disponíveis, [!DNL Jupyter Notebook] é recomendado porque é uma aplicação Web de código aberto que tem requisitos de computação baixos. Ele pode ser baixado de [o sítio oficial de Jupyter](https://jupyter.org/).

Antes de começar, você deve importar as bibliotecas necessárias. [!DNL FuzzyWuzzy] é um [!DNL Python] biblioteca incorporada sobre [!DNL difflib] biblioteca e usada para corresponder strings. Ele usa [!DNL Levenshtein Distance] para calcular as diferenças entre sequências e padrões. [!DNL FuzzyWuzzy] tem os seguintes requisitos:

- [!DNL Python] 2.4 (ou superior)
- [!DNL Python-Levenshtein]

Na linha de comando, use o seguinte comando para instalar [!DNL FuzzyWuzzy]:

```console
pip install fuzzywuzzy
```

Ou use o seguinte comando para instalar [!DNL Python-Levenshtein] também:

```console
pip install fuzzywuzzy[speedup]
```

Mais informações técnicas sobre [!DNL Fuzzywuzzy] podem ser encontradas em [documentação oficial](https://pypi.org/project/fuzzywuzzy/).

### Conectar ao Serviço de Consulta

Você deve conectar seu modelo de aprendizado de máquina ao Serviço de query fornecendo suas credenciais de conexão. Tanto as credenciais que expiram quanto as que não expiram podem ser fornecidas. Consulte a [guia de credenciais](../ui/credentials.md) para obter mais informações sobre como adquirir as credenciais necessárias. Se estiver usando [!DNL Jupyter Notebook], leia o guia completo sobre [como se conectar ao Serviço de query](../clients/jupyter-notebook.md).

Além disso, certifique-se de importar a variável [!DNL numpy] pacote em seu [!DNL Python] para ativar a álgebra linear.

```python
import numpy as np
```

Os comandos abaixo são necessários para se conectar ao Serviço de query de [!DNL Jupyter Notebook]:

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

Seu [!DNL Jupyter Notebook] A instância agora está conectada ao Serviço de query. Se a conexão for bem-sucedida, nenhuma mensagem será exibida. Se a conexão falhar, um erro será exibido.

### Desenhar dados do conjunto de dados do Luma {#luma-dataset}

Os dados para análise são obtidos do primeiro conjunto de dados com os seguintes comandos. Por brevidade, os exemplos foram limitados aos primeiros 10 resultados da coluna.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Selecionar **Saída** para exibir a matriz retornada.

+++Saída

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Desenhar dados do conjunto de dados Acme {#acme-dataset}

Os dados para análise agora são obtidos do segundo conjunto de dados com os seguintes comandos. Mais uma vez, por brevidade, os exemplos foram limitados aos primeiros 10 resultados da coluna.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Selecionar **Saída** para exibir a matriz retornada.

+++Saída

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Criar uma função de pontuação difusa {#fuzzy-scoring}

Em seguida, você deve importar `fuzz` da biblioteca do FuzzyWuzzy e execute uma comparação parcial da proporção das cadeias de caracteres. A função de proporção parcial permite executar a correspondência de subsequência de caracteres. Essa ação utiliza a string mais curta e a corresponde a todas as subsequências de caracteres com o mesmo comprimento. A função retorna uma proporção de similaridade de porcentagem de até 100%. Por exemplo, a função de proporção parcial compararia as strings a seguir &quot;Sala Deluxe&quot;, &quot;Cama Rei&quot; e &quot;Quarto Rei Deluxe&quot; e retornaria uma pontuação de similaridade de 69%.

No caso de uso de correspondência do quarto de hotel, isso é feito usando os seguintes comandos:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

Em seguida, importar `cdist` do [!DNL SciPy] biblioteca para calcular a distância entre cada par nas duas coleções de entradas. Isso calcula as pontuações entre todos os pares de quartos de hotel fornecidos por cada uma das agências de viagens.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Criar mapeamentos entre as duas colunas usando a pontuação de junção difusa

Agora que as colunas foram classificadas com base na distância, é possível indexar os pares e manter somente as correspondências com pontuação superior a uma porcentagem específica. Este exemplo retém apenas pares que correspondem com uma pontuação de 70% ou superior.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

Os resultados podem ser exibidos com o seguinte comando. Por brevidade, os resultados são limitados a dez linhas.

```python
matched_pairs[:10]
```

Selecionar **Saída** para ver os resultados.

+++Saída

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

Os resultados são então combinados usando SQL com o seguinte comando:

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Aplique os mapeamentos para fazer associação difusa no Serviço de query {#mappings-for-query-service}

Em seguida, os pares correspondentes de alta pontuação são unidos usando o SQL para criar um novo conjunto de dados.

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

Selecionar **Saída** para ver os resultados desta junção.

+++Saída

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### Salvar resultados de correspondência difusa na plataforma {#save-to-platform}

Finalmente, os resultados da correspondência difusa podem ser salvos como um conjunto de dados para uso no Adobe Experience Platform usando SQL.

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```


