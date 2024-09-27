---
title: Análise eficiente de big data com hipercubos no serviço de consulta de experiência
description: Saiba como usar hipercubos no Serviço de consulta do Adobe Experience Platform para otimizar a análise de big data com contagem exclusiva aproximada, reduzindo a necessidade de reprocessamento completo de dados.
source-git-commit: 67d4bcbf2a055d4427218ba7d98355f09d860a8c
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 2%

---

# Análise eficiente de big data com hipercubos

>[!AVAILABILITY]
>
>Esta funcionalidade só está disponível para usuários que compraram a [SKU do Data Distiller](../data-distiller/overview.md). Entre em contato com o representante da Adobe para obter mais informações.

Saiba como usar hipercubos no Serviço de consulta de experiência da Adobe Experience Platform para executar análise avançada de dados com eficiência aprimorada. Este documento aborda como usar funções avançadas da [[!DNL Apache Datasketches] biblioteca](https://datasketches.apache.org/) para lidar com contagens distintas e cálculos complexos de forma incremental, sem precisar reprocessar dados históricos a cada vez.

Na análise de big data, a geração de métricas como contagens, quantis, itens mais frequentes, junções e análises de gráfico distintas geralmente envolve contagem não aditiva (em que os resultados não podem simplesmente ser somados de subgrupos). Os métodos tradicionais exigem o reprocessamento de todos os dados históricos, o que pode consumir muitos recursos e muito tempo. Use rascunhos, que são resumos compactos que usam probabilidades para representar grandes conjuntos de dados, e funções avançadas do Serviço de consulta para simplificar esse processo, reduzindo a necessidade de recálculo.

## Funções principais dos hipercubos {#key-functions}

Os hipercubos oferecem várias funções avançadas para melhorar a eficiência e a flexibilidade da análise de dados.

1. **Contar usuários exclusivos ou consultas distintas**: use os recursos SQL para gerar contagens exclusivas de usuários que interagem com várias dimensões de dados, como exibições de produtos, visitas a sites ou atividades de comércio, sem reanalisar repetidamente os dados brutos.
2. **Processamento incremental**: execute atualizações incrementais para dobrar e mesclar pontos de dados entre dimensões e tempo sem recalcular tudo do zero.
3. **Análise multidimensional**: os hipercubos permitem filtragem multidimensional e reorganização de dados para criar linhas de resumo que representam combinações de dimensões. Esses resumos podem ser usados para gerar insights com sobrecarga mínima de computação.

## Casos de uso para hipercubos {#use-cases}

Use hipercubos para gerar contagens distintas com eficiência para várias interações de usuário sem recalcular totalmente os dados a cada vez. A seguir estão alguns cenários práticos para seu uso:

- Analise visitantes únicos que visualizam produtos específicos durante um período definido.
- Identifique usuários que interagem com vários produtos em um determinado período para aprimorar a análise de venda cruzada.
- Diferencie os usuários que interagem com um produto, mas não com outro, ao longo do tempo, para descobrir padrões de preferência.
- Combine dados de interação online e offline para obter uma visão abrangente do comportamento do usuário em um determinado período.
- Rastreie o movimento do usuário em diferentes atividades em um evento para otimizar o layout e os serviços.

## Benefícios do uso de hipercubos

Nessas situações, você pode pré-calcular informações básicas para categorias específicas. No entanto, ao analisar dados em várias dimensões e períodos, você precisa recalcular tudo, desde dados brutos, até usar um hipercubo do Serviço de consulta. Os hipercubos simplificam o processo organizando os dados com eficiência, o que permite uma filtragem flexível e uma análise multidimensional sem reprocessamento. Eles usam funções avançadas para estimar resultados com rapidez e precisão, oferecendo benefícios importantes como melhor eficiência de processamento, escalabilidade e adaptabilidade para tarefas analíticas complexas.

### Eficiência de tamanho de dados para processamento de consulta

O Serviço de consulta pode compactar milhões ou bilhões de pontos de dados (por exemplo, IDs de usuário) em um formato compacto chamado rascunho. Esse rascunho tem um tamanho de dados significativamente reduzido para o processamento de consultas, o que mantém a escalabilidade e torna o trabalho muito mais fácil e rápido. Não importa o tamanho dos dados originais, o tamanho do rascunho permanece pequeno, o que torna a análise de grandes dados muito mais gerenciável e eficiente.

O diagrama abaixo ilustra como o Commerce, as Informações do produto e a ExperienceEvents para dimensões da Web são processados em rascunhos, que são usados para aproximar contagens exclusivas.

![Infográfico que mostra a criação de rascunhos usando o Serviço de Consulta. O diagrama ilustra como ExperienceEvents com Commerce, Informações do Produto e dimensões da Web são processados em rascunhos, que são usados para aproximar contagens exclusivas.](../images/hypercubes/hypercube-overview.png)

### Mesclar rascunhos para tornar a análise de dados mais rápida e fácil

Para evitar recalcular e melhorar a velocidade de processamento, você pode mesclar rascunhos de diferentes categorias ou grupos. O Serviço de consulta também simplifica o design organizando os dados em um hipercubo, em que cada linha se torna um resumo da partição (uma coleção de dimensões) ao lado da coluna de rascunho. Cada linha do hipercubo contém a combinação de dimensão, mas não tem dados brutos. Ao executar uma consulta, especifique as colunas dimensionais que deseja usar para criar métricas aditivas e mescle os rascunhos dessas linhas.

![O diagrama mostra como os rascunhos de diferentes ExperienceEvents são mesclados para criar contagens exclusivas aproximadas em várias dimensões.](../images/hypercubes/merge-sketches.png)

### Relação custo-eficácia {#cost-effectiveness}

Os dados do cliente geralmente são em grande escala, mas você pode eliminar a necessidade de reprocessar dados históricos usando processamento incremental. Os rascunhos são muito menores e permitem resultados mais rápidos em tempo real, economizando recursos e custos de computação. Essa transformação de dados torna as queries interativas mais viáveis e eficientes.

## Visão geral das funções

Esta seção descreve como cada função otimiza o processamento de dados e aprimora os recursos analíticos por meio do uso eficiente de rascunhos e hipercubos. Ela detalha a finalidade, a sintaxe do exemplo, os parâmetros e a saída esperada.

### Criar estimativas de contagem exclusivas com rascunhos HLL

`hll_build_agg` é uma função agregada que cria um rascunho HLL (HyperLogLog). Essa função é um método probabilístico compacto para estimar o número de valores únicos em uma coluna ou expressão em um conjunto de dados agrupado.

#### Definição de função

```sql
hll_build_agg(column [, lgConfigK])
```

**Uso:**

O exemplo a seguir demonstra como a função pode ser estruturada em uma consulta.

```sql
SELECT
   [dim1, dim2 ... ,] hll_build_agg(coalesce(col1, col2, col3)) AS sketch_col
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parâmetros

| Parâmetro | Descrição |
|---------------------------|---------------------------------------|
| `column` | O nome da coluna ou da coluna na qual criar um rascunho. |
| `lgConfigK` | *Int* (Opcional) O log-base-2 de K, onde K é o número de compartimentos ou slots para o HLL Sketch. Valor mínimo: 4. Valor máximo: 12. Valor padrão: 12. |

#### Saída

| Coluna de saída | Descrição |
|---------------------------|---------------------------------------|
| `sketch_res` | Uma coluna do tipo string que contém o rascunho HLL codificado. |

#### Exemplo de SQL

O exemplo a seguir cria um rascunho agregado na coluna `customer_id`:

```sql
SELECT
  country,
  hll_build_agg(customer_id, 10) AS sketch
FROM
  EXPLODE(
    ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
      ('UA', 'customer_id_1', 'invoice_id_11'),
      ('CZ', 'customer_id_2', 'invoice_id_22'),
      ('CZ', 'customer_id_2', 'invoice_id_23'),
      ('BR', 'customer_id_3', 'invoice_id_31'),
      ('UA', 'customer_id_2', 'invoice_id_24')
    ])
GROUP BY country;
```

**Saída de exemplo SQL:**

| País | Sketch |
|---------|------------------------------------------------------------|
| UA | AgEHBAMAAgCR9mUEulKCQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| CZ | AgEHBAMAAAQC6UooJAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA= |
| BR | AgEHBAMAAQCcmH0HAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA= |

### Estimar contagens distintas com rascunhos HLL

`hll_estimate` é uma função escalar que fornece uma estimativa da contagem distinta em cada linha de um conjunto de dados. Ao contrário das funções de agregação, `hll_estimate` opera em nível de linha e é usado para estimar a contagem distinta de um rascunho em linhas individuais.

>[!NOTE]
>
>Esta função não pode ser usada como uma função agregada. Para contagens agregadas, use `sketch_count`.

#### Definição de função

```sql
hll_estimate(sketch_col)
```

**Uso:**

O exemplo a seguir demonstra como a função pode ser estruturada em uma consulta.

```sql
SELECT
   [col1, col2 ... ,] hll_estimate(sketch_column) AS estimate
FROM fact_sketch_table
```

#### Parâmetros

| Parâmetro | Descrição |
|---------------------------|---------------------------------------|
| `sketch_column` | Coluna que contém um esboço HLL estriado. Ele estima a contagem distinta para o rascunho em cada linha. |

#### Saída

| Coluna de saída | Descrição |
|---------------------------|---------------------------------------|
| `estimate` | Uma coluna do tipo double que fornece a estimativa do esboço, arredondada para duas casas decimais. |

#### Exemplo de SQL

O exemplo a seguir estima a contagem distinta de clientes por país usando a função `hll_estimate` em um rascunho HLL:

```sql
SELECT
  country,
  hll_estimate(hll_build_agg(customer_id, 10)) AS distinct_customers_by_country
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id, 10) AS sketch
    FROM 
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
  );
```

**Saída de Exemplo SQL:**

| País | distinct_customers_by_country |
|---------|-------------------------------|
| UA | 2,00 |
| CZ | 1,00 |
| BR | 1,00 |

### Mesclar vários rascunhos HLL com `hll_merge_agg`

`hll_merge_agg` é uma função agregada que mescla vários rascunhos HLL em um grupo, produzindo um novo rascunho como saída. Ele permite a combinação de rascunhos em partições ou dimensões, melhorando a flexibilidade da análise de dados.

#### Definição de função

```sql
hll_merge_agg(sketch_col [, allowDifferentLgConfigK])
```

**Uso:**

O exemplo a seguir demonstra como a função pode ser estruturada em uma consulta.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_agg(sketch_column.sketch) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parâmetros

| Parâmetro | Descrição |
|---------------------------|---------------------------------------|
| `sketch_column` | Coluna que contém o esboço HLL estriado. |
| `allowDifferentLgConfigK` | *Booleano* (Opcional) Se definido como verdadeiro, permite mesclar rascunhos com valores `lgConfigK` diferentes. O valor padrão é false. Uma exceção será lançada se o valor for falso e os rascunhos tiverem valores `lgConfigK` diferentes. |

>[!NOTE]
>
>Se `allowDifferentLgConfigK` estiver definido como falso, a mesclagem de rascunhos com diferentes valores de `lgConfigK` resultará em um `UnsupportedOperationException`.

#### Saída

| Coluna de saída | Descrição |
|----------------|-------------------------------------------------|
| `sketch_res` | Uma coluna do tipo esboço HLL que contém o esboço HLL mesclado restrito. |

#### Exemplo de SQL

O exemplo a seguir mescla vários rascunhos HLL na coluna `customer_id`:

```sql
SELECT
   hll_merge_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**Saída de Exemplo SQL:**

| País | hll_merge_agg(rascunho, true) |
|---------|--------------------------------------------|
| UA | AgEHDAMAAwiR9mUEulKCQAAAAAAAAAAAAAAAAA== |
| CZ | AgEHDAMAAQi6UooJAAAAAAAAAAAAAAAAAAAAAAAAAA= |
| BR | AgEHDAMAAQicmH0HAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| MX | AgEHFQMAAgiGL/kNdAAAAAAAAAAAAAAAAAAAAAAAAA== |

### Estimar cardinalidade com `hll_merge_count_agg`

`hll_merge_count_agg` é uma função agregada que estima a cardinalidade (número de elementos únicos) de um ou mais rascunhos em uma coluna. Retorna uma única estimativa para todos os rascunhos encontrados no agrupamento. Esta função é usada para agregar rascunhos e não pode ser usada como uma transformação em nível de linha. Para estimativas em linhas, use `sketch_estimate`.

#### Definição de função

```sql
hll_merge_count_agg(sketch_col [, allowDifferentLgConfigK])
```

**Uso:**

O exemplo a seguir demonstra como a função pode ser estruturada em uma consulta.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_count_agg(sketch_column) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parâmetros

| Parâmetro | Descrição |
|-------------------------|----------------------------------------------|
| `sketch_column` | Uma coluna contendo o esboço HLL estriado. |
| `allowDifferentLgConfigK` | *Booleano* (Opcional) O valor padrão é falso. Se definido como verdadeiro, permite a mesclagem de rascunhos com diferentes valores de `lgConfigK`. Caso contrário, um `UnsupportedOperationException` é lançado. |

#### Saída

| Coluna de saída | Descrição |
|---------------|----------------------------------------------------------|
| `estimate` | Uma coluna do tipo Double com a estimativa do esboço. |

#### Exemplo de SQL

O exemplo a seguir estima o número de clientes únicos com faturas usando a função `hll_merge_count_agg`:

```sql
SELECT
   hll_merge_count_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**Saída de Exemplo SQL:**

| País | hll_merge_count_agg(rascunho, true) |
|---------|----------------------------------|
| UA | 2.0 |
| CZ | 1,0 |
| BR | 1,0 |
| MX | 2.0 |

## Limitações

Atualmente, rascunhos não podem ser atualizados após serem criados. Atualizações futuras introduzirão a capacidade de atualizar rascunhos. Com essa funcionalidade, você pode lidar com execuções perdidas e dados de chegada tardia com mais eficiência.

## Próximas etapas

Após a leitura desse documento, agora você sabe como usar hipercubos e funções de rascunho associadas para executar um processamento de dados eficiente para análises complexas e multidimensionais, sem a necessidade de reprocessar dados históricos. Essa abordagem economiza tempo, reduz custos e oferece a flexibilidade necessária para consultas interativas em tempo real, tornando-a uma ferramenta valiosa para a análise de big data no Adobe Experience Platform.

Em seguida, explore outros conceitos importantes, como [carregamento incremental](../key-concepts/incremental-load.md) e [desduplicação de dados](../key-concepts/deduplication.md), para aprofundar sua compreensão de como usar essas funções com eficiência para suas necessidades de dados específicas.


