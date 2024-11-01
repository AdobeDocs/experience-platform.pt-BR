---
title: Extensão SQL de engenharia de recursos
description: Saiba mais sobre a extensão SQL de engenharia de recursos do Data Distiller para pré-processar dados para modelagem estatística avançada. Ele aborda as técnicas disponíveis de extração, transformação e seleção de recursos.
role: Developer
source-git-commit: 1fcfb5c41750e853daaf036ceaae3527b805391c
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Extensão SQL de engenharia de recursos

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que compraram o complemento Data Distiller. Para obter mais informações, entre em contato com o(a) representante da Adobe.

Para atender às suas necessidades de engenharia de recursos, use a extensão do transformador SQL para simplificar e automatizar o pré-processamento de dados. Use essa extensão para criar recursos e aproveitar a experimentação contínua com diferentes técnicas de engenharia de recursos, incluindo a associação deles a modelos. Projetado para computação distribuída, você pode realizar a engenharia de recursos em grandes conjuntos de dados de maneira paralela e escalável, reduzindo significativamente o tempo necessário para o pré-processamento de dados com a extensão SQL de engenharia de recursos do Data Distiller.

## Visão geral da técnica {#technique-overview}

Os recursos de engenharia de recursos abrangem três áreas principais: Extração de recursos, Transformação de recursos e Seleção de recursos. Cada área inclui funções específicas projetadas para extrair, converter, focalizar e melhorar o pré-processamento de dados.

### Extração de recursos {#feature-extraction}

Extraia informações relevantes de seus dados, especialmente dados de texto, e converta-os em um formato numérico que os modelos compatíveis possam consumir ou transformar e derivar conjuntos de dados. Use as seguintes funções para executar a extração de recursos:

- **[Transformador textual](./feature-transformation.md#textual-transformations)**: converta dados textuais em recursos numéricos.
- **[Vetorizador de Contagem](./feature-transformation.md#countvectorizer)**: transforma uma coleção de documentos de texto em vetores de contagens de token.
- **[N-grama](./feature-transformation.md#ngram)**: gerar sequências de n-gramas a partir de dados de texto.
- **[Removedor de Palavras Irrelevantes](./feature-transformation.md#stopwordsremover)**: filtre palavras comuns que não tenham significado significativo.
- **[TF-IDF](./feature-transformation.md#tf-idf)**: Meça a importância das palavras em um documento em relação a um corpo.
- **[Tokenizer](./feature-transformation.md#tokenizer)**: dividir o texto em termos individuais (palavras).
- **[Word2Vec](./feature-transformation.md#word2vec)**: mapear palavras para vetores de tamanho fixo e criar incorporações de palavras.

### Transformação de recursos {#feature-transformation}

Além de extrair recursos, use os seguintes transformadores gerais para preparar seus recursos para modelos estatísticos avançados e conjuntos de dados derivados. Aplique dimensionamento, normalização ou codificação para garantir que seus recursos estejam na mesma escala e tenham uma distribuição semelhante.

#### Transformadores gerais

Veja abaixo uma lista de ferramentas para processar uma grande variedade de tipos de dados para aprimorar o fluxo de trabalho de pré-processamento de dados.

- **[Imputador Numérico](./feature-transformation.md#numeric-imputer)**: preencher valores ausentes em colunas numéricas com um
- **[Imputador de Cadeia de Caracteres](./feature-transformation.md#string-imputer)**: Substitua os valores de cadeia de caracteres ausentes por um especificado
- **[Assembler de Vetor](./feature-transformation.md#vector-assembler)**: Combine várias colunas em uma única coluna de vetor.

#### Transformadores numéricos

Aplique essas técnicas para processar e dimensionar dados numéricos de maneira eficaz e obter um melhor desempenho do modelo.

- **[Binarizador](./feature-transformation.md#binarizer)**: converte recursos contínuos em valores binários com base em um limite.
- **[Bucketizer](./feature-transformation.md#bucketizer)**: mapeie recursos contínuos em compartimentos discretos.
- **[Escalonador Mín-Máx](./feature-transformation.md#minmaxscaler)**: redimensione os recursos para um intervalo especificado, normalmente [0, 1].
- **[Escalonador Abs Máx](./feature-transformation.md#maxabsscaler)**: redimensiona os recursos para o intervalo [-1, 1] sem alterar a dispersão.
- **[Normalizador](./feature-transformation.md#normalizer)**: normalize os vetores para ter uma norma de unidade.
- **[Discretizer de Quantidade](./feature-transformation.md#quantilediscretizer)**: converta recursos contínuos em recursos categóricos compartimentando-os em quantis.
- **[Escalonador Padrão](./feature-transformation.md#standardscaler)**: Normalize os recursos para ter um desvio padrão de unidade e/ou média zero.

#### Transformadores categóricos

Use esses transformadores para converter e codificar dados categóricos em formatos adequados para modelos de aprendizado de máquina.

- **[Indexador de Cadeia de Caracteres](./feature-transformation.md#stringindexer)**: converta dados de cadeia de caracteres categóricos em índices numéricos.
- **[One Hot Encoder](./feature-transformation.md#onehotencoder)**: mapeie dados categóricos em vetores binários.

### Seleção de recursos {#feature-selection}

Em seguida, concentre-se em selecionar um subconjunto dos recursos mais importantes do conjunto original. Esse processo ajuda a reduzir a dimensionalidade dos dados, facilitando o processamento dos modelos e melhorando o desempenho geral do modelo.

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## Implementar a cláusula OPTIONS {#options-clause}

Ao definir seu modelo, use a cláusula `OPTIONS` para especificar o algoritmo e seus parâmetros. Comece definindo o parâmetro `type` para indicar o algoritmo que você está usando, como `K-Means`. Em seguida, defina os parâmetros relevantes na cláusula `OPTIONS` como pares de valores-chave para ajustar o modelo. Entenda que alguns parâmetros podem ser posicionais e exigir que todos os parâmetros anteriores sejam especificados se forem fornecidos valores personalizados. Se você optar por não personalizar determinados parâmetros, o sistema aplicará as configurações padrão. Consulte a documentação relevante para entender a função de cada parâmetro e os valores padrão.

### Próximas etapas

Depois de aprender as técnicas de engenharia de recursos descritas neste documento, vá para o documento [Modelos](./models.md). Ele orienta você pelo processo de criação, treinamento e gerenciamento de modelos confiáveis usando os recursos que você projetou. Depois que seus modelos forem criados, prossiga para o [Documento Implementar modelos estatísticos avançados.](./implement-models/implement-models.md). Este documento serve como uma visão geral, vinculando a guias detalhados para diferentes técnicas de modelagem, incluindo clustering, classificação e regressão. Ao seguir esses documentos, você aprenderá a configurar e implementar vários modelos confiáveis em seus workflows de SQL e a otimizar seus modelos para análise avançada de dados.
