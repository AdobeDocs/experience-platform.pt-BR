---
title: Filtragem de bot usando estatística e aprendizado de máquina
description: Saiba como usar estatísticas do Data Distiller e aprendizado de máquina para identificar e filtrar a atividade de bot para garantir análises precisas e melhor integridade dos dados.
exl-id: 30d98281-7d15-47a6-b365-3baa07356010
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# Filtragem de bot usando estatísticas e aprendizado de máquina

As aplicações práticas da filtragem de bot abrangem vários setores. No comércio eletrônico, aumenta a confiabilidade das métricas de taxa de conversão, sites de notícias podem se beneficiar da mitigação de métricas de engajamento falso e as redes de publicidade podem garantir um faturamento justo. Para manter análises precisas e garantir a integridade dos dados em sequência de cliques ou dados de tráfego da Web, você deve abordar a atividade de bot. Você pode garantir dados de análise de alta qualidade usando o Data Distiller para implementar uma filtragem de bot eficiente e eliminar o tráfego indesejado.

Este documento fornece um guia abrangente para identificar e filtrar a atividade de bot usando técnicas de SQL e aprendizado de máquina. Ele apresenta uma progressão de abordagens complementares, começando com a filtragem básica e avançando para a detecção e avaliação baseadas em aprendizado de máquina. Adote essa estrutura robusta para aprimorar a detecção de bot e manter a integridade dos dados.

## Entender a atividade de bot {#understand-bot-activity}

A atividade de bot pode ser identificada pela detecção de picos nas ações do usuário em intervalos de tempo específicos. Por exemplo, cliques excessivos executados por um único usuário em um curto período de tempo podem indicar o comportamento do bot. Os dois principais atributos usados na filtragem de bot são:

- **ECID (Experience Cloud Visitor ID):** uma ID persistente e universal que identifica visitantes.
- **Carimbo de data/hora:** a data e a hora em que uma atividade ocorre no site.

Os exemplos abaixo demonstram como usar técnicas de SQL e aprendizado de máquina para identificar, refinar e prever a atividade do bot. Use esses métodos para melhorar a integridade dos dados e garantir análises acionáveis.

## Filtragem de bot com base em SQL {#sql-based-bot-filtering}

Este exemplo de filtragem de bot com base em SQL demonstra como usar consultas SQL para definir limites e detectar a atividade de bot com base em regras predefinidas. Essa abordagem básica ajuda a identificar anomalias no tráfego da Web, removendo atividades incomuns. Personalizando regras de detecção com limites e intervalos definidos, você pode adaptar efetivamente a filtragem de bot para atender aos padrões de tráfego específicos.

### Definir limites para a atividade de bot {#define-thresholds}

Comece analisando seu conjunto de dados para identificar e categorizar o comportamento do usuário. Concentre-se em atributos como ECID, carimbo de data e hora e `webPageDetails.name` (o nome da página da Web visitada) para agrupar ações de usuário e detectar padrões que indicam atividade de bot.

A consulta SQL abaixo demonstra como aplicar o limite de mais de 60 cliques em um minuto para identificar atividades suspeitas:

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### Expandir para vários intervalos {#expand-to-multiple-intervals}

Em seguida, defina intervalos de tempo diferentes para limites. Esses intervalos podem incluir:

- **Intervalo de 1 minuto:** Até 60 cliques.
- **Intervalo de 5 minutos:** até 300 cliques.
- **Intervalo de 30 minutos:** até 1800 cliques.

A consulta SQL a seguir cria uma exibição chamada `analytics_events_clicks_count_criteria` para lidar com limites em vários intervalos. A instrução consolida as contagens de cliques para intervalos de 1 minuto, 5 minutos e 30 minutos em um conjunto de dados estruturado e sinaliza a atividade potencial do bot com base em limites predefinidos.

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

A instrução une dados de `table_count_1_min`, `table_count_5_mins` e `table_count_30_mins` usando o valor `mcid` e a página da Web. Em seguida, consolida as contagens de cliques de cada usuário em vários intervalos de tempo para fornecer uma visualização completa da atividade do usuário. Finalmente, a lógica de sinalização identifica usuários que excedem 50 cliques em um minuto e os marca como bots (`isBot = 1`).

### Estrutura do conjunto de dados de saída

O conjunto de dados de saída é estruturado com campos simples e aninhados. Essa estrutura permite flexibilidade ao detectar tráfego anômalo e suporta estratégias de filtragem avançadas que usam SQL e aprendizado de máquina. Os campos aninhados incluem `count` e `web`, que encapsulam detalhes granulares sobre limites de atividade e páginas da Web. A captura dessas métricas significa que os recursos podem ser facilmente extraídos para tarefas de treinamento e previsão.

O diagrama de esquema a seguir descreve a estrutura do conjunto de dados resultante e destaca como os campos aninhados e simples podem ser usados para um processamento eficiente e detecção de bot.

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### O conjunto de dados de saída a ser usado para treinamento

O resultado dessa expressão pode ser semelhante à tabela fornecida abaixo. Na tabela, a coluna `isBot` atua como um rótulo que distingue entre atividades de bot e não de bot.

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## Funções estatísticas avançadas para filtragem de bot {#statistical-functions-for-bot-filtering}

Este segundo exemplo se baseia na filtragem SQL básica, incorporando técnicas de aprendizado de máquina para refinar limites e melhorar a precisão do filtro. Usando funções estatísticas avançadas, como análise de regressão ou algoritmos de clustering, essa abordagem introduz recursos preditivos que você pode usar para desenvolver modelos para lidar com conjuntos de dados complexos com mais precisão.

### Criar um conjunto de dados de treinamento {#build-a-training-dataset}

Primeiro, prepare um conjunto de dados com estruturas planas e aninhadas que o modelo de aprendizado de máquina possa usar (conforme descrito acima). Mais orientações sobre como fazer isso podem ser encontradas na [documentação Trabalho com estruturas de dados aninhadas](../../key-concepts/nested-data-structures.md). Agrupe os dados por carimbo de data e hora, ID de usuário e nome da página da Web para identificar padrões na atividade de bot.

### Usar as cláusulas TRANSFORM e OPTIONS para criação de modelo {#transform-and-preprocess}

Para transformar seu conjunto de dados e configurar seu modelo de aprendizado de máquina de maneira eficaz, siga as etapas abaixo. As etapas detalham como lidar com valores nulos, preparar recursos e definir os parâmetros do modelo para um desempenho ideal.

>[!TIP]
>
>Para saber mais sobre como usar transformações e pré-processar seus dados, consulte a [documentação de técnicas de transformação de recursos](../feature-transformation.md).

1. Para preencher valores nulos em colunas numéricas, de cadeia de caracteres e booleanas, use as funções `numeric_imputer`, `string_imputer` e `boolean_imputer` respectivamente. Esta etapa garante que o algoritmo de aprendizado de máquina possa processar os dados sem erros.
2. Aplicar transformações de recursos para preparar os dados para modelagem. Aplique `binarized`, `quantile_discretizer` ou `string_indexer` para categorizar ou padronizar as colunas. Em seguida, alimente a saída dos imputers (`numeric_imputer` e `string_imputer`) nos transformadores subsequentes, como `string_indexer` ou `quantile_discretizer`, para criar recursos significativos.
3. Use a função `vector_assembler` para combinar as colunas transformadas em uma única coluna de recurso. Em seguida, dimensione os recursos usando `min_max_scaler` para normalizar os valores para obter um melhor desempenho do modelo. Observação: No exemplo SQL, a última transformação mencionada na cláusula TRANSFORM torna-se a coluna de recurso usada pelo modelo de aprendizado de máquina.
4. Especifique o tipo de modelo e quaisquer outros hiperparâmetros na cláusula OPTIONS. Por exemplo, `decision_tree_classifier` foi escolhido aqui porque este é um problema de classificação. Outros parâmetros como `max_depth` foram ajustados (`MAX_DEPTH=4`) para ajustar o modelo a fim de obter melhor desempenho.
5. Combine recursos e rotule os dados de saída. Use a cláusula SELECT para especificar o conjunto de dados para treinamento. Esta cláusula deve incluir as colunas de recurso (`count_per_id`, `web`, `id`) e a coluna de rótulo (`isBot`), que indica se uma ação provavelmente será um bot.

Sua declaração pode ser semelhante ao exemplo abaixo.

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**Resultado**

Nos resultados exibidos abaixo, o modelo `bot_filtering_model` foi criado com êxito com uma ID, um nome e uma versão exclusivos. Essa saída serve como uma referência para rastrear e gerenciar modelos. Use essas referências para identificar a configuração e a versão exatas necessárias para previsões ou avaliações.

```console
           Created Model ID           |       Created Model       | Version
|--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### Avaliar o modelo treinado {#evaluate-trained-model}

Depois de criar o modelo, use o comando `MODEL_EVALUATE` para avaliar seu desempenho. Esta etapa garante que o modelo atenda aos requisitos de precisão e desempenho para detectar a atividade de bot.

Use os seguintes argumentos no comando SQL para avaliar o modelo:

1. Especifique o nome do modelo (`bot_filtering_model`) para indicar qual modelo avaliar. Este nome deve corresponder ao que você criou anteriormente com o comando `CREATE MODEL`.
2. Forneça a versão do modelo (`1`) no segundo argumento para especificar a versão do modelo que você deseja avaliar. Se houver várias versões, isso garante que a versão correta seja usada.
3. Inclua o conjunto de dados de avaliação para definir o conjunto de dados para avaliação. Verifique se o conjunto de dados inclui as mesmas colunas de recurso (`count_per_id`, `web`, `id`) e a coluna de rótulo (`isBot`) usada durante o treinamento.

>[!NOTE]
>
>As transformações aplicadas durante o treinamento do modelo são automaticamente aplicadas durante a avaliação.

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**Resultado**

A resposta inclui métricas como precisão, precisão, recuperação e AUC-ROC. Os resultados confirmam se o modelo teve ou não bom desempenho.

>[!NOTE]
>
>Valores no intervalo de 0 a 1 representam proporções ou probabilidades, com 1,0 indicando desempenho perfeito.

```console
auc_roc | accuracy | precision | recall
|---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **Métrica** | **Descrição** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | Essa métrica indica com que eficiência seu modelo pode classificar bots e não bots. É amplamente usado para avaliar modelos de classificação. |
| `accuracy` | A porcentagem de previsões corretas feitas pelo modelo. |
| `precision` | A proporção de previsões de bots verdadeiros entre todos os bots previstos. |
| `recall` | A proporção de bots verdadeiros detectados de todos os bots reais. |

>[!TIP]
>
>Para uso em sandboxes de produção, considere avaliar o modelo em conjuntos de dados de teste para garantir que ele se generalize de maneira eficaz.

### Prever atividade de bot {#predict-bot-activity}

Use o comando `MODEL_PREDICT` com o modelo treinado para identificar quais usuários (`id`) são bots. Siga as etapas abaixo para gerar previsões para identificar a atividade de bot:

1. Use o nome do modelo (`bot_filtering_model`) no primeiro argumento para especificar qual modelo usar para previsões.
2. Especifique a versão do modelo (`1`) no segundo argumento para garantir que a versão correta do modelo seja usada.
3. Para fornecer os dados corretos para previsões, use uma instrução SELECT para especificar as colunas de recursos (`count_per_id`, `web`, `id`). Não inclua a coluna de rótulo (`isBot`) porque o modelo gerará previsões para este campo.

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**Resultado**

A resposta inclui previsões para cada usuário (`id`), juntamente com detalhes sobre sua atividade e o resultado de classificação do modelo. Essa saída permite um exame detalhado do comportamento do usuário e da classificação do modelo da atividade de bot.

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
|---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

A tabela abaixo explica cada métrica:

| Nome da coluna | Descrição |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | O identificador exclusivo de cada usuário. |
| `count.one_minute` | A contagem de cliques agregada para intervalos de 1 minuto. |
| `count.five_minute` | A contagem de cliques agregada para intervalos de 5 minutos. |
| `count.thirty_minute` | A contagem de cliques agregada é para intervalos de 30 minutos. |
| `web.webpagedetails.name` | O nome da página da Web visitada. Isso fornece o contexto para a atividade do usuário. |
| `prediction` | A previsão do modelo. Um resultado `1.0` indica que o usuário está sinalizado como um bot com base em seus padrões de atividade. |

## Gerenciar seus modelos {#manage-models}

Para gerenciar seus modelos de aprendizado de máquina, use as palavras-chave SQL listadas na seção abaixo.

### Listar modelos disponíveis {#list-available-models}

Gerencie e revise com eficiência os modelos com o comando `SHOW MODELS;`. Este comando lista todos os modelos de aprendizado de máquina que foram criados no espaço de trabalho atual. A saída fornece uma visão geral dos modelos disponíveis e inclui seus nomes, versões e outros metadados.

```sql
SHOW MODELS;
```

### Excluir modelos {#delete-models}

Para liberar recursos e garantir que somente modelos relevantes sejam mantidos, use o comando `DROP MODEL` para remover modelos obsoletos ou desnecessários. Esse comando exclui qualquer modelo de aprendizado de máquina especificado após as palavras-chave. No exemplo abaixo, o `bot_filtering_model` é removido do sistema.

```sql
DROP MODEL bot_filtering_model;
```

## Próximas etapas

Ao ler este documento, você aprendeu a identificar e filtrar a atividade de bot usando técnicas SQL e de aprendizado de máquina com os métodos do Data Distiller. Em seguida, aplique esses conceitos a seus conjuntos de dados e automatize o novo treinamento do modelo para melhoria contínua.
