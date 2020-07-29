---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funções SQL Spark
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a98e31f57c6ff4fc49d8d8f64441a6e1e18d89da
workflow-type: tm+mt
source-wordcount: '4900'
ht-degree: 5%

---


# [!DNL Spark] Funções SQL

Os [!DNL Spark] auxiliares SQL fornecem funções [!DNL Spark] SQL incorporadas para estender a funcionalidade SQL.

Referência: [Documentação da função SQL Spark](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE]
>
>Nem todas as funções na documentação externa são suportadas.

## Categorias

- [Operadores e funções de matemática e estatística](#math-and-statistical-operators-and-functions)
- [Operadores lógicos](#logical-operators)
- [Funções de data/hora](#date/time-functions)
- [funções de Agregação](#aggregate-functions)
- [Matrizes](#arrays)
- [Funções de difusão de tipo de dados](#datatype-casting-functions)
- [Funções de conversão e formatação](#conversion-and-formatting-functions)
- [Avaliação dos dados](#data-evaluation)
- [Informações atuais](#current-information)

### Operadores e funções de matemática e estatística

#### Módulo

`expr1 % expr2`: Retorna o restante após `expr1`/`expr2`.

Exemplos:

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Multiplicar

`expr1 * expr2`: Devoluções `expr1`*`expr2`.

Exemplo:

```
> SELECT 2 * 3;
 6
```

#### Add

`expr1 + expr2`: Devoluções `expr1`+`expr2`.

Exemplo:

```
> SELECT 1 + 2;
 3
```

#### Subtrair

`expr1 - expr2`: Devoluções `expr1`-`expr2`.

Exemplo:

```
> SELECT 2 - 1;
 1
```

#### Dividir

`expr1 / expr2`: Devoluções `expr1`/`expr2`. Ele sempre faz divisão de ponto flutuante.

Exemplos:

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`: Retorna o valor absoluto do valor numérico.

Exemplo:

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`: Retorna o cosseno inverso (também conhecido como cosseno de arco) de `expr`, como se fosse calculado por `java.lang.Math.acos`.

Exemplos:

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### aprox_percentile

`approx_percentile(col, percentage [, accuracy])`: Retorna o valor aproximado do percentil da coluna numérica `col` na porcentagem especificada. O valor da porcentagem deve estar entre 0,0 e 1,0. O `accuracy` parâmetro (padrão: 10000) é um literal numérico positivo que controla a precisão da aproximação ao custo da memória. O valor mais alto de `accuracy` produz melhor precisão `1.0/accuracy` é o erro relativo da aproximação. Quando `percentage` é uma matriz, cada valor da matriz de porcentagem deve estar entre 0,0 e 1,0. Nesse caso, a matriz de percentil aproximada da coluna `col` na determinada matriz de porcentagem é retornada.

Exemplos:

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asina

`asin(expr)`: Retorna o seno inverso (também conhecido como seno arco), o seno arco de `expr`, como se fosse calculado por `java.lang.Math.asin`.

Exemplos:

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atã

`atan(expr)`: Retorna a tangente inversa (também conhecida como tangente de arco) de `expr`como se fosse calculada por `java.lang.Math.atan`

Exemplo:

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`: Retorna o ângulo, em radianos, entre o eixo x positivo de um plano e o ponto dado pelas coordenadas (`exprX`, `exprY`), como se fosse calculado por `java.lang.Math.atan2`.

Argumentos:

`exprY`: Coordenar no eixo`exprX`y: Coordenar no eixo x

Exemplo:

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`: Retorna a média calculada a partir dos valores de um grupo.

#### cardinalidade

`cardinality(expr)`: Retorna o tamanho de uma matriz ou mapa. A função retornará -1 se sua entrada for nula e `spark.sql.legacy.sizeOfNull` estiver definida como true (padrão). Se `spark.sql.legacy.sizeOfNull` for definida como false, a função retornará null para entrada nula.

Exemplos:

```
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`: Retorna a raiz do cubo de `expr`.

Exemplo:

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`: Retorna o menor número inteiro não menor que `expr`.

Exemplos:

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### teto

`ceiling(expr)`: Retorna o menor número inteiro não menor que `expr`.

Exemplos:

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### ct

`conv(num, from_base, to_base)`: Converter `num` de `from_base` para `to_base`

Exemplos:

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)`: Retorna o coeficiente de correlação Pearson entre um conjunto de pares de números.

#### cos

`cos(expr)`: Retorna o cosseno de `expr`, como se fosse calculado por `java.lang.Math.cos`.

Exemplo:

```
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`: Retorna o cosseno hiperbólico de `expr`, como se fosse calculado por `java.lang.Math.cosh`.

Argumentos:
- `expr`: Ângulo hiperbólico

Exemplo:

```
> SELECT cosh(0);
 1.0
```

#### berço

`cot(expr)`: Retorna o contêiner de `expr`, como se fosse calculado por `1/java.lang.Math.cot`.

Argumentos:
- `expr`: Ângulo em radianos

Exemplo:

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`: Calcula a classificação de um valor em um grupo de valores. O resultado é um mais o valor de classificação atribuído anteriormente. Diferentemente da função `rank`, `dense_rank` não produz lacunas na sequência de classificação.

#### e

`e()`: Retorna o número de Euler, e.

Exemplo:

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`: Retorna-me à potência de `expr`.

Exemplo:

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`: Retorna exp(`expr`) - 1.

Exemplo:

```
> SELECT expm1(0);
 0.0
```

#### fatorial

`factorial(expr)`: Retorna o fatorial de `expr`. `expr` é [0.20]. Caso contrário, nulo.

Exemplo:

```
> SELECT factorial(5);
 120
```

#### chão

`floor(expr)`: Retorna o maior número inteiro não maior que `expr`.

Exemplos:

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### best

`greatest(expr, ...)`: Retorna o maior valor de todos os parâmetros, ignorando valores nulos.

Exemplo:

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hipótese

`hypot(expr1, expr2)`: Retorna sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>).

Exemplo:

```
> SELECT hypot(3, 4);
 5.0
```

#### curtose

`kurtosis(expr)`: Retorna o valor de kurtosis calculado a partir dos valores de um grupo.


#### less

`least(expr, ...)`: Retorna o menor valor de todos os parâmetros, ignorando valores nulos.

Exemplo:

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### levenshtein

`levenshtein(str1, str2)`: Retorna a distância Levenshtein entre as duas strings especificadas.

Exemplos:

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`: Retorna o logaritmo natural (base e) de `expr`.

Exemplo:

```
> SELECT ln(1);
 0.0
```

#### registro

`log(base, expr)`: Retorna o logaritmo de `expr` with `base`.

Exemplo:

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`: Retorna o logaritmo de `expr` com base 10.

Exemplo:

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: Devoluções `log(1 + expr)`.

Exemplo:

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`: Retorna o logaritmo de `expr` com base 2.

Exemplo:

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`: Retorna o valor máximo de `expr`.

#### média

`mean(expr)`: Retorna a média calculada a partir dos valores de um grupo.

#### min

`min(expr)`: Retorna o valor mínimo de `expr`.

#### monotonicamente_growth_id

`monotonically_increasing_id()`: Retorna números inteiros de 64 bits que aumentam monotonicamente. A ID gerada é garantida por aumentar monotonicamente e ser exclusiva, mas não consecutiva. A implementação atual coloca a ID da partição nos 31 bits superiores, e os 33 bits inferiores representam o número de registro dentro de cada partição. A suposição é que o quadro de dados tem menos de 1 bilhão de partições, e cada partição tem menos de 8 bilhões de registros. A função não é determinística porque seu resultado depende das IDs de partição.

#### negativo

`negative(expr)`: Retorna o valor negado de `expr`.

Exemplo:

```
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()`: Calcula a classificação percentual de um valor em um grupo de valores.

#### percentil

`percentile(col, percentage [, frequency])`: Retorna o valor exato do percentil da coluna numérica `col` na porcentagem especificada. O valor de `percentage` deve estar entre 0,0 e 1,0. O valor de `frequency` deve ser integral positivo.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`: Retorna a matriz exata de valores de percentil da coluna numérica `col` nas porcentagens especificadas. Cada valor da matriz de porcentagem deve estar entre 0,0 e 1,0. O valor de `frequency` deve ser integral positivo.

#### percentile_aprox

`percentile_approx(col, percentage [, accuracy])`: Retorna o valor aproximado do percentil da coluna numérica `col` na porcentagem especificada. O valor de `percentage` deve estar entre 0,0 e 1,0. O `accuracy` parâmetro (padrão: 10000) é um literal numérico positivo que controla a precisão da aproximação ao custo da memória. O valor mais alto de `accuracy` produz melhor precisão `1.0/accuracy` é o erro relativo da aproximação. Quando `percentage` é uma matriz, cada valor da matriz de porcentagem deve estar entre 0,0 e 1,0. Nesse caso, retorna a matriz de percentil aproximada da coluna `col` na matriz de porcentagem especificada.

Exemplos:

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`: Retorna pi.

Exemplo:

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`: Retorna o valor positivo do `expr1` modo `expr2`.

Exemplos:

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positivo

`positive(expr)`: Retorna o valor positivo de `expr`

#### vara

`pow(expr1, expr2)`: Levanta `expr1` o poder do `expr2`.

Exemplo:

```
> SELECT pow(2, 3);
 8.0
```

#### potência

`power(expr1, expr2)`: Levanta `expr1` o poder do `expr2`.

Exemplos:

```
> SELECT power(2, 3);
 8.0
```

#### radianos

`radians(expr)`: Converte graus em radianos.

Argumentos:

- `expr`: Ângulo em graus

Exemplo:

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`: Retorna um valor aleatório com valores distribuídos de forma independente e idêntica (i.i.) uniformemente em (0, 1).

Exemplos:

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE]
>
>Esta função não é determinística em casos gerais.

#### randn

`randn([seed])`: Retorna um valor aleatório com valores independentes e distribuídos de forma idêntica (i.i.d.) extraídos da distribuição normal padrão.

Exemplos:

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE]
>
>Esta função não é determinística em casos gerais.

#### impressão

`rint(expr)`: Retorna o valor do duplo mais próximo no valor do argumento e igual a um número inteiro matemático.

Exemplos:

```
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`: Retorna `expr` arredondados para `d` casas decimais usando o modo de arredondamento HALF_UP.

Exemplo:

```
> SELECT round(2.5, 0);
 3.0
```

#### sign

`sign(expr)`: Retorna -1.0, 0.0 ou 1.0 como `expr` negativo, 0 ou positivo.

Exemplo:

```
> SELECT sign(40);
 1.0
```

#### signo

`signum(expr)`: Retorna -1.0, 0.0 ou 1.0 como `expr` negativo, 0 ou positivo.

Exemplo:

```
> SELECT signum(40);
 1.0
```

#### pecado

`sin(expr)`: Retorna o seno de `expr`, como se fosse calculado por `java.lang.Math.sin`.

Argumentos:

- `expr`: Ângulo em radianos

Exemplo:

```
> SELECT sin(0);
 0.0
```

#### sinho

`sinh(expr)`: Retorna seno hiperbólico de `expr`, como se fosse calculado por `java.lang.Math.sinh`.

Argumentos:

- `expr`: Ângulo hiperbólico

Exemplo:

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`: Retorna a raiz quadrada de `expr`.

Exemplo:

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`: Retorna o desvio padrão da amostra calculado a partir dos valores de um grupo.

#### stddev_pop

`sttdev_pop(expr)`: Retorna o desvio padrão da população calculado a partir dos valores de um grupo.

#### stddev_samp

`stddev_samp(expr)`: Retorna o desvio padrão da amostra calculado a partir dos valores de um grupo.

#### sum

`sum(expr)`: Retorna a soma calculada a partir dos valores de um grupo.

#### bronzeado

`tan(expr)`: Retorna a tangente de `expr`, como se fosse calculada por `java.lang.Math.tan`.

Argumentos:

- `expr`: Ângulo em radianos

Exemplo:

```
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`: Retorna a tangente hiperbólica de `expr`, como se fosse calculada por `java.lang.Math.tanh`.

Argumentos:

- `expr`: Ângulo hiperbólico

Exemplo:

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`: Retorna a variação de população calculada a partir dos valores de um grupo.

#### Var_samp

`var_samp(expr)`: Retorna a variação de amostra calculada a partir dos valores de um grupo.

#### variação

`variance(expr)`: Retorna a variação de amostra calculada a partir dos valores de um grupo.

### Operadores lógicos

#### Lógico não

`! expr`: Não é lógico.

#### Less than

`expr1 < expr2`: Retorna true se `expr1` for menor que `expr2`.

Argumentos:

- `expr1, expr2`: As duas expressões devem ser do mesmo tipo ou podem ser enviadas para um tipo comum e devem ser de um tipo que possa ser solicitado. Por exemplo, o tipo de mapa não pode ser solicitado, portanto não é suportado. Para tipos complexos, como array/struct, os tipos de dados de campos devem ser ordenáveis.

Exemplos:

```
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### Less than or equal to

`expr1 <= expr2`: Retorna true se `expr1` for menor que ou igual a `expr2`.

Argumentos:

- `expr1, expr2`: As duas expressões devem ser do mesmo tipo ou podem ser transmitidas para um tipo comum e devem ser do tipo que pode ser solicitado. Por exemplo, o tipo de mapa não pode ser solicitado, portanto não é suportado. Para tipos complexos, como array/struct, os tipos de dados de campos devem ser ordenáveis.

Exemplos:

```
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### Equal to

`expr1 = expr2`: Retorna true se `expr1` for igual `expr2`ou false se não for igual.

Argumentos:

- `expr1, expr2`: As duas expressões devem ser do mesmo tipo ou podem ser colocadas em um tipo comum e devem ser um tipo que possa ser usado na comparação de igualdade. O tipo de mapa não é suportado. Para tipos complexos, como array/struct, os tipos de dados de campos devem ser ordenáveis.

Exemplos:

```
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### Greater than

`expr1 > expr2`: Retorna true se `expr1` for maior que `expr2`.

Argumentos:

- `expr1, expr2`: As duas expressões devem ser do mesmo tipo ou podem ser enviadas para um tipo comum e devem ser de um tipo que possa ser solicitado. Por exemplo, o tipo de mapa não pode ser solicitado, portanto não é suportado. Para tipos complexos, como array/struct, os tipos de dados de campos devem ser ordenáveis.

Exemplos:

```
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### Greater than or equal to

`expr1 >= expr2`: Retorna true se `expr1` for maior ou igual a `expr2`.

Argumentos:

- `expr1, expr2`: As duas expressões devem ser do mesmo tipo ou podem ser enviadas para um tipo comum e devem ser de um tipo que possa ser solicitado. Por exemplo, o tipo de mapa não pode ser solicitado, portanto não é suportado. Para tipos complexos, como array/struct, os tipos de dados de campos devem ser ordenáveis.

Exemplos:

```
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### Exclusivo em nível de bits ou

`expr1 ^ expr2`: Retorna o resultado de OR exclusivo bit a bit de `expr1` e `expr2`.

Exemplo:

```
> SELECT 3 ^ 5;
 2
```

#### e

`expr1 and expr2`: AND lógico.

#### arrays_duplicate

`arrays_overlap(a1, a2)`: Retorna true se a1 contiver pelo menos um elemento não nulo presente também em a2. Se as matrizes não tiverem um elemento comum e não estiverem vazias e qualquer uma delas contiver um elemento nulo, null será retornado. Caso contrário, false será retornado.

Exemplo:

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Desde: 2.4.0

#### assert_true

`assert_true(expr)`: Emite uma exceção se não `expr` for verdadeira.

Exemplo:

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`: Se `expr1` for avaliado como true, retornará `expr2`; caso contrário, retorna `expr3`.

Exemplo:

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### nulo

`ifnull(expr1, expr2)`: Retorna `expr2` se `expr1` for nulo ou `expr1` diferente.

Exemplo:

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`: Retorna true se `expr` for igual a qualquer valN.

Argumentos:
- `expr1, expr2, expr3, ...`: Os argumentos devem ser do mesmo tipo.

Exemplos:

```
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)`: Retorna true se `expr` for NaN, ou false se não for.

Exemplo:

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`: Retorna true se não `expr` for nulo ou false se não for nulo.

Exemplos:

```
> SELECT isnotnull(1);
 true
```

#### nulo

`isnull(expr)`: Retorna true se `expr` for nulo, ou false se não for.

Exemplo:

```
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)`: Retorna `expr1` se não for NaN, ou `expr2` não.

Exemplo:

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`: Não é lógico.

#### ou

`expr1 or expr2`: Ou lógico.

#### xpath_boolean

`xpath_boolean(xml, xpath)`: Retorna true se a expressão XPath for avaliada como true ou se um nó correspondente for encontrado.

Exemplo:

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Funções de data/hora

#### add_months

`add_months(start_date, num_months)`: Retorna a data `num_months` posterior `start_date`.

Exemplo:

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Desde: 1.5.0

#### date_add

`date_add(start_date, num_days)`: Retorna a data `num_days` posterior `start_date`.

Exemplo:

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Desde: 1.5.0

#### date_format

`date_format(timestamp, fmt)`: Converte `timestamp` em um valor de string no formato especificado pelo formato de data `fmt`.

Exemplo:

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

Desde: 1.5.0

#### date_sub

`date_sub(start_date, num_days)`: Retorna a data anterior `num_days` ao `start_date`.

Exemplo:

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Desde: 1.5.0

#### date_trunc

`date_trunc(fmt, ts)`: Retorna os carimbos de data e hora truncados para a unidade especificada pelo modelo de formato `fmt`. `fmt` deve ser um de [&quot;ANO&quot;, &quot;AAAA&quot;, &quot;YY&quot;, &quot;MON&quot;, &quot;MÊS&quot;, &quot;MM&quot;, &quot;DIA&quot;, &quot;DD&quot;, &quot;HORA&quot;, &quot;MINUTO&quot;, &quot;SEGUNDO&quot;, &quot;SEMANA&quot;, &quot;TRIMESTRE&quot;]

Exemplos:

```
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

Desde: 2.3.0

#### datedificação

`datediff(endDate, startDate)`: Retorna o número de dias de `startDate` a `endDate`.

Exemplos:

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

Desde: 1.5.0

#### dia

`day(date)`: Retorna o dia do mês da data/carimbo de data e hora.

Exemplo:

```
> SELECT day('2009-07-30');
 30
```

Desde: 1.5.0

#### dia do mês

`dayofmonth(date)`: Retorna o dia do mês da data/carimbo de data e hora.

Exemplo:

```
> SELECT dayofmonth('2009-07-30');
 30
```

Desde: 1.5.0

#### dia da semana

`dayofweek(date)`: Retorna o dia da semana para data/carimbo de data e hora (1 = domingo, 2 = segunda, ..., 7 = sábado).

Exemplo:

```
> SELECT dayofweek('2009-07-30');
 5
```

Desde: 2.3.0

#### dia

`dayofyear(date)`: Retorna o dia do ano da data/carimbo de data e hora.

Exemplo:

```
> SELECT dayofyear('2016-04-09');
 100
```

Desde: 1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)`: Retorna `unix_time` no especificado `format`.

Exemplo:

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Desde: 1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`: Interpreta um carimbo de data e hora como &#39;2017-07-14 02:40:00.0&#39; como um horário em UTC, e renderiza esse horário como um carimbo de data e hora no fuso horário especificado. Por exemplo, &#39;GMT+1&#39; renderia &#39;2017-07-14 03:40:00.0&#39;.

Exemplo:

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Desde: 1.5.0

#### hora

`hour(timestamp)`: Retorna o componente de hora da string/timestamp.

Exemplo:

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

Desde: 1.5.0

#### last_day

`last_day(date):` Retorna o último dia do mês ao qual a data pertence.

Exemplo:

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

Desde: 1.5.0

#### minuto

`minute(timestamp)`: Retorna o componente de minuto da string/timestamp.

Exemplo:

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

Desde: 1.5.0

#### mês

`month(date)` Retorna o componente de mês da data/carimbo de data e hora.

Exemplo:

```
> SELECT month('2016-07-30');
 7
```

Desde: 1.5.0

#### months_between

`months_between(timestamp1, timestamp2[, roundOff])`: Se `timestamp1` for posterior a `timestamp2`, o resultado será positivo. Se `timestamp1` e `timestamp2` estiverem no mesmo dia do mês, ou se ambos forem o último dia do mês, a hora do dia será ignorada. Caso contrário, a diferença é calculada com base em 31 dias por mês e arredondada para 8 dígitos, a menos que `roundOff=false`.

Exemplos:

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Desde: 1.5.0

#### next_day

`next_day(start_date, day_of_week)`: Retorna a primeira data posterior `start_date` e nomeada conforme indicado.

Exemplo:

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Desde: 1.5.0

#### trimestre

`quarter(date)`: Retorna o trimestre do ano para a data, no intervalo de 1 a 4.

Exemplo:

```
> SELECT quarter('2016-08-31');
 3
```

Desde: 1.5.0

#### second

`second(timestamp)`: Retorna o segundo componente da string/timestamp.

Exemplo:

```
> SELECT second('2009-07-30 12:58:59');
 59
```

Desde: 1.5.0

#### to_date

`to_date(date_str[, fmt])`: Analisa a `date_str` expressão com a `fmt` expressão até uma data. Retorna null com entrada inválida. Por padrão, ele segue regras de projeção para uma data se o item `fmt` for omitido.

Exemplos:

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Desde: 1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`: Analisa a `timestamp` expressão com a `fmt` expressão em um carimbo de data e hora. Retorna null com entrada inválida. Por padrão, ele segue regras de atribuição para um carimbo de data e hora se o formulário `fmt` for omitido.

Exemplos:

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

Desde: 2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`: Retorna o carimbo de data e hora UNIX do horário especificado.

Exemplo:

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Desde: 1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`: Interpreta um carimbo de data e hora como &#39;2017-07-14 02:40:00.0&#39; como um horário em um determinado fuso horário, e renderiza esse horário como um carimbo de data e hora em UTC. Por exemplo, &#39;GMT+1&#39; renderia &#39;2017-07-14 01:40:00.0&#39;.

Exemplo:

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Desde: 1.5.0

#### tronco

`trunc(date, fmt)`: Retorna a data com a parte do tempo do dia truncada para a unidade especificada pelo modelo de formato `fmt`. `fmt` é um de [&quot;year&quot;, &quot;yyyy&quot;, &quot;yy&quot;, &quot;mon&quot;, &quot;month&quot;, &quot;mm&quot;]

Exemplos:

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

Desde: 1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`: Retorna o carimbo de data e hora UNIX da hora atual ou especificada.

Exemplos:

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Desde: 1.5.0

#### dia útil

`weekday(date)`: Retorna o dia da semana para data/carimbo de data/hora (0 = segunda-feira, 1 = terça-feira, ..., 6 = domingo).

Exemplo:

```
> SELECT weekday('2009-07-30');
 3
```

Desde: 2.4.0

#### semana_do_ano

`weekofyear(date)`: Retorna a semana do ano da data especificada. Uma semana é considerada como start em uma segunda-feira e a semana 1 é a primeira semana com >3 dias.

Exemplo:

```
> SELECT weekofyear('2008-02-20');
 8
```

Desde: 1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`: Quando `expr1` = true, retorna `expr2`; else when `expr3` = true, retorna `expr4`; else retorna `expr5`.

Argumentos:

- `expr1`, `expr3`: As expressões de condição de ramificação devem ser do tipo booleano.
- `expr2`, `expr4`, `expr5`: As expressões de valor de ramificação e a expressão de valor else devem ser do mesmo tipo ou coerciveis a um tipo comum.

Exemplos:

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### ano

`year(date)`: Retorna o componente de ano da data/carimbo de data e hora.

Exemplo:

```
> SELECT year('2016-07-30');
 2016
```

Desde: 1.5.0

### funções de Agregação

#### aprox_count_different

`approx_count_distinct(expr[, relativeSD])`: Retorna a cardinalidade estimada por HyperLogLog++. `relativeSD` define o erro máximo de estimativa permitido.

### Matrizes

#### matriz

`array(expr, ...)`: Retorna uma matriz com os elementos especificados.

Exemplo:

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`: Retorna true se a matriz contiver o valor.

Exemplo:

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_different

`array_distinct(array)`: Remove valores de duplicado da matriz.

Exemplo:

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Desde: 2.4.0

#### array_exceto

`array_except(array1, array2)`: Retorna uma matriz dos elementos dentro, `array1` mas não dentro, `array2`sem duplicados.

Exemplo:

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Desde: 2.4.0

#### array_intersect

`array_intersect(array1, array2)`: Retorna uma matriz dos elementos na interseção de `array1` e `array2`, sem duplicados.

Exemplo:

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Desde: 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`: Concatena os elementos de determinada matriz usando o delimitador e uma string opcional para substituir valores nulos. Se nenhum valor for definido para `nullReplacement`, qualquer valor nulo será filtrado.

Exemplos:

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Desde: 2.4.0

#### array_max

`array_max(array)`: Retorna o valor máximo na matriz. Elementos nulos são ignorados.

Exemplo:

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

Desde: 2.4.0

#### array_min

`array_min(array)`: Retorna o valor mínimo na matriz. Elementos nulos são ignorados.

Exemplo:

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

Desde: 2.4.0

#### array_position

`array_position(array, element)`: Retorna o índice (baseado em 1) do primeiro elemento da matriz por quanto tempo.

Exemplo:

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Desde: 2.4.0

#### array_remove

`array_remove(array, element)`: Remova todos os elementos iguais ao elemento da matriz.

Exemplo:

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Desde: 2.4.0

#### array_again

`array_repeat(element, count)`: Retorna a matriz que contém o tempo de contagem de elementos.

Exemplo:

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Desde: 2.4.0

#### array_sort

`array_sort(array)`: Classifica a matriz de entrada em ordem crescente. Os elementos da matriz de entrada devem ser ordenáveis. Elementos nulos são colocados no final da matriz retornada.

Exemplo:

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Desde: 2.4.0

#### array_união

`array_union(array1, array2)`: Retorna uma matriz dos elementos na união de `array1` e `array2`, sem duplicados.

Exemplo:

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Desde: 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`: Retorna uma matriz unida de estruturas na qual a N-th struct contém todos os N-th valores de matrizes de entrada.

Exemplos:

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Desde: 2.4.0

#### element_at

`element_at(array, index)`: Retorna o elemento da matriz em determinado índice (baseado em 1). Se `index < 0`, acessa elementos do último ao primeiro. Retorna NULL se o índice exceder o comprimento da matriz.

`element_at(map, key)`: Retorna o valor de determinada chave, ou NULL se a chave não estiver contida no mapa

Exemplos:

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

Desde: 2.4.0

#### explosão

`explode(expr)`: Separa os elementos da matriz `expr` em várias linhas ou os elementos do mapa `expr` em várias linhas e colunas.

Exemplos:

```
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_external

`explode_outer(expr)`: Separa os elementos da matriz `expr` em várias linhas ou os elementos do mapa `expr` em várias linhas e colunas.

Exemplo:

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`: Retorna o índice (com base em 1) da string especificada (`str`) na lista delimitada por vírgulas (`str_array`). Retorna 0, se a string não foi encontrada ou se a string (`str`) especificada contiver uma vírgula.

Exemplo:

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### flatten

`flatten(arrayOfArrays)`: Transforma uma matriz de arrays em um único array.

Exemplo:

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Desde: 2.4.0

#### inline

`inline(expr)`: Explica uma matriz de estruturas em uma tabela.

Exemplo:

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_external

`inline_outer(expr)`: Explica uma matriz de estruturas em uma tabela.

Exemplo:

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### poexplode

`posexplode(expr)`: Separa os elementos da matriz `expr` em várias linhas com posições ou os elementos do mapa `expr` em várias linhas e colunas com posições.

Exemplo:

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_external

`posexplode_outer(expr)`: Separa os elementos da matriz `expr` em várias linhas com posições ou os elementos do mapa `expr` em várias linhas e colunas com posições.

Exemplo:

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### reverso

`reverse(array)`: Retorna uma string revertida ou uma matriz com ordem inversa de elementos.

Exemplos:

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

Desde: 1.5.0
>[!NOTE]
>
>a lógica RSE para matrizes está disponível desde 2.4.0.

#### embaralhamento

`shuffle(array)`: Retorna uma permutação aleatória da matriz em questão.

Exemplos:

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Desde: 2.4.0
>[!NOTE]
>
>não é determinista.

#### fatia

`slice(x, start, length)`: Subdefine a matriz x a partir do start de índice (ou a partir do final se o start for negativo) com o comprimento especificado.

Exemplos:

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Desde: 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`: Classifica a matriz de entrada em ordem crescente ou decrescente de acordo com a ordem natural dos elementos da matriz. Elementos nulos são colocados no início da matriz retornada em ordem crescente ou no final da matriz retornada em ordem decrescente.

Exemplos:

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`: Une os dois arrays especificados, em nível de elemento, em um único array usando a função. Se uma matriz for menor, os valores nulos serão anexados no final para corresponder ao comprimento da matriz mais longa, antes de aplicar a função.

Exemplos:

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

Desde: 2.4.0

### Funções de difusão de tipo de dados

#### bigint

`bigint(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `bigint`.

#### binário

`binary(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `binary`.

#### booleano

`boolean(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `boolean`.

#### elenco

`cast(expr AS type)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `type`.

Exemplo:

```
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `date`.

#### decimal

`decimal(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `decimal`.

#### duplo

`double(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `double`.

#### flutuante

`float(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `float`.

#### int

`int(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `int`.

#### mapa

`map(key0, value0, key1, value1, ...)`: Cria um mapa com os pares de chave/valor fornecidos.

Exemplo:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### minúsculo

`smallint(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`: Cria um mapa após dividir o texto em pares de chave/valor usando delimitadores. Os delimitadores padrão são &#39;,&#39; para `pairDelim` e &#39;:&#39; para `keyValueDelim`.

Exemplos:

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### string

`string(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `string`.

#### struct

`struct(col1, col2, col3, ...)`: Cria uma estrutura com os valores de campo especificados.

#### tinyint

`tinyint(expr)`: Faz a projeção do valor `expr` para o tipo de dados do público alvo `tinyint`.

### Funções de conversão e formatação

#### ascii

`ascii(str)`: Retorna o valor numérico do primeiro caractere de `str`.

Exemplos:

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`: Converte o argumento de um binário `bin` em uma string base 64.

Exemplo:

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### compartimento

`bin(expr)`: Retorna a representação da string do valor longo `expr` representado em binário.

Exemplos:

```
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`: Retorna o comprimento do bit dos dados da string ou o número de bits dos dados binários.

Exemplo:

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`: Retorna o caractere ASCII com o valor binário equivalente a `expr`. Se n for maior que 256, o resultado será equivalente a `chr(n % 256)`.

Exemplo:

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`: Retorna o comprimento do caractere dos dados da string ou o número de bytes dos dados binários. O comprimento dos dados da string inclui os espaços à direita. O comprimento dos dados binários inclui zeros binários.

Exemplos:

```
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)`: Retorna o comprimento do caractere dos dados da string ou o número de bytes dos dados binários. O comprimento dos dados da string inclui os espaços à direita. O comprimento dos dados binários inclui zeros binários.

Exemplos:

```
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`: Retorna o caractere ASCII com o equivalente binário a expr. Se n for maior que 256, o resultado será equivalente a `chr(n % 256)`

Exemplo:

```
> SELECT chr(65);
 A
```

#### graus

`degrees(expr)`: Converte radianos em graus.

Argumentos:
- `expr`: Ângulo em radianos

Exemplo:

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`: Formata o número `expr1` como &#39;#,###,###.##&#39;, arredondado às `expr2` casas decimais. Se `expr2` for 0, o resultado não terá ponto decimal ou parte fracional. `expr2` também aceita um formato especificado pelo usuário. Isso deve funcionar como o MySQL `FORMAT`.

Exemplos:

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`: Retorna um valor struct com os valores fornecidos `jsonStr` e `schema`.

Exemplos:

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Desde: 2.2.0

#### hash

`hash(expr1, expr2, ...)`: Retorna um valor hash dos argumentos.

Exemplo:

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### hexadecimal

`hex(expr)`: Converte `expr` em hexadecimal.

Exemplos:

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`: Retorna `str` com a primeira letra de cada palavra em maiúsculas. Todas as outras letras estão em minúsculas. As palavras são delimitadas por espaço em branco.

Exemplo:

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### maiúscula

`lcase(str)`: Retorna `str` com todos os caracteres alterados para minúsculas.

Exemplo:

```
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)`: Retorna `str` com todos os caracteres alterados para minúsculas.

Exemplo:

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`: Retorna `str`, preenchido à esquerda com `pad` um comprimento de `len`. Se `str` for maior que `len`, o valor de retorno será reduzido para `len` caracteres.

Exemplos:

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### mapa

`map(key0, value0, key1, value1, ...)`: Cria um mapa com os pares de chave/valor fornecidos.

Exemplo:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)`: Cria um mapa com um par das matrizes de chave/valor fornecidas. Os elementos nas chaves não podem ser nulos.

Exemplo:

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Desde: 2.4.0

#### map_from_tries

`map_from_entries(arrayOfEntries)`: Retorna um mapa criado a partir de determinada matriz de entradas.

Exemplo:

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Desde: 2.4.0

#### md5

`md5(expr)`: Retorna uma soma de verificação MD5 de 128 bits como uma sequência hexadecimal de `expr`.

Exemplo:

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`: Retorna `str`, preenchido à direita com `pad` um comprimento de `len`. Se `str` for maior que `len`, o valor de retorno será reduzido para `len` caracteres.

Exemplos:

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`: Remove os caracteres de espaço à direita de `str`.

`rtrim(trimStr, str)`: Remove a string à direita, que contém os caracteres da string de apara da `str`.

Argumentos:
- `str`: Uma expressão de string
- `trimStr`: Os caracteres de string de aparagem a serem aparados. O valor padrão é um espaço único

Exemplos:

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`: Retorna um valor de `sha1` hash como uma string hexadecimal do `expr`.

Exemplo:

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`: Retorna um valor de `sha1` hash como uma string hexadecimal do `expr`.

Exemplo:

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`: Retorna uma soma de verificação da família SHA-2 como uma sequência hexadecimal de `expr`. SHA-224, SHA-256, SHA-384 e SHA-512 são suportados. O comprimento de 0 bit equivale a 256.

Exemplo:

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`: Retorna o código Soundex da string.

Exemplo:

```
> SELECT soundex('Miller');
 M460
```

#### pilha

`stack(n, expr1, ..., exprk)`: Separa `expr1`, ..., `exprk` em `n` linhas.

Exemplo:

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`: Retorna a subsequência de caracteres dos start com comprimento `str` e comprimento `pos` , ou a parte da matriz de bytes que start com `len`e é de comprimento `pos` `len`.

Exemplos:

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### substring

`substring(str, pos[, len])`: Retorna a subsequência de caracteres dos start com comprimento `str` e comprimento `pos` , ou a parte da matriz de bytes que start com `len`e é de comprimento `pos` `len`.

Exemplos:

```
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`: Retorna uma string JSON com um determinado valor struct.

Exemplos:

```
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

Desde: 2.2.0

#### tradução

`translate(input, from, to)`: Traduz a `input` string substituindo os caracteres presentes na `from` string pelos caracteres correspondentes na `to` string.

Exemplo:

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`: Remove os caracteres de espaço à esquerda e à direita de `str`.

`trim(BOTH trimStr FROM str)`: Remova os `trimStr` caracteres à esquerda e à direita de `str`.

`trim(LEADING trimStr FROM str)`: Remova os `trimStr` caracteres à esquerda de `str`.

`trim(TRAILING trimStr FROM str)`: Remova os `trimStr` caracteres à direita de `str`.

Argumentos:
- `str`: Uma expressão de string
- `trimStr`: Os caracteres de string de aparagem a serem aparados, o valor padrão é um espaço único
- `BOTH`, `FROM`: Essas são palavras-chave para especificar caracteres de string de aparagem em ambas as extremidades da string
- `LEADING`, `FROM`: Essas são palavras-chave para especificar caracteres de string de aparagem na extremidade esquerda da string
- `TRAILING`, `FROM`: Essas são palavras-chave para especificar caracteres de string de aparagem na extremidade direita da string

Exemplos:

```
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### ucase

`ucase(str)`: Retorna `str` com todos os caracteres alterados para maiúsculas.

Exemplo:

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`: Converte o argumento de uma string base 64 `str` em um binário.

Exemplo:

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`: Converte hexadecimal `expr` em binário.

Exemplo:

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`: Retorna `str` com todos os caracteres alterados para maiúsculas.

Exemplo:

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`: Retorna uma string de identificador universalmente único (UUID). O valor é retornado como uma sequência canônica de 36 caracteres UID.

Exemplo:

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE]
>
>A função é não-determinística.

### Avaliação dos dados

#### coalescência

`coalesce(expr1, expr2, ...)`: Retorna o primeiro argumento não nulo, se existir. Caso contrário, nulo.

Exemplo:

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_lista

`collect_list(expr)`: Coleta e retorna uma lista de elementos não exclusivos.

#### collect_set

`collect_set(expr)`: Coleta e retorna um conjunto de elementos exclusivos.

#### concat

`concat(col1, col2, ..., colN)`: Retorna a concatenação de col1, col2, ..., colN.

Exemplos:

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE]
>
>`concat` lógica para matrizes está disponível desde 2.4.0.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`: Retorna a concatenação das strings separadas por `sep`.

Exemplo:

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`: Retorna o número total de linhas recuperadas, incluindo linhas que contêm null.

`count(expr[, expr...])`: Retorna o número de linhas para as quais as expressões fornecidas não são todas nulas.

`count(DISTINCT expr[, expr...])`: Retorna o número de linhas para as quais as expressões fornecidas são exclusivas e não nulas.

#### crc32

`crc32(expr)`: Retorna um valor de verificação de redundância cíclica do `expr` como padrão.

Exemplo:

```
> SELECT crc32('Spark');
 1557323817
```

#### decodificação

`decode(bin, charset)`: Decodifica o primeiro argumento usando o segundo conjunto de caracteres de argumento.

Exemplo:

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)`: Retorna a `n`entrada, por exemplo, retorna `input2` quando `n` é 2.

Exemplo:

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### codificar

`encode(str, charset)`: Codifica o primeiro argumento usando o segundo conjunto de caracteres de argumento.

Exemplo:

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`: Retorna o primeiro valor de `expr` para um grupo de linhas. Se `isIgnoreNull` for true, retornará somente valores não nulos.

#### first_value

`first_value(expr[, isIgnoreNull])`: Retorna o primeiro valor de `expr` para um grupo de linhas. Se `isIgnoreNull` for true, retornará somente valores não nulos.

#### get_json_object

`get_json_object(json_txt, path)`: Extrai um objeto json de `path`.

Exemplo:

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### agrupamento

<!-- was blank --->

#### group_id

<!-- was blank --->

#### instr

`instr(str, substr)`: Retorna o índice (baseado em 1) da primeira ocorrência de `substr` in `str`.

Exemplo:

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`: Retorna uma tupla como a função `get_json_object`, mas requer vários nomes. Todos os parâmetros de entrada e tipos de coluna de saída são string.

Exemplo:

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### atraso

`lag(input[, offset[, default]])`: Retorna o valor de `input` na `offset`linha anterior à linha atual na janela. O valor padrão de `offset` é 1 e o valor padrão de `default` é nulo. Se o valor de `input` na `offset`linha for nulo, null será retornado. Se essa linha de deslocamento não existir (por exemplo, quando o deslocamento for 1, a primeira linha da janela não terá nenhuma linha anterior) e `default` será retornada.

#### last

`last(expr[, isIgnoreNull])`: Retorna o último valor de `expr` para um grupo de linhas. Se `isIgnoreNull` for true, retornará somente valores não nulos.

#### last_value

`last_value(expr[, isIgnoreNull])`: Retorna o último valor de `expr` para um grupo de linhas. Se `isIgnoreNull` for true, retornará somente valores não nulos.

#### chumbo

`lead(input[, offset[, default]])`: Retorna o valor de `input` na `offset`linha após a linha atual na janela. O valor padrão de `offset` é 1 e o valor padrão de `default` é nulo. Se o valor de `input` na `offset`linha for nulo, null será retornado. Se essa linha de deslocamento não existir (por exemplo, quando o deslocamento for 1, a última linha da janela não terá nenhuma linha subsequente) e `default` será retornada.


#### left

`left(str, len)`: Retorna os caracteres mais à esquerda `len` (`len` podem ser do tipo string) da string `str`. Se `len` for menor que ou igual a 0, o resultado será uma string vazia.

Exemplo:

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)`: Retorna o comprimento do caractere dos dados da string ou o número de bytes dos dados binários. O comprimento dos dados da string inclui os espaços à direita. O comprimento dos dados binários inclui zeros binários.

Exemplos:

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### location

`locate(substr, str[, pos])`: Retorna a posição da primeira ocorrência de `substr` em `str` após a posição `pos`. O valor fornecido `pos` e o valor de retorno são baseados em 1.

Exemplos:

```
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`: Retorna a união de todos os mapas especificados.

Exemplo:

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Desde: 2.4.0

#### map_keys

`map_keys(map)`: Retorna uma matriz não ordenada que contém as chaves do mapa.

Exemplo:

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`: Retorna uma matriz não ordenada que contém os valores do mapa.

Exemplo:

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### bloco

`ntile(n)`: Divide as linhas de cada partição de janela em `n` compartimentos que variam de 1 a no máximo `n`.

#### nullif

`nullif(expr1, expr2)`: Retorna nulo se `expr1` for igual a `expr2`ou `expr1` diferente.

Exemplo:

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`: Retorna `expr2` se `expr1` for nulo ou `expr1` diferente.

Exemplo:

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`: Retorna `expr2` se não `expr1` for nulo, ou `expr3` não.

Exemplo:

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`: Extrai uma parte de um URL.

Exemplos:

```
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])`: Retorna a posição da primeira ocorrência de `substr` em `str` após a posição `pos`. O valor fornecido `pos` e o valor de retorno são baseados em 1.

Exemplos:

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### classificação

`rank()`: Calcula a classificação de um valor em um grupo de valores. O resultado é um mais o número de linhas anteriores ou iguais à linha atual na ordem da partição. Os valores produzem lacunas na sequência.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`: Extrai um grupo que corresponde `regexp`.

Exemplo:

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`: Substitui todas as subsequências de caracteres `str` que correspondem `regexp` com `rep`.

Exemplo:

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### repetição

`repeat(str, n)`: Retorna a string que repete o valor de string especificado n vezes.

Exemplo:

```
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`: Substitui todas as ocorrências de `search` com `replace`.

Argumentos:
- `str`: Uma expressão de string
- `search`: Uma expressão de string. Se não `search` for encontrado em `str`, `str` será retornado inalterado.
- `replace`: Uma expressão de string. Se não `replace` for especificado ou for uma string vazia, nada substituirá a string removida `str`.

Exemplo:

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### rollup

<!-- was blank -->

#### row_number

`row_number()`: Atribui um número exclusivo e sequencial a cada linha, começando com uma, de acordo com a ordem de linhas dentro da partição da janela.

#### schema_de_json

`schema_of_json(json[, options])`: Retorna o schema no formato DDL da string JSON.

Exemplo:

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Desde: 2.4.0

#### sentenças

`sentences(str[, lang, country])`: Divide-se `str` em um conjunto de palavras.

Exemplo:

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### sequência

`sequence(start, stop, step)`: Gera uma matriz de elementos do start para parar (inclusive), incrementando por etapa. O tipo dos elementos retornados é o mesmo que o tipo de expressão de argumento.

Os tipos suportados são: byte, curto, inteiro, longo, data, carimbo de data e hora.

As `start` expressões e `stop` as  devem ser resolvidas no mesmo tipo. Se `start` e `stop` o expressão forem resolvidos para o tipo &#39;date&#39; ou &#39;timestamp&#39;, a `step` expressão deverá ser resolvida para o tipo &#39;intervalo&#39;; caso contrário, ele resolverá para o mesmo tipo das `start` expressões e `stop` .

Argumentos:
- `start`: Uma expressão. O start do intervalo.
- `stop`: Uma expressão. O fim do intervalo (inclusive).
- `step`: Uma expressão opcional. A etapa do intervalo. Por padrão, `step` é 1 se `start` for menor que ou igual a `stop`, caso contrário, é -1. Para as sequências temporais é de 1 dia e -1 dia, respectivamente. Se `start` for maior que `stop`, o `step` deve ser negativo e vice-versa.

Exemplos:

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

Desde: 2.4.0

#### deslocamento para a esquerda

`shiftleft(base, expr)`: Deslocamento à esquerda em nível de bits.

Exemplo:

```
> SELECT shiftleft(2, 1);
 4
```

#### desvio

`shiftright(base, expr)`: Deslocamento à direita em nível de bits (assinado).

Exemplo:

```
> SELECT shiftright(4, 1);
 2
```

#### shift trightunsigned

`shiftrightunsigned(base, expr)`: Desvio à direita não assinado em nível de bits.

Exemplo:

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### tamanho

`size(expr)`: Retorna o tamanho de uma matriz ou mapa. A função retornará -1 se sua entrada for nula e `spark.sql.legacy.sizeOfNull` estiver definida como true. Se `spark.sql.legacy.sizeOfNull` for definida como false, a função retornará null para entrada nula. By default, the `spark.sql.legacy.sizeOfNull` parameter is set to true.

Exemplos:

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### espaço

`space(n)`: Retorna uma string que consiste em `n` espaços.

Exemplo:

```
> SELECT concat(space(2), '1');
   1
```

#### split

`split(str, regex)`: Divide `str` as ocorrências correspondentes `regex`.

Exemplo:

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`: Retorna a subsequência de caracteres de `str` antes `count` das ocorrências do delimitador `delim`. Se `count` for positivo, tudo à esquerda do delimitador final (contando da esquerda) será retornado. Se `count` for negativo, tudo à direita do delimitador final (contando da direita) será retornado. A função `substring_index` realiza uma correspondência que diferencia maiúsculas e minúsculas ao pesquisar por `delim`.

Exemplo:

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### janela

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`: Retorna uma matriz de string de valores dentro dos nós do xml que correspondem à expressão XPath.

Exemplo:

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_duplo

`xpath_double(xml, xpath)`: Retorna um valor de duplo, o valor zero se nenhuma correspondência for encontrada ou NaN se uma correspondência for encontrada, mas o valor for não numérico.

Exemplo:

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`: Retorna um valor flutuante, o valor zero se nenhuma correspondência for encontrada ou NaN se uma correspondência for encontrada, mas o valor não for numérico.

Exemplo:

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`: Retorna um valor inteiro, ou o valor zero se nenhuma correspondência for encontrada, ou se uma correspondência for encontrada, mas o valor não for numérico.

Exemplo:

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`: Retorna um valor inteiro longo, ou o valor zero se nenhuma correspondência for encontrada, ou se uma correspondência for encontrada, mas o valor não for numérico.

Exemplo:

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`: Retorna um valor de duplo, o valor zero se nenhuma correspondência for encontrada ou NaN se uma correspondência for encontrada, mas o valor for não numérico.

Exemplo:

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`: Retorna um valor inteiro curto, ou o valor zero se nenhuma correspondência for encontrada, ou se uma correspondência for encontrada, mas o valor não for numérico.

Exemplo:

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`: Retorna o conteúdo do texto do primeiro nó xml que corresponde à expressão XPath.

Exemplo:

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### Informações atuais

#### current_database

`current_database()`: Retorna o banco de dados atual.

Exemplo:

```
> SELECT current_database();
 default
```

#### current_date

`current_date()`: Retorna a data atual no start da avaliação do query.

Desde: 1.5.0

#### current_timestamp

`current_timestamp()`: Retorna o carimbo de data e hora atual no start da avaliação do query.

Desde: 1.5.0

#### now

`now()`: Retorna o carimbo de data e hora atual no start da avaliação do query.

Desde: 1.5.0
