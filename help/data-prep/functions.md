---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;map;map fields;map funções de mapeamento;
solution: Experience Platform
title: Funções de mapeamento de preparo de dados
topic: overview
description: Este documento apresenta as funções de mapeamento usadas com a Preparação de dados.
translation-type: tm+mt
source-git-commit: 49124d58fffa3670b332fab07843f2ef3db65f79
workflow-type: tm+mt
source-wordcount: '3609'
ht-degree: 3%

---


# Funções de mapeamento da preparação de dados

As funções de Prep de dados podem ser usadas para calcular e calcular valores com base no que é inserido nos campos de origem.

## Campos

Um nome de campo pode ser qualquer identificador legal - uma sequência ilimitada de letras e dígitos Unicode, começando com uma letra, o símbolo de dólar (`$`) ou o caractere sublinhado (`_`). Os nomes de variáveis também fazem distinção entre maiúsculas e minúsculas.

Se um nome de campo não seguir esta convenção, o nome do campo deve estar vinculado a `${}`. Portanto, por exemplo, se o nome do campo for &quot;Nome&quot; ou &quot;Nome.Nome&quot;, o nome deverá ser vinculado como `${First Name}` ou `${First.Name}` respectivamente.

Além disso, os nomes de campo são **any** das seguintes palavras-chave reservadas, devem estar vinculados a `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Os dados nos subcampos podem ser acessados usando a notação de pontos. Por exemplo, se houver um objeto `name`, para acessar o campo `firstName`, use `name.firstName`.

## Lista de funções

As tabelas a seguir listas todas as funções de mapeamento suportadas, incluindo expressões de amostra e suas saídas resultantes.

### Funções de string

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | Concatena as strings fornecidas. | <ul><li>STRING: As cordas que serão concatenadas.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Oi, &quot;, &quot;lá&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explosão | Divide a string com base em um regex e retorna uma matriz de partes. Como opção, pode incluir regex para dividir a string. Por padrão, a divisão resolve para &quot;,&quot;. Os seguintes delimitadores **precisam** para serem escapados com `\`: `+, ?, ^, |, ., [, (, {, ), *, $, \` | <ul><li>STRING: **Obrigatório** A cadeia de caracteres que precisa ser dividida.</li><li>REGEX: *Opcional* A expressão regular que pode ser usada para dividir a string.</li></ul> | explode(STRING, REGEX) | explode(&quot;Oi, aqui!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Retorna o local/índice de uma substring. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres que está sendo pesquisada.</li><li>SUBSTRING: **Obrigatório** A subcadeia que está a ser procurada dentro da cadeia de caracteres.</li><li>START_POSITION: *Opcional* O local de onde o start deve ser exibido na sequência de caracteres.</li><li>OCORRÊNCIA: *Opcional* A enésima ocorrência a ser procurada a partir da posição do start. Por padrão, é definido como 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCORRÊNCIA) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| substituta | Substitui a string de pesquisa, se presente na string original. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres de entrada.</li><li>TO_FIND: **Obrigatório** A cadeia de caracteres para procurar dentro da entrada.</li><li>TO_REPLACE: **Obrigatório** A cadeia de caracteres que substituirá o valor em &quot;TO_FIND&quot;.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replace(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Este é um teste de substituição de string&quot; |
| substr | Retorna uma substring de um determinado comprimento. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres de entrada.</li><li>START_INDEX: **Obrigatório** O índice da cadeia de caracteres de entrada em que a subsequência de caracteres é start.</li><li>COMPRIMENTO: **Obrigatório** O comprimento da subsequência de caracteres.</li></ul> | ASTM(INPUT, START_INDEX, LENGTH) | SAA(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Converte uma string em minúsculas. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres que será convertida em minúsculas.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;EleLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Converte uma string em maiúsculas. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres que será convertida em maiúsculas.</li></ul> | above(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;OLÁ&quot; |
| split | Divide uma string de entrada em um separador. O seguinte separador **necessita de** para ser retirado com `\`: `\`. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres de entrada que será dividida.</li><li>SEPARADOR: **Obrigatório** A cadeia de caracteres usada para dividir a entrada.</li></ul> | split(INPUT, SEPARADOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Une uma lista de objetos usando o separador. | <ul><li>SEPARADOR: **Obrigatório** A cadeia de caracteres que será usada para unir os objetos.</li><li>OBJETOS: **Obrigatório** Uma matriz de cadeias de caracteres que serão unidas.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Olá mundo&quot; |
| lpad | Preenche o lado esquerdo de uma string com a outra string especificada. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres que será preenchida. Essa string pode ser nula.</li><li>CONTAGEM: **Obrigatório** O tamanho da cadeia de caracteres a ser preenchida.</li><li>PREENCHIMENTO: **Obrigatório** A cadeia de caracteres para colar a entrada. Se nulo ou vazio, será tratado como um único espaço.</li></ul> | lpad(ENTRADA, CONTAGEM, PREENCHIMENTO) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzyzybat&quot; |
| rpad | Preenche o lado direito de uma string com a outra string especificada. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres que será preenchida. Essa string pode ser nula.</li><li>CONTAGEM: **Obrigatório** O tamanho da cadeia de caracteres a ser preenchida.</li><li>PREENCHIMENTO: **Obrigatório** A cadeia de caracteres para colar a entrada. Se nulo ou vazio, será tratado como um único espaço.</li></ul> | rpad(ENTRADA, CONTAGEM, PREENCHIMENTO) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Obtém os primeiros caracteres &quot;n&quot; da string especificada. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres para a qual você está recebendo os primeiros caracteres &quot;n&quot;.</li><li>CONTAGEM: **Obrigatório** Os caracteres &quot;n&quot; que você deseja obter da string.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Obtém os últimos &quot;n&quot; caracteres da string especificada. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres para a qual você está obtendo os últimos &quot;n&quot; caracteres.</li><li>CONTAGEM: **Obrigatório** Os caracteres &quot;n&quot; que você deseja obter da string.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Remove o espaço em branco do início da string. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres da qual você deseja remover o espaço em branco.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Remove o espaço em branco do final da string. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres da qual você deseja remover o espaço em branco.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Remove o espaço em branco do início e do fim da string. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres da qual você deseja remover o espaço em branco.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| igual a | Compara duas strings para confirmar se são iguais. Essa função faz distinção entre maiúsculas e minúsculas. | <ul><li>STRING1: **Obrigatório** A primeira cadeia de caracteres que deseja comparar.</li><li>STRING2: **Obrigatório** A segunda cadeia de caracteres que deseja comparar.</li></ul> | STRING1. &#x200B;igual( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;igual a &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Compara duas strings para confirmar se são iguais. Esta função distingue maiúsculas de minúsculas **e não**. | <ul><li>STRING1: **Obrigatório** A primeira cadeia de caracteres que deseja comparar.</li><li>STRING2: **Obrigatório** A segunda cadeia de caracteres que deseja comparar.</li></ul> | STRING1. &#x200B;igualIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;igualIgnoreCase &#x200B;(&quot;STRING1&quot;) | true |

&#x200B;

### Funções de expressão regular

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| extract_regex | Extrai grupos da string de entrada, com base em uma expressão regular. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres da qual você está extraindo os grupos.</li><li>REGEX: **Obrigatório** A expressão regular que você deseja que o grupo corresponda.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Verifica se a string corresponde à expressão regular inserida. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres que você está verificando corresponde à expressão normal.</li><li>REGEX: **Obrigatório** A expressão normal que você está comparando.</li></ul> | matches_regex(STRING, REGEX) | corresponde_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

### Funções de hash

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | Obtém uma entrada e produz um valor de hash usando o Secure Hash Algorithm 1 (SHA-1). | <ul><li>ENTRADA: **Necessário** O texto sem formatação a ser submetido a hash.</li><li>CARIMBO: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha1(ENTRADA, CARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Obtém uma entrada e produz um valor de hash usando o Secure Hash Algorithm 256 (SHA-256). | <ul><li>ENTRADA: **Necessário** O texto sem formatação a ser submetido a hash.</li><li>CARIMBO: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha256(ENTRADA, CARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Obtém uma entrada e produz um valor de hash usando o Secure Hash Algorithm 512 (SHA-512). | <ul><li>ENTRADA: **Necessário** O texto sem formatação a ser submetido a hash.</li><li>CARIMBO: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha512(ENTRADA, CARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 888a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Obtém uma entrada e produz um valor de hash usando MD5. | <ul><li>ENTRADA: **Necessário** O texto sem formatação a ser submetido a hash.</li><li>CARIMBO: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII. </li></ul> | md5(ENTRADA, CARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Utiliza uma entrada para usar um algoritmo CRC (Cyclic Redundancy Check [verificação de redundância cíclica]) para produzir um código cíclico de 32 bits. | <ul><li>ENTRADA: **Necessário** O texto sem formatação a ser submetido a hash.</li><li>CARIMBO: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | crc32(ENTRADA, CARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### Funções de URL

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | Retorna o protocolo do URL fornecido. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** O URL a partir do qual o protocolo precisa ser extraído.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Retorna o host do URL especificado. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** O URL a partir do qual o host precisa ser extraído.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Retorna a porta do URL especificado. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** O URL a partir do qual a porta precisa ser extraída.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Retorna o caminho do URL especificado. Por padrão, o caminho completo é retornado. | <ul><li>URL: **Obrigatório** O URL a partir do qual o caminho precisa ser extraído.</li><li>FULL_PATH: *Opcional* Um valor booliano que determina se o caminho completo é retornado. Se definido como false, somente o final do caminho será retornado.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; empregado.csv&quot; |
| get_url_query_str | Retorna a string de query de um determinado URL. | <ul><li>URL: **Obrigatório** O URL do qual você está tentando obter a string do query.</li><li>ÂNCORA: **Required** Determina o que será feito com a âncora na string do query. Pode ser um dos três valores: &quot;reter&quot;, &quot;remover&quot; ou &quot;acrescentar&quot;.<br><br>Se o valor for &quot;reter&quot;, a âncora será anexada ao valor retornado.<br>Se o valor for &quot;remove&quot;, a âncora será removida do valor retornado.<br>Se o valor for &quot;append&quot; (Acrescentar), a âncora será retornada como um valor separado.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;retém&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042/over &#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Funções de data e hora

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | Recupera a hora atual. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| carimbo de data e hora | Recupera o tempo Unix atual. |  | carimbo de data e hora() | carimbo de data e hora() | 1571850624571 |
| format | Formata a data de entrada de acordo com um formato especificado. | <ul><li>DATA: **Obrigatório** A data de entrada, como um objeto ZoningDateTime, que você deseja formatar.</li><li>FORMATO: **Obrigatório** O formato para o qual você deseja alterar a data.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;aaaa-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Converte um carimbo de data e hora em uma string de data de acordo com um formato especificado. | <ul><li>CARIMBO DE DATA E HORA: **Obrigatório** O carimbo de data e hora que deseja formatar. Isto está escrito em milissegundos.</li><li>FORMATO: **Obrigatório** O formato para o qual você deseja alterar o carimbo de data e hora.</li></ul> | dformat &#x200B;(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-out-2019 11:24&quot; |
| data | Converte uma string de data em um objeto ZondedDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A cadeia de caracteres que representa a data.</li><li>FORMATO: **Obrigatório** A cadeia de caracteres que representa o formato da data.</li><li>DEFAULT_DATE: **Obrigatório** A data padrão retornada, se a data fornecida for nula.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| data | Converte uma string de data em um objeto ZondedDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A cadeia de caracteres que representa a data.</li><li>FORMATO: **Obrigatório** A cadeia de caracteres que representa o formato da data.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| data | Converte uma string de data em um objeto ZondedDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A cadeia de caracteres que representa a data.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Recupera as partes da data. Os seguintes valores de componente são suportados: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;Trimestre&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;&lt;a 11/>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;dia útil&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minuto&quot;<br>&quot;mi&quot;<br>&quot;n&quot; a28/>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisegundo&quot;<br>&quot;ms&quot;<br><br><br> | <ul><li>COMPONENTE: **Obrigatório** Uma string que representa a parte da data. </li><li>DATA: **Obrigatório** A data, em um formato padrão.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Substitui um componente em uma determinada data. Os seguintes componentes são aceitos: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;&lt;a1 1/>&quot;minuto&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;segundo&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br> | <ul><li>COMPONENTE: **Obrigatório** Uma string que representa a parte da data. </li><li>VALOR: **Obrigatório** O valor a ser definido para o componente para uma determinada data.</li><li>DATA: **Obrigatório** A data, em um formato padrão.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Cria uma data de partes. Essa função também pode ser induzida usando make_timestamp. | <ul><li>ANO: **Obrigatório** O ano, escrito em quatro dígitos.</li><li>MÊS: **Obrigatório** O mês. Os valores permitidos são de 1 a 12.</li><li>DIA: **Obrigatório** O dia. Os valores permitidos são de 1 a 31.</li><li>HORA: **Obrigatório** A hora. Os valores permitidos são de 0 a 23.</li><li>MINUTO: **Necessário** O minuto. Os valores permitidos são de 0 a 59.</li><li>NANOSECOND: **Obrigatório** Os valores de nanossegundos. Os valores permitidos são 0 a 999999999.</li><li>FUSO HORÁRIO: **Obrigatório** O fuso horário para a hora da data.</li></ul> | make_date_time &#x200B;(ANO, MÊS, DIA, HORA, MINUTO, SEGUNDO, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;América/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Converte uma data em qualquer fuso horário em uma data em UTC. | <ul><li>DATA: **Obrigatório** A data em que está a tentar converter.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Converte uma data de um fuso horário para outro. | <ul><li>DATA: **Obrigatório** A data em que está a tentar converter.</li><li>ZONA: **Obrigatório** O fuso horário para o qual você está tentando converter a data.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

&#x200B;

### Hierarquias - Objetos

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | Retorna o tamanho da entrada. | <ul><li>ENTRADA: **Obrigatório** O objeto do qual você está tentando encontrar o tamanho.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Verifica se um objeto está vazio ou não. | <ul><li>ENTRADA: **Obrigatório** O objeto que está a tentar verificar está vazio.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | Cria uma lista de objetos. | <ul><li>ENTRADA: **Obrigatório** Um agrupamento de pares de chaves e matrizes.</li></ul> | arrays_to_object(INPUT) | amostra necessidade | amostra necessidade |
| to_object | Cria um objeto com base nos pares de chave/valor simples fornecidos. | <ul><li>ENTRADA: **Obrigatório** Uma lista simples de pares de chaves/valores.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Cria um objeto a partir da string de entrada. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres que está sendo analisada para criar um objeto.</li><li>VALUE_DELIMITER: *Opcional* O delimitador que separa um campo do valor. O delimitador padrão é `:`.</li><li>FIELD_DELIMITADOR: *Opcional* O delimitador que separa pares de valores de campo. O delimitador padrão é `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | phone - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Verifica se o objeto existe nos dados de origem. | <ul><li>ENTRADA: **Obrigatório** O caminho a ser verificado se ele existir nos dados de origem.</li></ul> | is_set(INPUT) | is_set &#x200B;(&quot;evars.evar.field1&quot;) | true |
| null | Define o valor do atributo para `null`. Isso deve ser usado quando você não deseja copiar o campo para o schema do público alvo. |  | void() | void() | `null` |

### Hierarquias - Matrizes

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| coalescência | Retorna o primeiro objeto não nulo em uma determinada matriz. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o primeiro objeto não nulo.</li></ul> | coalesce (ENTRADA) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Recupera o primeiro elemento da matriz em questão. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o primeiro elemento.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera o último elemento da matriz especificada. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o último elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | Obtém uma lista de entradas e a converte em um storage. | <ul><li>INCLUDE_NULLS: **Obrigatório** Um valor booliano para indicar se deve ou não incluir valores nulos na matriz de respostas.</li><li>VALORES: **Obrigatório** Os elementos que devem ser convertidos em uma matriz.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Operadores lógicos

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decodificação | Considerando uma chave e uma lista de pares de valores chave nivelados como uma matriz, a função retornará o valor se a chave for encontrada ou retornará um valor padrão se estiver presente na matriz. | <ul><li>CHAVE: **Obrigatório** A chave a ser correspondida.</li><li>OPTIONS: **Necessário** Uma matriz nivelada de pares de chaves/valores. Como opção, um valor padrão pode ser colocado no final.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Se stateCode fornecido for &quot;ca&quot;, &quot;California&quot;.<br>Se o stateCode fornecido for &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Se o stateCode não corresponder ao seguinte, &quot;N/A&quot;. |
| iif | Avalia uma determinada expressão booleana e retorna o valor especificado com base no resultado. | <ul><li>EXPRESSÃO: **Obrigatório** A expressão booleana que está sendo avaliada.</li><li>TRUE_VALUE: **Obrigatório** O valor que é retornado se a expressão for avaliada como true.</li><li>FALSE_VALUE: **Required** O valor que é retornado se a expressão for avaliada como false.</li></ul> | iif(EXPRESSÃO, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Verdadeiro&quot; |

### Agregação

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | Retorna o mínimo dos argumentos fornecidos. Usa ordenação natural. | <ul><li>OPTIONS: **Obrigatório** Um ou mais objetos que podem ser comparados entre si.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Retorna o máximo dos argumentos fornecidos. Usa ordenação natural. | <ul><li>OPTIONS: **Obrigatório** Um ou mais objetos que podem ser comparados entre si.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### Conversões de tipo

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | Converte uma string em um BigInteger. | <ul><li>STRING: **Required** A cadeia de caracteres que deve ser convertida em BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Converte uma string em um Duplo. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres que deve ser convertida em um Duplo.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Converte uma string em Flutuante. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres que deve ser convertida em Flutuante.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Converte uma string em um número inteiro. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres que deve ser convertida em um Número Inteiro.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### Funções JSON

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | Deserialize o conteúdo JSON da string especificada. | <ul><li>STRING: **Obrigatório** A cadeia de caracteres JSON a ser desserializada.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}}) | Um objeto que representa o JSON. |

### Operações especiais

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | Gera uma ID pseudo-aleatória. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c20633 |

### Funções do agente do usuário

>[!NOTE]
>
>Role para a esquerda/direita para visualização do conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Exemplo de saída |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | Extrai o nome do sistema operacional da string do agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A cadeia de caracteres do agente do usuário.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrai a versão principal do sistema operacional da string do agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A cadeia de caracteres do agente do usuário.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrai a versão do sistema operacional da string do agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A cadeia de caracteres do agente do usuário.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrai o nome e a versão do sistema operacional da string do agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A cadeia de caracteres do agente do usuário.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrai a versão do agente da string do agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A cadeia de caracteres do agente do usuário.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extrai o nome do agente e a versão principal da string do agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A cadeia de caracteres do agente do usuário.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrai o nome do agente da string do agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A cadeia de caracteres do agente do usuário.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrai a classe do dispositivo da string do agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A cadeia de caracteres do agente do usuário.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefone |