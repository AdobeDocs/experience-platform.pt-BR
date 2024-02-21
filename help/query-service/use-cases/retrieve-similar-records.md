---
title: Recuperar Registros Semelhantes com Funções de Ordem Superior
description: Saiba como identificar e recuperar registros semelhantes ou relacionados de um ou mais conjuntos de dados com base em uma métrica de similaridade e limite de similaridade. Esse fluxo de trabalho pode destacar relações significativas ou sobreposições entre conjuntos de dados diferentes.
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 27eab04e409099450453a2a218659e576b8f6ab4
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 3%

---

# Recuperar registros semelhantes com funções de ordem superior

Use as funções de ordem superior do Data Distiller para resolver vários casos de uso comuns. Para identificar e recuperar registros semelhantes ou relacionados de um ou mais conjuntos de dados, use as funções de filtragem, transformação e redução, conforme detalhado neste guia. Para saber como funções de ordem superior podem ser usadas para processar tipos de dados complexos, consulte a documentação sobre como [gerenciar tipos de dados de matriz e mapa](../sql/higher-order-functions.md).

Use este guia para identificar produtos de diferentes conjuntos de dados que tenham uma semelhança significativa em suas características ou atributos. Essa metodologia fornece soluções para: desduplicação de dados, vinculação de registros, sistemas de recomendação, recuperação de informações e análise de texto, entre outras.

O documento descreve o processo de implementação de uma junção de similaridade, que usa funções de ordem superior do Data Distiller para calcular a similaridade entre conjuntos de dados e filtrá-los com base em atributos selecionados. São fornecidos trechos de código SQL e explicações para cada etapa do processo. O workflow implementa junções de similaridade usando a medida de similaridade Jaccard e a tokenização usando funções de ordem superior do Data Distiller. Esses métodos são usados para identificar e recuperar registros semelhantes ou relacionados de um ou mais conjuntos de dados com base em uma métrica de similaridade. As principais seções do processo incluem: [geração de tokens usando funções de ordem superior](#data-transformation), o [junção cruzada de elementos únicos](#cross-join-unique-elements), o [Cálculo de similaridade de cartão](#compute-the-jaccard-similarity-measure), e o [filtragem baseada em limite](#similarity-threshold-filter).

## Pré-requisitos

Antes de continuar com este documento, você deve se familiarizar com os seguintes conceitos:

- A **junção de similaridade** é uma operação que identifica e recupera pares de registros de uma ou mais tabelas com base em uma medida de similaridade entre os registros. Os principais requisitos para uma junção de similaridade são os seguintes:
   - **Métrica de similaridade**: uma junção de similaridade depende de uma métrica ou medida de similaridade predefinida. Essas métricas incluem: similaridade de Jaccard, similaridade do cosseno, distância de edição, e assim por diante. A métrica depende da natureza dos dados e do caso de uso. Essa métrica quantifica a semelhança ou diferença entre dois registros.
   - **Limite**: um limite de similaridade é usado para determinar quando os dois registros são considerados semelhantes o suficiente para serem incluídos no resultado de junção. Os registros com uma pontuação de similaridade acima do limite são considerados correspondências.
- A variável **Semelhança de Jaccard** índice, ou a medida de similaridade de Jaccard, é uma estatística usada para medir a similaridade e a diversidade dos conjuntos de amostras. É definido como o tamanho da interseção dividido pelo tamanho da união dos conjuntos de amostra. A medida de similaridade de Jaccard varia de zero a um. Uma similaridade de Jaccard de zero indica nenhuma similaridade entre os conjuntos, e uma similaridade de Jaccard de um indica que os conjuntos são idênticos.
  ![Um diagrama de Venn para ilustrar a medida de similaridade de Jaccard.](../images/use-cases/jaccard-similarity.png)
- **Funções de ordem superior** no Data Distiller são ferramentas dinâmicas e em linha que processam e transformam dados diretamente em instruções SQL. Essas funções versáteis eliminam a necessidade de várias etapas na manipulação de dados, especialmente quando [lidar com tipos complexos como arrays e mapas](../sql/higher-order-functions.md). Ao melhorar a eficiência da consulta e simplificar as transformações, as funções de alto nível contribuem para uma análise mais ágil e uma melhor tomada de decisões em vários cenários de negócios.

## Introdução

O SKU do Data Distiller é necessário para executar as funções de ordem superior nos dados do Adobe Experience Platform. Se você não tiver o Data Distiller SKU, entre em contato com o representante do serviço de atendimento ao cliente da Adobe para obter mais informações.

## Estabelecer similaridade {#establish-similarity}

Este caso de uso requer uma medida de similaridade entre cadeias de texto que podem ser usadas posteriormente para estabelecer um limite para filtragem. Neste exemplo, os produtos no Conjunto A e no Conjunto B representam as palavras em dois documentos.

A medida de similaridade de Jaccard pode ser aplicada a uma grande variedade de tipos de dados, incluindo dados de texto, dados categóricos e dados binários. Também é adequado para processamento em tempo real ou em lote, pois pode ser computacionalmente eficiente para calcular conjuntos de dados grandes.

O Conjunto de produtos A e o Conjunto B contêm os dados de teste para esse workflow.

- Conjunto de produtos A: `{iPhone, iPad, iWatch, iPad Mini}`
- Conjunto de produtos B: `{iPhone, iPad, Macbook Pro}`

Para calcular a similaridade de Jaccard entre os conjuntos de produtos A e B, primeiro encontre o **interseção** (elementos comuns) dos conjuntos de produtos. Nesse caso, `{iPhone, iPad}`. Em seguida, localize o **união** (todos os elementos únicos) de ambos os conjuntos de produtos. Neste exemplo, `{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`.

Finalmente, use a fórmula de similaridade Jaccard: `J(A,B) = A∪B / A∩B` para calcular a semelhança.

J = Distância Jaccard A = set 1 B = set 2

A similaridade de Jaccard entre os conjuntos de produtos A e B é de 0,4. Isso indica um grau moderado de similaridade entre as palavras usadas nos dois documentos. Essa similaridade entre os dois conjuntos define as colunas na junção de similaridade. Essas colunas representam informações, ou características associadas aos dados, que são armazenadas em uma tabela e usadas para executar os cálculos de similaridade.

### Computação de Jaccard emparelhada com similaridade de strings {#pairwise-similarity}

Para comparar com mais precisão as semelhanças entre as cadeias de caracteres, a similaridade emparelhada deve ser calculada. A similaridade emparelhada divide objetos altamente dimensionais em objetos dimensionais menores para comparação e análise. Para fazer isso, uma cadeia de caracteres de texto é dividida em partes ou unidades menores (tokens). Elas podem ser letras individuais, grupos de letras (como sílabas) ou palavras inteiras. A similaridade é calculada para cada par de tokens entre cada elemento no Conjunto A com cada elemento no Conjunto B. Essa geração de tokens fornece uma base para comparações analíticas e computacionais, relações e insights a serem obtidos dos dados.

Para o cálculo de similaridade em pares, este exemplo usa bigramas de caracteres (dois tokens de caracteres) para comparar uma correspondência de similaridade entre as strings de texto dos produtos no Conjunto A e no Conjunto B. Um bigrama é uma sequência consecutiva de dois itens ou elementos em uma determinada sequência ou texto. Você pode generalizar isso para n-gramas.

Este exemplo pressupõe que o caso não importa e que os espaços não devem ser contabilizados. De acordo com esses critérios, o conjunto A e o conjunto B têm os seguintes bigramas:

Conjunto de produtos A, em gramas:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- iWatch (5): &quot;iw&quot;, &quot;wa&quot;, &quot;at&quot;, &quot;tc&quot;, &quot;ch&quot;
- iPad Mini (7): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;, &quot;dm&quot;, &quot;mi&quot;, &quot;in&quot;, &quot;ni&quot;

Grupo de produtos B, em bigramas:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- Macbook Pro (9): &quot;Ma&quot;, &quot;ac&quot;, &quot;cb&quot;, &quot;bo&quot;, &quot;oo&quot;, &quot;ok&quot;, &quot;kp&quot;, &quot;pr&quot;, &quot;ro&quot;

Em seguida, calcule o coeficiente de similaridade de Jaccard para cada par:

|                   | iPhone (Conjunto B) | iPad (Conjunto B) | Macbook Pro (Conjunto B) |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone (Conjunto A) | (Interseção: 5, União: 5) = 5 / 5 = 1 | (Interseção: 1, União: 7) =1 / 7 ≈ 0.14 | (Interseção: 0, União: 14) = 0 / 14 = 0 |
| iPad (Conjunto A) | (Interseção: 1, União: 7) = 1 / 7 ≈ 0,14 | (Interseção: 3, União: 3) = 3 / 3 = 1 | (Interseção: 0, União: 12) = 0 / 12 = 0 |
| iWatch (conjunto A) | (Interseção: 0, União: 8) = 0 / 8 = 0 | (Interseção: 0, União: 8) = 0 / 8 = 0 | (Interseção: 0, União: 8) = 0 / 8 =0 |
| iPad Mini (Conjunto A) | (Interseção: 1, União: 11) = 1 / 11 ≈ 0,09 | (Interseção: 3, União: 7) = 3 / 7 ≈ 0,43 | (Interseção: 0, União: 16) = 0 / 16 = 0 |

{style="table-layout:auto"}

## Criar os dados de teste com SQL {#create-test-data}

Para criar manualmente uma tabela de teste para os conjuntos de produtos, use a instrução SQL CREATE TABLE.

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

As descrições a seguir fornecem um detalhamento do bloco de código SQL acima:

- Linha 1: `CREATE TEMP TABLE featurevector1 AS`: essa instrução cria uma tabela temporária chamada `featurevector1`. Normalmente, as tabelas temporárias só podem ser acessadas na sessão atual e são descartadas automaticamente no final da sessão.
- Linhas 1 e 2: `SELECT * FROM (...)`: essa parte do código é uma subconsulta usada para gerar os dados inseridos na variável `featurevector1` tabela.
Dentro da subconsulta, vários `SELECT` são combinadas usando o `UNION ALL` comando. Each `SELECT` gera uma linha de dados com os valores especificados para a variável `ProductName` coluna.
- Linha 3: `SELECT 'iPad' AS ProductName`: gera uma linha com o valor `iPad` no `ProductName` coluna.
- Linha 5: `SELECT 'iPhone'`: gera uma linha com o valor `iPhone` no `ProductName` coluna.

A instrução SQL cria uma tabela como visto abaixo:

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

Para criar o segundo vetor de recurso, use a seguinte instrução SQL:

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## Transformações de dados {#data-transformation}

Neste exemplo, várias ações devem ser executadas para comparar com precisão os conjuntos. Primeiro, todos os espaços em branco são removidos dos vetores de recursos, pois assume-se que não contribuem para a medida de similaridade. Em seguida, quaisquer duplicatas presentes no vetor de recurso são removidas, pois desperdiçam o processamento computacional. Em seguida, tokens de dois caracteres (bigramas) são extraídos dos vetores de recursos. Neste exemplo, supõe-se que estejam sobrepostas.

>[!NOTE]
>
>Para fins de ilustração, as colunas processadas são adicionadas ao lado do vetor de recurso para cada uma das etapas.

As seções a seguir ilustram as transformações de dados de pré-requisito, como desduplicação, remoção de espaços em branco e conversão de minúsculas, antes de iniciar o processo de geração de tokens.

### Desduplicação {#deduplication}

Em seguida, use o `DISTINCT` para remover duplicatas. Não há duplicatas neste exemplo, no entanto, é uma etapa importante para melhorar a precisão de qualquer comparação. O SQL necessário é exibido abaixo:

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### Remoção de espaço em branco {#whitespace-removal}

Na instrução SQL a seguir, os espaços em branco são removidos dos vetores de recursos. A variável `replace(ProductName, ' ', '') AS featurevector1_nospaces` parte da consulta utiliza o `ProductName` coluna da `featurevector1` tabela e usa o `replace()` função. A variável `REPLACE` A função substitui todas as ocorrências de um espaço (&#39; &#39;) por uma string vazia (&#39;&#39;). Isso remove efetivamente todos os espaços da `ProductName` valores. O resultado recebe o alias de `featurevector1_nospaces`.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

Os resultados são mostrados na tabela abaixo:

|   | featurevetor1_distinct | featurevetor1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

A instrução SQL e seus resultados no segundo vetor de recurso são vistos abaixo:

+++Selecione para expandir

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

Os resultados são exibidos conforme abaixo:

|   | featurevetor2_distinct | featurevetor2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### Converter para minúsculas {#lowercase-conversion}

Em seguida, o SQL é aprimorado para converter os nomes de produtos em minúsculas e remover espaços em branco. A função inferior (`lower(...)`) é aplicada ao resultado da `replace()` função. A função inferior converte todos os caracteres no `ProductName` valores em minúsculas. Isso garante que os valores estejam em minúsculas, independentemente da caixa original.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

O resultado dessa instrução é:

|   | featurevetor1_distinct | featurevetor1_transform |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

A instrução SQL e seus resultados no segundo vetor de recurso são vistos abaixo:

+++Selecione para expandir

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

Os resultados são exibidos conforme abaixo:

|   | featurevetor2_distinct | featurevetor2_transform |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iphone |

{style="table-layout:auto"}

+++

### Extrair tokens usando SQL {#tokenization}

A próxima etapa é a geração de tokens ou a divisão de texto. Tokenization é o processo de pegar o texto e quebrá-lo em termos individuais. Normalmente, isso envolve dividir frases em palavras. Neste exemplo, as cadeias de caracteres são divididas em bigramas (e n-gramas de ordem superior) extraindo tokens usando funções SQL como `regexp_extract_all`. Bigramas sobrepostos devem ser gerados para geração de tokens eficaz.

O SQL foi aprimorado ainda mais para usar `regexp_extract_all`. `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:` Essa parte da consulta processa ainda mais os `ProductName` valores criados na etapa anterior. Ele usa o `regexp_extract_all()` função para extrair todas as subsequências não sobrepostas de um a dois caracteres das subsequências modificadas e em minúsculas `ProductName` valores. A variável `.{2}` o padrão de expressão regular corresponde a substrings de dois caracteres de comprimento. A variável `regexp_extract_all(..., '.{2}', 0)` A parte da função extrai todas as subsequências de caracteres correspondentes do texto de entrada.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

|   | featurevetor1_distinct | featurevetor1_transform | tokens |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;, &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Para melhorar ainda mais a precisão, o SQL deve ser usado para criar tokens sobrepostos. Por exemplo, a cadeia de caracteres &quot;iPad&quot; acima não tem o token &quot;pa&quot;. Para corrigir isso, alterne o operador de lookahead (usando `substring`) por uma etapa e gerar os bigramas.

Semelhante à etapa anterior, `regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):` O extrai sequências de dois caracteres do nome do produto modificado, mas começa no segundo caractere usando o `substring` para criar tokens sobrepostos. Em seguida, nas linhas 3 a 7 (`array_union(...) AS tokens`), o `array_union()` A função combina as matrizes de sequências de dois caracteres obtidas pelas duas extrações de expressão regular. Isso garante que o resultado contenha tokens exclusivos de sequências não sobrepostas e sobrepostas.

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

|   | featurevetor1_distinct | featurevetor1_transform | tokens |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;,&quot;pa&quot;,&quot;dm&quot;,&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;,&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;,&quot;ch&quot;,&quot;wa&quot;,&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;,&quot;ph&quot;,&quot;on&quot;} |

{style="table-layout:auto"}

+++

No entanto, a utilização de `substring` A solução para o problema tem limitações. Se você fizesse tokens do texto com base em trigramas (três caracteres), seria necessário usar dois `substrings` para analisar duas vezes e obter os turnos necessários. Para fazer 10 gramas, você precisaria de nove `substring` expressões. Isso faria o código inflar e se torna insustentável. O uso de expressões regulares simples não é adequado. É necessária uma nova abordagem.

### Ajustar para o comprimento do nome do produto {#length-adjustment}

O SQl pode ser melhorado com as funções de sequência e comprimento. No exemplo a seguir, `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)` O gera uma sequência de números de um até o comprimento do nome do produto modificado menos três. Por exemplo, se o nome do produto modificado for &quot;ipadmini&quot; com um comprimento de caracteres de oito, ele gerará números de um a cinco (oito a três).

A instrução abaixo extrai nomes de produtos exclusivos e depois divide cada nome em sequências de caracteres (tokens) de quatro tamanhos de caracteres, excluindo espaços e apresentando-os como duas colunas. Uma coluna mostra os nomes exclusivos de produtos e a outra mostra os tokens gerados.

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

|   | featurevetor1_distinct | tokens |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;,&quot;padm&quot;,&quot;admi&quot;,&quot;dmin&quot;,&quot;mini&quot;} |
| 2 | iPad | {&quot;ipad&quot;} |
| 3 | iWatch | {&quot;iwat&quot;,&quot;watc&quot;,&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;,&quot;phone&quot;,&quot;phone&quot;} |

{style="table-layout:auto"}

+++

### Garantir o comprimento do token definido {#ensure-set-token-length}

Condições adicionais podem ser adicionadas à instrução para garantir que as sequências geradas sejam de um comprimento específico. A instrução SQL a seguir é expandida na lógica de geração de token, tornando o `transform` é mais complexa. A instrução usa o `filter` função dentro de `transform` para garantir que as sequências geradas tenham seis caracteres. Ela trata os casos em que isso não é possível, atribuindo valores NULL a essas posições.

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

|   | featurevetor1_distinct | tokens |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;,&quot;padmin&quot;,&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {&quot;iwatch&quot;} |
| 4 | iPhone | {&quot;iphone&quot;} |

{style="table-layout:auto"}

+++

## Explorar soluções usando funções de ordem superior do Data Distiller {#higher-order-function-solutions}

Funções de ordem superior são construções poderosas que permitem implementar &quot;programação&quot; como sintaxe no Data Distiller. Eles podem ser usados para iterar uma função sobre vários valores em uma matriz.

No contexto do Data Distiller, funções de ordem mais alta são ideais para criar n-gramas e iterar sequências de caracteres.

A variável `reduce` especialmente quando usada em sequências geradas por `transform`, fornece uma maneira de obter valores cumulativos ou agregados, que podem ser fundamentais em vários processos analíticos e de planejamento.

Por exemplo, na instrução SQL abaixo, a variável `reduce()` A função agrega elementos em uma matriz usando um agregador personalizado. Ele simula um loop for para **criar as somas cumulativas de todos os números inteiros** de um a cinco. `1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`.

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Higher-order function to add numbers
    )
) AS sum_result;
```

Veja a seguir uma análise da instrução SQL:

- Linha 1: `transform` aplica a função `x -> reduce` em cada elemento gerado na sequência.
- Linha 2: `sequence(1, 5)` gera uma sequência de números de um a cinco.
- Linha 3: `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)` executa uma operação de redução para cada elemento x na sequência (de 1 a 5).
   - A variável `reduce` A função recebe um valor de acumulador inicial de 0, uma sequência de um ao valor atual de `x`e uma função de ordem superior `(acc, y) -> acc + y` para adicionar os números.
   - A função de ordem superior `acc + y` acumula a soma adicionando o valor atual `y` ao acumulador `acc`.
- Linha 8: `AS sum_result` renomeia a coluna resultante como sum_result.

Em resumo, essa função de ordem mais alta utiliza dois parâmetros (`acc` e `y`) e define a operação a ser executada, que, nesse caso, é add `y` ao acumulador `acc`. Essa função de ordem superior é executada para cada elemento na sequência durante o processo de redução.

A saída dessa instrução é uma única coluna (`sum_result`) que contém as somas cumulativas de números de um a cinco.

### O valor de funções de ordem superior {#value-of-higher-order-functions}

Esta seção analisa uma versão reduzida de uma instrução SQL de três gramas para entender melhor o valor de funções de ordem superior no Data Distiller para criar n-gramas com mais eficiência.

A declaração a seguir opera no `ProductName` dentro do `featurevector1` tabela. Ele produz um conjunto de substrings de três caracteres derivadas dos nomes de produtos modificados na tabela, usando posições obtidas da sequência gerada.

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

Veja a seguir uma análise da instrução SQL:

- Linha 2: `transform` aplica uma função de ordem superior a cada inteiro na sequência.
- Linha 3: `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)` gera uma sequência de inteiros de `1` ao comprimento do nome do produto modificado menos dois.
   - `length(lower(replace(ProductName, ' ', '')))` calcula o comprimento da variável `ProductName` depois de colocar em minúsculas e remover espaços.
   - `- 2` subtrai dois do comprimento para garantir que a sequência gere posições iniciais válidas para substrings de 3 caracteres. Subtrair 2 garante que você tenha caracteres suficientes após cada posição inicial para extrair uma substring de 3 caracteres. A função de subsequência de caracteres aqui funciona como um operador de lookahead.
- Linha 4: `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)` é uma função de ordem superior que opera em cada inteiro `i` na sequência gerada.
   - A variável `substring(...)` A função extrai uma subsequência de 3 caracteres da `ProductName` coluna.
   - Antes de extrair a substring, `lower(replace(ProductName, ' ', ''))` converte o `ProductName` para minúsculas e remove espaços para garantir a consistência.

A saída é uma lista de substrings de três caracteres de comprimento, extraídas dos nomes de produtos modificados, com base nas posições especificadas na sequência.

## Filtrar os resultados {#filter-results}

A variável `filter` função, com subsequente [transformações de dados](#data-transformation), permite uma extração mais refinada e precisa de informações relevantes de dados de texto. Isso permite obter insights, melhorar a qualidade dos dados e facilitar melhores processos de tomada de decisão.

A variável `filter` A função na instrução SQL a seguir serve para refinar e limitar a sequência de posições dentro da string da qual as substrings são extraídas usando a função de transformação subsequente.

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

A variável `filter` gera uma sequência de posições iniciais válidas dentro do grupo `ProductName` e extrai substrings de um comprimento específico. Somente as posições iniciais que permitem a extração de uma subsequência de sete caracteres são permitidas.

A condição `i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))` garante que a posição inicial `i` mais `6` (o comprimento da substring de sete caracteres desejada menos um) não excede o comprimento da substring modificada `ProductName`.

A variável `CASE` é usada para incluir ou excluir condicionalmente substrings com base em seu comprimento. Somente substrings de sete caracteres são incluídas; outras são substituídas por NULL. Essas subsequências de caracteres são usadas pelo `transform` para criar uma sequência de subsequências de caracteres da `ProductName` na `featurevector1` tabela.

>[!TIP]
>
>Você pode usar o [modelos com parâmetros](../ui/parameterized-queries.md) recurso para reutilizar e abstrair a lógica nas consultas. Por exemplo, ao criar funções de utilitário de uso geral (como a exibida acima para cadeias de caracteres de tokenização), você pode usar modelos parametrizados do Data Distiller em que o número de caracteres seria um parâmetro.

## Calcular a junção cruzada de elementos únicos em dois vetores de recursos {#cross-join-unique-elements}

Identificar as diferenças ou discrepâncias entre os dois conjuntos de dados com base em uma transformação específica dos dados é um processo comum para manter a precisão dos dados, melhorar a qualidade dos dados e garantir a consistência entre os conjuntos de dados.

Esta instrução SQL abaixo extrai os nomes de produtos exclusivos presentes em `featurevector2` mas não em `featurevector1` após aplicar as transformações.

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>Além de `EXCEPT`, você também pode usar `UNION` e `INTERSECT` dependendo do seu caso de uso. Além disso, você pode experimentar com `ALL` ou `DISTINCT` cláusulas para ver a diferença entre incluir todos os valores e retornar apenas os valores únicos para as colunas especificadas.

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

|   | lower(replace(ProductName, &#39; &#39;, &#39;&#39;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

Em seguida, execute uma junção cruzada para combinar elementos dos dois vetores de recursos para criar pares de elementos para comparação. A primeira etapa desse processo é criar um vetor tokenizado.

Um vetor tokenizado é uma representação estruturada de dados de texto em que cada palavra, frase ou unidade de significado (token) é convertida em um formato numérico. Essa conversão permite que algoritmos de processamento de linguagem natural entendam e analisem informações textuais.

O SQL abaixo cria um vetor tokenizado.

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>Se você estiver usando [!DNL DbVisualizer], após criar ou excluir uma tabela, atualize a conexão de banco de dados para que o cache de metadados da tabela seja atualizado. O Data Distiller não envia atualizações de metadados.

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

|   | featurevetor1_distinct | tokens |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 3 | iwatch | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} |
| 4 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Em seguida, repita o processo para `featurevector2`:

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

|   | featurevetor2_distinct | tokens |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Com ambos os vetores tokenizados concluídos, agora é possível criar a associação cruzada. Isso é visto no SQL abaixo:

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

Veja a seguir um resumo do SQl usado para criar a junção cruzada:

- Linha 2: `A.featurevector1_distinct AS SetA_ProductNames` seleciona o `featurevector1_distinct` coluna da tabela `A` e atribui a ele um alias `SetA_ProductNames`. Esta seção do SQL resulta em uma lista de nomes de produtos distintos do primeiro conjunto de dados.
- Linha 4: `A.tokens AS SetA_tokens1` seleciona o `tokens` coluna da tabela ou subconsulta `A` e atribui a ele um alias `SetA_tokens1`. Esta seção do SQL resulta em uma lista de valores tokenizados associados aos nomes de produtos do primeiro conjunto de dados.
- Linha 8: a `CROSS JOIN` A operação combina todas as combinações possíveis de linhas dos dois conjuntos de dados. Em outras palavras, ele emparelha cada nome de produto e seus tokens associados da primeira tabela (`A`) com cada nome de produto e seus tokens associados da segunda tabela (`B`). Isso resulta em um produto Cartesiano dos dois conjuntos de dados, em que cada linha na saída representa uma combinação de um nome de produto e seus tokens associados de ambos os conjuntos de dados.

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## Calcular a medida de similaridade de Jaccard {#compute-the-jaccard-similarity-measure}

Em seguida, calcule usar o coeficiente de similaridade de Jaccard para executar uma análise de similaridade entre os dois conjuntos de nomes de produtos comparando suas representações tokenizadas. A saída do script SQL abaixo fornece o seguinte: nomes de produtos de ambos os conjuntos, suas representações tokenizadas, contagens de tokens únicos comuns e totais e o coeficiente de similaridade de Jaccard calculado para cada par de conjuntos de dados.


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

Veja a seguir um resumo do SQL usado para calcular o coeficiente de similaridade de Jaccard:

- Linha 6: `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count` calcula o número de tokens comuns a ambos `SetA_tokens1` e `SetB_tokens2`. Esse cálculo é feito calculando o tamanho da interseção das duas matrizes de tokens.
- Linha 7: `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count` calcula o número total de tokens únicos em ambos `SetA_tokens1` e `SetB_tokens2`. Essa linha calcula o tamanho da união das duas matrizes de tokens.
- Linha 8-10: `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity` calcula a similaridade de Jaccard entre os conjuntos de tokens. Essas linhas dividem o tamanho da interseção do token pelo tamanho da união de tokens e arredondam o resultado para duas casas decimais. O resultado é um valor entre zero e um, onde um indica total similaridade.

Os resultados são mostrados na tabela abaixo:

+++Selecione para expandir

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Semelhança de Jaccard |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 7 | 0,43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 16 | 0.0 |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 11 | 0,09 |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 3 | 1.0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 12 | 0.0 |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 7 | 0,14 |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 0 | 8 | 0.0 |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0.0 |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 0 | 10 | 0.0 |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 1 | 7 | 0,14 |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0.0 |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 5 | 5 | 1.0 |

{style="table-layout:auto"}

+++

## Filtrar resultados com base no limite de Similaridade de Jacard {#similarity-threshold-filter}

Por fim, filtre os resultados com base em um limite predefinido para selecionar apenas os pares que atendem aos critérios de similaridade. A instrução SQL abaixo filtra os produtos com um coeficiente de similaridade de Jaccard de pelo menos 0,4. Isso estreita os resultados para pares que exibem um grau substancial de similaridade.

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

Os resultados desta consulta fornecem as colunas para a junção de similaridade, conforme visto abaixo:

+++Selecione para expandir

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iphone | iphone |

{style="table-layout:auto"}

+++:

### Próximas etapas {#next-steps}

Ao ler este documento, agora é possível usar essa lógica para realçar relações significativas ou sobreposições entre conjuntos de dados diferentes. A capacidade de identificar produtos de diferentes conjuntos de dados que têm uma semelhança significativa em suas características ou atributos tem várias aplicações reais. Essa lógica pode ser usada para cenários como:

- Correspondência de produto: para agrupar ou recomendar produtos semelhantes aos clientes.
- Limpeza de dados: para melhorar a qualidade dos dados.
- Análise da cesta de compras: para fornecer informações sobre o comportamento do cliente, preferências e possíveis oportunidades de venda cruzada.

Se ainda não tiver feito isso, leia as [Visão geral do pipeline de recursos de IA/ML](../data-distiller/ml-feature-pipelines/overview.md). Use essa visão geral para saber como o Data Distiller e seu aprendizado de máquina preferido podem criar modelos de dados personalizados que apoiam seus casos de uso de marketing com dados de Experience Platform.
