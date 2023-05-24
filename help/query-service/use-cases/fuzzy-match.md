---
title: Correspondência Difusa no Serviço de Consulta
description: Saiba como executar uma correspondência nos dados da Platform que combina resultados de vários conjuntos de dados correspondendo aproximadamente a uma cadeia de caracteres de sua escolha.
exl-id: ec1e2dda-9b80-44a4-9fd5-863c45bc74a7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---

# Correspondência difusa no Serviço de consulta

Use uma correspondência &quot;difusa&quot; nos dados do Adobe Experience Platform para retornar as correspondências aproximadas mais prováveis, sem a necessidade de pesquisar cadeias de caracteres com caracteres idênticos. Isso permite uma pesquisa muito mais flexível de seus dados e torna seus dados mais acessíveis, economizando tempo e esforço.

Em vez de tentar reformatar as cadeias de caracteres de pesquisa para correspondê-las, a correspondência difusa analisa a proporção de similaridade entre duas sequências e retorna a porcentagem de similaridade. [[!DNL FuzzyWuzzy]](https://pypi.org/project/fuzzywuzzy/) é recomendado para esse processo, pois suas funções são mais adequadas para ajudar a corresponder strings em situações mais complexas em comparação com [!DNL regex] ou [!DNL difflib].

O exemplo fornecido neste caso de uso se concentra em corresponder atributos semelhantes de uma pesquisa de quarto de hotel em dois conjuntos de dados de agências de viagens diferentes. O documento demonstra como fazer a correspondência de strings por seu grau de similaridade a partir de grandes fontes de dados separadas. Neste exemplo, a correspondência difusa compara os resultados da pesquisa para os recursos de um quarto das agências de viagens Luma e Acme.

## Introdução {#getting-started}

Como parte desse processo requer que você treine um modelo de aprendizado de máquina, este documento presume um conhecimento prático de um ou mais ambientes de aprendizado de máquina.

Este exemplo usa [!DNL Python] e a variável [!DNL Jupyter Notebook] ambiente de desenvolvimento. Embora existam muitas opções disponíveis, [!DNL Jupyter Notebook] O é recomendado porque é um aplicativo web de código aberto que tem poucos requisitos computacionais. Ele pode ser baixado em [o sítio oficial de Jupyter](https://jupyter.org/).

Antes de começar, você deve importar as bibliotecas necessárias. [!DNL FuzzyWuzzy] O é um software de código aberto [!DNL Python] biblioteca criada sobre a [!DNL difflib] e usado para corresponder strings. Usa [!DNL Levenshtein Distance] para calcular as diferenças entre sequências e padrões. [!DNL FuzzyWuzzy] O tem os seguintes requisitos:

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

Mais informações técnicas sobre [!DNL Fuzzywuzzy] podem ser encontrados em seus [documentação oficial](https://pypi.org/project/fuzzywuzzy/).

### Conectar-se ao Serviço de consulta

Você deve conectar seu modelo de aprendizado de máquina ao Serviço de consulta fornecendo suas credenciais de conexão. As credenciais com e sem expiração podem ser fornecidas. Consulte a [guia de credenciais](../ui/credentials.md) para obter mais informações sobre como adquirir as credenciais necessárias. Se você estiver usando [!DNL Jupyter Notebook], leia o guia completo sobre [como se conectar ao Serviço de consulta](../clients/jupyter-notebook.md).

Além disso, certifique-se de importar o [!DNL numpy] pacote em seu [!DNL Python] para habilitar a álgebra linear.

```python
import numpy as np
```

Os comandos abaixo são necessários para se conectar ao Serviço de consulta de [!DNL Jupyter Notebook]:

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

Seu [!DNL Jupyter Notebook] A instância do agora está conectada ao Serviço de consulta. Se a conexão for bem-sucedida, nenhuma mensagem será exibida. Se a conexão falhar, um erro será exibido.

### Desenhar dados do conjunto de dados Luma {#luma-dataset}

Os dados para análise são retirados do primeiro conjunto de dados com os seguintes comandos. Por motivos de brevidade, os exemplos foram limitados aos primeiros 10 resultados da coluna.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Selecionar **Output** para exibir a matriz retornada.

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

Os dados para análise agora são retirados do segundo conjunto de dados com os seguintes comandos. Novamente, por questões de brevidade, os exemplos foram limitados aos primeiros 10 resultados da coluna.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Selecionar **Output** para exibir a matriz retornada.

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

Em seguida, você deve importar `fuzz` da biblioteca FuzzyWuzzy e execute uma comparação de proporção parcial das cadeias de caracteres. A função de proporção parcial permite executar a correspondência de substring. Isto pega a string mais curta e combina com todas as sub- strings que tenham o mesmo comprimento. A função retorna uma taxa de similaridade percentual de até 100%. Por exemplo, a função de proporção parcial compararia as seguintes strings &quot;Quarto Deluxe&quot;, &quot;1 Cama King&quot; e &quot;Quarto King Deluxe&quot; e retornaria uma pontuação de similaridade de 69%.

No caso de uso de correspondência de quarto de hotel, isso é feito usando os seguintes comandos:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

Em seguida, importe `cdist` do [!DNL SciPy] para calcular a distância entre cada par nas duas coleções de entradas. Este cálculo calcula as pontuações entre todos os pares de quartos de hotel fornecidos por cada uma das agências de viagens.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Criar mapeamentos entre as duas colunas usando a pontuação de junção difusa

Agora que as colunas foram pontuadas com base na distância, você pode indexar os pares e reter somente correspondências que tiveram pontuação maior do que uma determinada porcentagem. Este exemplo retém apenas pares que corresponderam a uma pontuação de 70% ou superior.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

Os resultados podem ser exibidos com o comando a seguir. Por motivos de brevidade, os resultados são limitados a dez linhas.

```python
matched_pairs[:10]
```

Selecionar **Output** para ver os resultados.

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

Os resultados são correspondidos usando SQL com o seguinte comando:

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Aplicar os mapeamentos para fazer junção difusa no Serviço de consulta {#mappings-for-query-service}

Em seguida, os pares correspondentes de alta pontuação são unidos usando SQL para criar um novo conjunto de dados.

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

Selecionar **Output** para ver os resultados desta associação.

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

### Salvar resultados de correspondência difusa na Platform {#save-to-platform}

Por fim, os resultados da correspondência difusa podem ser salvos como um conjunto de dados para uso no Adobe Experience Platform usando SQL.

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
