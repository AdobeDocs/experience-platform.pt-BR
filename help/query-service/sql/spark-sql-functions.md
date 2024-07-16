---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;spark sql;Spark sql;spark;funções spark sql;funções;
solution: Experience Platform
title: Funções Spark SQL no Serviço de consulta
description: Saiba mais sobre as funções Spark SQL compatíveis que estendem a funcionalidade SQL.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: 7ac1521adb916313c8b53fe2a095821d756480be
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 1%

---

# [!DNL Spark] funções SQL

Você pode usar várias funções Spark SQL incorporadas para estender a funcionalidade SQL com o Serviço de consulta da Adobe Experience Platform. Este documento lista as funções do Spark SQL compatíveis com o Serviço de consulta.

Para obter informações mais detalhadas sobre as funções, incluindo sintaxe, uso e exemplos, leia a [documentação da função Spark SQL](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>Nem todas as funções na documentação externa são compatíveis.

## Operadores e funções matemáticos e estatísticos {#math}

| Operador/Função | Descrição |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | Retorna o restante dos dois números |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Multiplica os dois números |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Adiciona os dois números |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Subtrai os dois números |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Divide os dois números |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Retorna o valor absoluto da entrada |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Retorna o valor inverso do cosseno |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Retorna a cardinalidade estimada por HyperLogLog++ |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Retorna o valor do percentil aproximado na porcentagem especificada |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Retorna o valor do seno inverso |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Retorna o valor da tangente inversa |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Retorna o ângulo entre o plano positivo do eixo x e os pontos fornecidos pelas coordenadas |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Retorna o valor médio |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Retorna a raiz do cubo |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) ou [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Retorna o menor inteiro não maior que o valor inserido |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Converter de uma base para outra |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Retorna o coeficiente Pearson entre os números |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Retorna o valor do cosseno |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Retorna o valor do cosseno hiperbólico |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Retorna o valor cotangente |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Retorna a classificação de um valor em um grupo de valores |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Retorna o número de Euler |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Retorna e à potência do valor |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Retorna e à potência do valor menos 1 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Retorna o fatorial do valor |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Retorna o maior inteiro não menor que o valor |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Retorna o maior valor de todos os parâmetros |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Retorna a hipotenusa dos dois valores fornecidos |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Retorna o valor de curtose do grupo |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Retorna o menor valor de todos os parâmetros |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Retorna o logaritmo natural do valor |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Retorna o logaritmo do valor |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Retorna o logaritmo do valor na base 10 |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Retorna o logaritmo do valor mais 1 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Retorna o logaritmo do valor na base 2 |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Retorna o valor máximo da expressão |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Retorna a média calculada dos valores |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Retorna o valor mínimo da expressão |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Retorna IDs monotonicamente crescentes |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Retorna o valor negado |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Retorna a classificação de porcentagem de um valor |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Retorna o percentil exato em uma determinada porcentagem |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Retorna o percentil aproximado em uma determinada porcentagem |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Retorna pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Retorna o módulo positivo entre dois valores |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Retorna o valor positivo |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Retorna o primeiro valor à potência do segundo valor |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Converte o valor em radianos |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Retorna um número aleatório de 0 a 1 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Retorna um valor aleatório |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Retorna o valor duplo mais próximo |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Retorna o valor arredondado mais próximo |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Retorna o sinal do número |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Retorna o seno do valor |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Retorna o seno hiperbólico do valor |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Retorna a raiz quadrada do valor |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Retorna o desvio padrão do valor |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Retorna o desvio padrão da população do valor |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Retorna o desvio padrão de exemplo do valor |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Retorna a soma dos valores |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Retorna a tangente do valor |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Retorna a tangente hiperbólica do valor |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Retorna a variação de população calculada |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Retorna a variação da amostra calculada |

### Operadores e funções lógicos {#logical-operators}

| Operador/Função | Descrição |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) ou [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | Not lógico |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Menor que |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | Menor que ou igual a |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Igual a |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Maior que |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Maior que ou igual a |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Exclusivo ou bit a bit |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | Ou bit a bit |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | Não em nível de bits |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Retorna os elementos comuns |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Afirma se a expressão é verdadeira |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Se a expressão for avaliada como verdadeira, retorna a segunda expressão. Caso contrário, retorne a terceira expressão. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Se a expressão for nula, ela retornará a segunda expressão. Caso contrário, retornará a primeira expressão. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Retorna verdadeiro se a primeira expressão estiver em qualquer uma das expressões subsequentes. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Retorna verdadeiro se o valor não for um número |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Retorna verdadeiro se o valor não for nulo |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Retorna verdadeiro se o valor for nulo |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Retorna a primeira expressão se não for um número; caso contrário, retorna a segunda expressão |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Ou lógico |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | Quando o pode ser usado para criar condições de ramificação para comparação |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Retorna verdadeiro se a expressão XPath for avaliada como verdadeira ou se um nó correspondente for encontrado |

### Funções de data/hora {#datetime-functions}

| Função | Descrição |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Adicionar meses à data |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Adicionar dias à data |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Modificar formato de data |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Subtrair dias da data |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Retorna a data truncada na unidade especificada |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Retorna a diferença entre datas em dias |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day), [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Retorna o dia do mês |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Retorna o dia da semana (1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Retorna o dia do ano |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Retorna a data no horário UNIX® |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Retorna a data UTC |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Retorna a hora da entrada |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Retorna o último dia do mês ao qual a data pertence |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Retorna o minuto da entrada |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Retorna o mês da entrada |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Número de meses entre |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Retorna o primeiro dia após a entrada |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Retorna o trimestre da entrada |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Retorna o segundo da cadeira de caracteres |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Converte a cadeia de caracteres em uma data. **Observação:** a cadeia de caracteres **deve** estar no formato `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Converte a cadeia de caracteres em um carimbo de data e hora. **Observação:** a cadeia de caracteres **deve** estar no formato `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Converte a string em um carimbo de data e hora UNIX® |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Converte a cadeia de caracteres em um carimbo de data e hora UTC |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Trunca a data |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Retorna o carimbo de data e hora UNIX® |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Dia da semana (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Retorna a semana do ano de uma determinada data |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Retorna o ano da cadeira de caracteres |

### Matrizes {#arrays}

| Função | Descrição |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Cria uma matriz com os elementos fornecidos |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Verifica se a matriz contém o valor |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Remove valores duplicados da matriz |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Retorna uma matriz dos elementos na primeira matriz, mas não na segunda |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Retorna a interseção das duas matrizes |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Une dois arrays |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Retorna o valor máximo da matriz |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Retorna o valor mínimo da matriz |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Retorna a posição do elemento com base em 1 |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Remove todos os elementos iguais ao elemento |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Cria uma matriz contendo o valor contado vezes |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Classifica a matriz |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Une o array sem duplicatas |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Combina os valores de matrizes fornecidas com os valores da coleção original em um determinado índice |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Retorna o tamanho da matriz |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Retornar o elemento na posição |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Separar elementos da matriz em várias linhas, excluindo nulos |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Separar elementos da matriz em várias linhas, incluindo nulo |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Retorna a posição de base 1 da matriz |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Nivela um conjunto de arrays |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Separar a matriz de structs em uma tabela, excluindo null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Separar a matriz de structs em uma tabela, incluindo null |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | Separar elementos de uma matriz em várias linhas com posições, excluindo valores nulos |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Inverter elementos da matriz |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Retorna uma permutação aleatória da matriz |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Subconjuntos de uma matriz |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Classificar uma matriz, dada uma ordem |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Mescla as duas matrizes em uma única matriz antes de aplicar uma função |

### Funções de conversão do tipo de dados {#datatype-casting}

| Função | Descrição |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Alterar o tipo de dados para bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Alterar o tipo de dados para binário |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Alterar o tipo de dados para booleano |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Alterar o tipo de dados para o tipo especificado |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Alterar o tipo de dados para data |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Alterar o tipo de dados para decimal |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Alterar o tipo de dados para duplo |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Alterar o tipo de dados para flutuante |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Alterar o tipo de dados para int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Alterar o tipo de dados para smallint |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Criar um mapa a partir de uma cadeia de caracteres |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Alterar o tipo de dados para cadeia de caracteres |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Criar uma estrutura |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Alterar o tipo de dados para tinyint |

### Funções de conversão e formatação {#conversion}

| Função | Descrição |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Retorna o valor numérico (ASCII) |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Altere o argumento para uma string base64 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Alterar o argumento para um valor binário |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Retornar o comprimento de bits |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | Retorna o caractere ASCII |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Retorna o tamanho da string |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Retorna o valor de verificação de redundância cíclica |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Converter radianos em graus |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Alterar o formato do número |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Obter dados do JSON |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Retornar o valor de hash |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Converter o argumento em um valor hexadecimal |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Altera a string para letras maiúsculas e minúsculas |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Altera a cadeia de caracteres para ficar totalmente em minúsculas |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Preenche o lado esquerdo de uma cadeira de caracteres |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Criar um mapa |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Criar um mapa a partir de uma matriz |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Criar um mapa a partir de uma matriz de estruturas |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | Retornar o valor md5 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Preenche o lado direito de uma cadeira de caracteres |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Remove espaços à direita |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | Retornar o valor SHA1 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | Retornar o valor SHA2 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Retornar o código soundex |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Separar valores em linhas |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Retornar a subcadeia de caracteres |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Retorna uma string JSON |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Substituir valores na cadeia de caracteres |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Remover caracteres à esquerda e à direita |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Alterar a cadeia de caracteres para ficar totalmente em maiúsculas |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Converter a sequência de caracteres base64 em binária |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Converter o hexadecimal em binário |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | Retornar uma UUID |

### Avaliação de dados {#data-evaluation}

| Função | Descrição |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Retorna o primeiro argumento não nulo |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Retornar uma lista de elementos não exclusivos |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Retorna um conjunto de elementos únicos |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Concatenação |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Concatenação com separador |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Retorna a contagem total de linhas |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Decodificar usando um conjunto de caracteres |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Retornar a [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)ª entrada |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Codificar usando um conjunto de caracteres |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Retorna o primeiro valor |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Indica se uma coluna está agrupada |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Retorna o nível de agrupamento |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Retorna um índice de ocorrência de caracteres com base em 1 |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Retorna uma tupla de uma entrada JSON |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Retorna o valor antes do deslocamento |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Retorna o último valor |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Retorna os primeiros [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) caracteres |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Retorna o comprimento da cadeira de caracteres |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Retorna a distância de Levenshtein entre as cadeias de caracteres |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Retorna a posição da primeira ocorrência de uma substring |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Concatenar um mapa |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Retornar as chaves de um mapa |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Retornar os valores de um mapa |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Dividir linhas em partições |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Retorna nulo se verdadeiro |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Retorna o valor se for nulo |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Retorna o valor se não for nulo |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Extrai parte de um URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Calcula a classificação de um valor |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extrai algo que corresponde ao regex |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Substitui algo que corresponde ao regex |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Retorna uma string que se repete |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Substituir todas as instâncias de uma cadeia de caracteres |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Criar um rollup multidimensional |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Atribui um número de linha exclusivo |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Retorna o esquema do JSON |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Divide a string em uma matriz de palavras |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Gera uma matriz de elementos |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Deslocamento bit a bit assinado para a esquerda |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Deslocamento bit a bit assinado para a direita |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Deslocamento bit a bit sem sinal para a direita |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Retorna o tamanho da matriz |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Retornar uma cadeia de caracteres com [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) espaços |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Dividir string |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Índice de retorno da substring |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Janela |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | Analisar nós XML |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | Analisar nós XML para duplo |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | Analisar nós XML para flutuação |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | Analisar nós XML para inteiro |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Analisar nós XML por muito tempo |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | Analisar nós XML para inteiro curto |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | Analisar nós XML para cadeia de caracteres |

### Informações atuais {#current-information}

| Função | Descrição |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Retorna o banco de dados atual |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Retorna a data atual |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Retorna o carimbo de data e hora atual |

### Funções de ordem superior {#higher-order}

| Função | Descrição |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Transformar elementos em uma matriz |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Verificar se o elemento existe |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtrar a matriz de entrada |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Aplicar um operador binário a todos os elementos |
