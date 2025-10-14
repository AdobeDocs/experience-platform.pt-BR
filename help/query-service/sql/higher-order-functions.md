---
title: Gerenciar tipos de dados de matriz e mapa com funções de ordem superior
description: Saiba como gerenciar tipos de dados de matriz e mapa com funções de ordem superior no Serviço de consulta. Os exemplos são fornecidos com casos de uso comuns.
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: d2bc580ba1cacdfab45bdc6356c630a63e7d0f6e
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Gerenciar tipos de dados de matriz e mapa com funções de ordem superior

Use este guia para saber como as funções de ordem superior podem processar tipos de dados complexos, como matrizes e mapas. Essas funções eliminam a necessidade de explodir a matriz, executam uma função e combinam o resultado. Funções de ordem superior são particularmente úteis para analisar ou processar conjuntos de dados e análises de séries temporais, que geralmente apresentam estruturas aninhadas complexas, arrays, mapas e casos de uso diversos.

A lista de casos de uso a seguir contém exemplos de funções de matriz e de manipulação de mapa de ordem superior.

## Usar transformação para ajustar o preço total por n {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

O trecho acima aplica uma função a cada elemento da matriz e retorna uma nova matriz de elementos transformados. Especificamente, a função `transform` pega uma matriz do tipo T e converte cada elemento do tipo T para o tipo U. Em seguida, retorna uma matriz de tipo U. Os tipos reais T e U dependem do uso específico da função de transformação.

`transform(array<T>, function<T, Int, U>): array<U>`

Esta função de transformação de matriz é semelhante ao exemplo anterior, mas há dois argumentos para a função. O segundo argumento nessa função também recebe o índice do elemento na matriz, além de ser transformado.

**Exemplo**

O exemplo de SQL abaixo demonstra esse caso de uso. A consulta recupera um conjunto limitado de linhas da tabela especificada, transformando a matriz `productListItems` multiplicando o atributo `priceTotal` de cada item por 73. O resultado inclui as colunas `_id`, `productListItems` e as colunas `price_in_inr` transformadas. A seleção é baseada em um intervalo específico de carimbo de data e hora.

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
 productListItems | price_in_inr
-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## Existe uso para descobrir se um produto com um SKU específico existe {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

No trecho acima, a função `exists` é aplicada a cada elemento da matriz e retorna um valor booleano. O booleano indica se há um ou mais elementos na matriz que satisfazem uma condição especificada. Nesse caso, confirma se um produto com uma SKU específica existe.

**Exemplo**

No exemplo SQL abaixo, a consulta busca `productListItems` da tabela `geometrixxx_999_xdm_pqs_1batch_10k_rows` e avalia se existe um elemento com uma SKU igual a `123679` na matriz `productListItems`. Em seguida, ele filtra os resultados com base em um intervalo específico de carimbos de data e hora e limita os resultados finais a dez linhas.

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
productListItems
-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## Use o filtro para localizar produtos nos quais o SKU > 100000 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

Essa função filtra uma matriz de elementos com base em uma determinada condição que avalia cada elemento como um valor booleano. Em seguida, ele retorna uma nova matriz que inclui apenas elementos em que a condição retornou um valor verdadeiro.

**Exemplo**

A consulta abaixo seleciona a coluna `productListItems`, aplica um filtro para incluir apenas elementos com SKU maior que 100000 e restringe o conjunto de resultados a linhas em um intervalo de carimbo de data/hora específico. A matriz filtrada recebe o alias como `_filter` na saída.

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
productListItems | _filter
-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## Use a agregação para somar os SKUs de todos os itens da lista de produtos associados a uma ID específica e dobrar o total resultante {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

Essa operação de agregação aplica um operador binário a um estado inicial e a todos os elementos na matriz. Também reduz vários valores a um único estado. Após essa redução, o estado final é convertido no resultado final usando uma função finish. A função finish toma o último estado obtido após aplicar o operador binário a todos os elementos de matriz e faz algo com ele para produzir o resultado final.

**Exemplo**

Este exemplo de consulta calcula o valor máximo de SKU da matriz `productListItems` dentro do intervalo de carimbo de data/hora especificado e dobra o resultado. A saída inclui a matriz `productListItems` original e o `max_value` calculado.

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
productListItems | max_value
-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## Use zip_with para atribuir um número de sequência a todos os itens na lista de produtos {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

Este fragmento combina os elementos de dois arrays em um único array novo. A operação é executada de forma independente em cada elemento da matriz e gera pares de valores. Se uma matriz for mais curta, valores nulos serão adicionados para corresponder ao comprimento da matriz mais longa. Isso acontece antes da função ser aplicada.

**Exemplo**

A consulta a seguir usa a função `zip_with` para criar pares de valores de duas matrizes. Ele faz isso adicionando os valores de SKU da matriz `productListItems` a uma sequência inteira, que foi gerada usando a função `Sequence`. O resultado é selecionado junto com a coluna original `productListItems` e é limitado com base em um intervalo de carimbo de data/hora.

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
productListItems     | zip_with
---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## Use map_from_entries para atribuir um número de sequência a cada item na lista de produtos e obter o resultado final como um mapa {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

Este trecho converte uma matriz de pares de valores-chave em um mapa. É útil ao lidar com dados de par de valor-chave que poderiam se beneficiar de uma estrutura mais organizada e eficiente.

**Exemplo**

A consulta a seguir cria pares de valores de uma sequência e a matriz productListItems converte esses pares em um mapa usando map_from_entries e seleciona a coluna productListItems original junto com a coluna map_from_entries recém-criada. O resultado é filtrado e limitado com base no intervalo de carimbo de data e hora especificado.

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Use map_form_arrays para atribuir números de sequência a itens na lista de produtos e retornar o resultado como um mapa {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

A função `map_form_arrays` cria um mapa usando valores emparelhados de duas matrizes.

>[!IMPORTANT]
>
>Não deve haver elementos nulos nas chaves.

**Exemplo**

O SQL abaixo cria um mapa em que as chaves são números sequenciados gerados usando a função `Sequence`, e os valores são elementos da matriz `productListItems`. A consulta seleciona a coluna `productListItems` e usa a função `Map_from_arrays` para criar o mapa com base na sequência gerada de números e os elementos da matriz. O resultado é limitado a dez linhas e filtrado com base em um intervalo de carimbo de data e hora.

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Use map_concat para concatenar dois mapas em como mapa único {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

A função `map_concat` no trecho acima pega vários mapas como argumentos e retorna um novo mapa que combina todos os pares de valores chave dos mapas de entrada. A função concatena vários mapas em um único mapa, e o mapa resultante inclui todos os pares de valores-chave dos mapas de entrada.

**Exemplo**

O SQL abaixo cria um mapa em que cada item em `productListItems` é associado a um número de sequência, que é então concatenado com outro mapa em que as chaves são geradas em um intervalo de sequência específico.

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Use element_at para recuperar um valor correspondente a &#39;AAID&#39; no mapa de identidade para cálculo adicional {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

Para matrizes, o trecho retorna o elemento em um índice especificado (com base em 1) ou o valor associado a uma chave em um mapa. Se o índice for &lt; 0, ele acessará os elementos do último ao primeiro e retornará null se o índice exceder o comprimento da matriz.

Para mapas, ele retorna um valor para a chave fornecida ou nulo se a chave não estiver contida no mapa.

**Exemplo**

A consulta seleciona a coluna `identitymap` da tabela `geometrixxx_999_xdm_pqs_1batch_10k_rows` e extrai o valor associado à chave `AAID` para cada linha. Os resultados são restritos a linhas que estão dentro do intervalo de carimbo de data e hora especificado, e a consulta limita a saída a dez linhas.

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## Usar cardinalidade para localizar o número de identidades no mapa de identidades {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

Este trecho retorna o tamanho de uma determinada matriz ou mapa e fornece um alias. Ele retorna -1 se o valor for nulo.

**Exemplo**

A consulta abaixo recupera a coluna `identitymap`, e a função `Cardinality` calcula o número de elementos em cada mapa dentro de `identitymap`. Os resultados são limitados a dez linhas e filtrados com base em um intervalo de carimbo de data e hora especificado.

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
                                                                  identitymap                                            |  size(identitymap) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## Use array_distinct para localizar os elementos distintos em productListItems {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

O trecho acima remove valores duplicados da matriz especificada.

**Exemplo**

A consulta abaixo seleciona a coluna `productListItems`, remove os itens duplicados das matrizes e limita a saída a dez linhas com base em um intervalo de carimbo de data/hora especificado.

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Resultado**

Os resultados para esse SQL seriam semelhantes aos vistos abaixo.

```console
productListItems     | array_distinct(productListItems)
---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### Funções adicionais de ordem superior {#additional-higher-order-functions}

Os seguintes exemplos de funções de ordem superior são explicados como parte do caso de uso recuperar registros semelhantes. Um exemplo e uma explicação do uso de cada função são fornecidos na respectiva seção desse documento.

O exemplo de função [`transform` &#x200B;](../use-cases/retrieve-similar-records.md#length-adjustment) abrange a geração de tokens de uma lista de produtos.

O exemplo de função [`filter` &#x200B;](../use-cases/retrieve-similar-records.md#filter-results) demonstra uma extração mais refinada e precisa de informações relevantes de dados de texto.

A função [`reduce` &#x200B;](../use-cases/retrieve-similar-records.md#higher-order-function-solutions) fornece uma maneira de derivar valores cumulativos ou agregações, que podem ser fundamentais em vários processos analíticos e de planejamento.
