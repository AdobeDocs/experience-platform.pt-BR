---
keywords: Experience Platform, home, tópicos populares, mapear csv, mapear arquivo csv, mapear arquivo csv para xdm, mapear csv para xdm, guia da interface do usuário, mapear, mapear campos, mapear funções de mapeamento;
solution: Experience Platform
title: Funções de mapeamento de preparação de dados
topic-legacy: overview
description: Este documento apresenta as funções de mapeamento usadas com a Preparação de dados.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: c01f8d9f785bec5be712c0a64a8347557db0577e
workflow-type: tm+mt
source-wordcount: '3971'
ht-degree: 4%

---

# Funções de mapeamento da preparação de dados

As funções de Preparação de dados podem ser usadas para calcular e calcular valores com base no que é inserido nos campos de origem.

## Campos

Um nome de campo pode ser qualquer identificador legal - uma sequência ilimitada de letras e dígitos Unicode, começando com uma letra, o cifrão (`$`) ou o caractere sublinhado (`_`). Os nomes de variáveis também diferenciam maiúsculas de minúsculas.

Se um nome de campo não seguir esta convenção, o nome do campo deve ser envolvido com `${}`. Assim, por exemplo, se o nome do campo for &quot;Nome&quot; ou &quot;Nome.Nome&quot;, o nome deverá ser colocado como `${First Name}` ou `${First.Name}` respectivamente.

Além disso, se um nome de campo for **any** das seguintes palavras-chave reservadas, elas devem estar vinculadas a `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Os dados nos subcampos podem ser acessados usando a notação de pontos. Por exemplo, se houver um `name` para acessar o `firstName` campo , use `name.firstName`.

## Lista de funções

As tabelas a seguir listam todas as funções de mapeamento compatíveis, incluindo expressões de amostra e suas saídas resultantes.

### Funções de string {#string}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Concatena as strings fornecidas. | <ul><li>CADEIA DE CARACTERES: As cadeias de caracteres que serão concatenadas.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Olá, &quot;, &quot;lá&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explodido | Divida a string com base em um regex e retorna uma matriz de partes. Opcionalmente, pode incluir regex para dividir a cadeia de caracteres. Por padrão, a divisão resolve para &quot;,&quot;. Os seguintes delimitadores **need** para ser evitada com `\`: `+, ?, ^, |, ., [, (, {, ), *, $, \` Se você incluir vários caracteres como delimitador, o delimitador será tratado como um delimitador de vários caracteres. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string que precisa ser dividida.</li><li>REGEX: *Opcional* A expressão regular que pode ser usada para dividir a string.</li></ul> | explode(STRING, REGEX) | explode(&quot;Olá, lá!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Retorna o local/índice de uma substring. | <ul><li>ENTRADA: **Obrigatório** A string que está sendo pesquisada.</li><li>SUBSTRING: **Obrigatório** A substring que está sendo pesquisada dentro da string.</li><li>START_POSITION: *Opcional* O local onde começar a procurar na string.</li><li>OCORRÊNCIA: *Opcional* A nona ocorrência a ser procurada a partir da posição inicial. Por padrão, é definido como 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCORRÊNCIA) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| substituidor | Substitui a string de pesquisa, se presente na string original. | <ul><li>ENTRADA: **Obrigatório** A string de entrada.</li><li>TO_FIND: **Obrigatório** A string a ser pesquisada na entrada.</li><li>TO_REPLACE: **Obrigatório** A string que substituirá o valor em &quot;TO_FIND&quot;.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;Esta é uma string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Este é um teste de substituição de string&quot; |
| substr | Retorna uma substring de um determinado comprimento. | <ul><li>ENTRADA: **Obrigatório** A string de entrada.</li><li>START_INDEX: **Obrigatório** O índice da string de entrada em que a substring é iniciada.</li><li>COMPRIMENTO: **Obrigatório** O comprimento da substring.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;Este é um teste de substring&quot;, 7, 8) | &quot; um subst&quot; |
| lower /<br>lcase | Converte uma cadeia de caracteres em minúsculas. | <ul><li>ENTRADA: **Obrigatório** A string que será convertida em minúsculas.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Converte uma cadeia de caracteres em maiúsculas. | <ul><li>ENTRADA: **Obrigatório** A string que será convertida em maiúsculas.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;OLÁ&quot; |
| split | Divide uma string de entrada em um separador. O seguinte separador **necessidades** para ser evitada com `\`: `\`. Se você incluir vários delimitadores, a string será dividida em **any** dos delimitadores presentes na string. | <ul><li>ENTRADA: **Obrigatório** A string de entrada que será dividida.</li><li>SEPARADOR: **Obrigatório** A string usada para dividir a entrada.</li></ul> | split(INPUT, SEPARADOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Usa o separador para unir uma lista de objetos. | <ul><li>SEPARADOR: **Obrigatório** A string que será usada para unir os objetos.</li><li>OBJETOS: **Obrigatório** Uma matriz de strings que serão unidas.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Olá mundo&quot; |
| lpad | Preenche o lado esquerdo de uma cadeira de caracteres com a outra determinada. | <ul><li>ENTRADA: **Obrigatório** A string que será preenchida. Essa string pode ser nula.</li><li>CONTAGEM: **Obrigatório** O tamanho da string a ser preenchida.</li><li>PREENCHIMENTO: **Obrigatório** A string com a qual colar a entrada. Se for nulo ou vazio, ele será tratado como um espaço único.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Preenche o lado direito de uma string com a outra string especificada. | <ul><li>ENTRADA: **Obrigatório** A string que será preenchida. Essa string pode ser nula.</li><li>CONTAGEM: **Obrigatório** O tamanho da string a ser preenchida.</li><li>PREENCHIMENTO: **Obrigatório** A string com a qual colar a entrada. Se for nulo ou vazio, ele será tratado como um espaço único.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Obtém os primeiros &quot;n&quot; caracteres da string especificada. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A sequência de caracteres para a qual você está obtendo os primeiros &quot;n&quot; caracteres.</li><li>CONTAGEM: **Obrigatório** Os caracteres &quot;n&quot; que você deseja obter da string.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Obtém os últimos &quot;n&quot; caracteres da string especificada. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A sequência de caracteres para a qual você está obtendo os últimos &quot;n&quot; caracteres.</li><li>CONTAGEM: **Obrigatório** Os caracteres &quot;n&quot; que você deseja obter da string.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Remove o espaço em branco do início da cadeia de caracteres. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string da qual você deseja remover o espaço em branco.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Remove o espaço em branco do final da cadeia de caracteres. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string da qual você deseja remover o espaço em branco.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Remove o espaço em branco do início e do fim da cadeia de caracteres. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string da qual você deseja remover o espaço em branco.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| igual a | Compara duas strings para confirmar se são iguais. Essa função diferencia maiúsculas e minúsculas. | <ul><li>STRING1: **Obrigatório** A primeira string que você deseja comparar.</li><li>CADEIA DE CARACTERES2: **Obrigatório** A segunda string que você deseja comparar.</li></ul> | STRING1. &#x200B;é igual( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;é igual a &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Compara duas strings para confirmar se são iguais. Esta função é **not** diferencia maiúsculas de minúsculas. | <ul><li>STRING1: **Obrigatório** A primeira string que você deseja comparar.</li><li>CADEIA DE CARACTERES2: **Obrigatório** A segunda string que você deseja comparar.</li></ul> | STRING1. &#x200B;é igual aIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

{style=&quot;table-layout:auto&quot;}

### Funções de expressão regular

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrai grupos da string de entrada, com base em uma expressão regular. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string da qual você está extraindo os grupos.</li><li>REGEX: **Obrigatório** A expressão regular que deseja que o grupo corresponda.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Verifica se a string corresponde à expressão regular inserida. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string que você está marcando corresponde à expressão regular.</li><li>REGEX: **Obrigatório** A expressão regular que está sendo comparada.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

{style=&quot;table-layout:auto&quot;}

### Funções de hash {#hashing}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Obtém uma entrada e um valor de hash usando o Algoritmo de Hash Seguro 1 (SHA-1). | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser submetido a hash.</li><li>CARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha1(ENTRADA, CARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Obtém uma entrada e um valor de hash usando o Algoritmo de Hash Seguro 256 (SHA-256). | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser submetido a hash.</li><li>CARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha256(ENTRADA, CARSET) | sha256(&quot;meu texto&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Obtém uma entrada e um valor de hash usando o Algoritmo de Hash Seguro 512 (SHA-512). | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser submetido a hash.</li><li>CARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha512(ENTRADA, CARSET) | sha512(&quot;meu texto&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Obtém uma entrada e um valor de hash usando MD5. | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser submetido a hash.</li><li>CARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Utiliza uma entrada para usar um algoritmo CRC (Cyclic Redundancy Check, verificação de redundância cíclica) para produzir um código cíclico de 32 bits. | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser submetido a hash.</li><li>CARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;meu texto&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### Funções de URL {#url}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Retorna o protocolo do URL especificado. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** O URL do qual o protocolo precisa ser extraído.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Retorna o host do URL especificado. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** O URL do qual o host precisa ser extraído.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Retorna a porta do URL especificado. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** O URL do qual a porta precisa ser extraída.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Retorna o caminho de determinada URL. Por padrão, o caminho completo é retornado. | <ul><li>URL: **Obrigatório** O URL do qual o caminho precisa ser extraído.</li><li>FULL_PATH: *Opcional* Um valor booleano que determina se o caminho completo é retornado. Se definido como false, somente o final do caminho será retornado.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; employee.csv&quot; |
| get_url_query_str | Retorna a string de consulta de um determinado URL. | <ul><li>URL: **Obrigatório** O URL do qual você está tentando obter a string de consulta.</li><li>ÂNCORA: **Obrigatório** Determina o que será feito com a âncora na string de consulta. Pode ser um dos três valores: &quot;manter&quot;, &quot;remover&quot; ou &quot;anexar&quot;.<br><br>Se o valor for &quot;reter&quot;, a âncora será anexada ao valor retornado.<br>Se o valor for &quot;remove&quot;, a âncora será removida do valor retornado.<br>Se o valor for &quot;append&quot;, a âncora será retornada como um valor separado.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/third?name= &#x200B; ferret#nose&quot;, &quot;keep&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/third?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com &#x200B;:8042/over/lá &#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### Funções de data e hora {#date-and-time}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela. Mais informações sobre o `date` pode ser encontrada na seção de datas da variável [guia de manipulação do formato de dados](./data-handling.md#dates).

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Recupera a hora atual. |  | now() | now() | `2021-10-26T10:10:24Z` |
| carimbo de data e hora | Recupera o horário Unix atual. |  | carimbo de data e hora() | carimbo de data e hora() | 1571850624571 |
| format | Formata a data de entrada de acordo com um formato especificado. | <ul><li>DATA: **Obrigatório** A data de entrada, como um objeto ZoningDateTime, que você deseja formatar.</li><li>FORMATO: **Obrigatório** O formato para o qual você deseja alterar a data.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;aaaa-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Converte um carimbo de data e hora em uma string de data de acordo com um formato especificado. | <ul><li>CARIMBO DE DATA E HORA: **Obrigatório** O carimbo de data e hora que você deseja formatar. Isso é escrito em milissegundos.</li><li>FORMATO: **Obrigatório** O formato no qual você deseja que o carimbo de data e hora se torne.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;aaaa-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | &quot;2019-10-23T11:24:35.000Z&quot; |
| data | Converte uma cadeia de caracteres de data em um objeto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A string que representa a data.</li><li>FORMATO: **Obrigatório** A string que representa o formato da data de origem.**Observação:** Isso faz **not** representa o formato no qual você deseja converter a string de data. </li><li>DEFAULT_DATE: **Obrigatório** A data padrão retornada, se a data fornecida for nula.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24:00Z&quot; |
| data | Converte uma cadeia de caracteres de data em um objeto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A string que representa a data.</li><li>FORMATO: **Obrigatório** A string que representa o formato da data de origem.**Observação:** Isso faz **not** representa o formato no qual você deseja converter a string de data. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| data | Converte uma cadeia de caracteres de data em um objeto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A string que representa a data.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Recupera as partes da data. Os seguintes valores de componentes são suportados: <br><br>&quot;ano&quot;<br>&quot;aaaa&quot;<br>&quot;yy&quot;<br><br>&quot;trimestre&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;mês&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;dia&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;semana&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;dia útil&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hora&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minuto&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;segundo&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;milissegundos&quot;<br>&quot;ms&quot; | <ul><li>COMPONENTE: **Obrigatório** Uma string que representa a parte da data. </li><li>DATA: **Obrigatório** A data, em um formato padrão.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, data(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | Substitui um componente em uma determinada data. Os seguintes componentes são aceitos: <br><br>&quot;ano&quot;<br>&quot;aaaa&quot;<br>&quot;yy&quot;<br><br>&quot;mês&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dia&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hora&quot;<br>&quot;hh&quot;<br><br>&quot;minuto&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;segundo&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPONENTE: **Obrigatório** Uma string que representa a parte da data. </li><li>VALOR: **Obrigatório** O valor a ser definido para o componente de uma determinada data.</li><li>DATA: **Obrigatório** A data, em um formato padrão.</li></ul> | set_date_part &#x200B;(COMPONENTE, VALOR, DATA) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | Cria uma data a partir de partes. Essa função também pode ser induzida usando make_timestamp. | <ul><li>ANO: **Obrigatório** O ano, escrito em quatro dígitos.</li><li>MÊS: **Obrigatório** O mês. Os valores permitidos são de 1 a 12.</li><li>DIA: **Obrigatório** O dia. Os valores permitidos são de 1 a 31.</li><li>HORA: **Obrigatório** A hora. Os valores permitidos são de 0 a 23.</li><li>MINUTO: **Obrigatório** O minuto. Os valores permitidos são de 0 a 59.</li><li>NANOSECOND: **Obrigatório** Os valores de nanossegundos. Os valores permitidos são de 0 a 999999999.</li><li>FUSO HORÁRIO: **Obrigatório** O fuso horário da data e hora.</li></ul> | make_date_time &#x200B;(ANO, MÊS, DIA, HORA, MINUTO, SEGUNDO, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Converte uma data em qualquer fuso horário em uma data em UTC. | <ul><li>DATA: **Obrigatório** A data em que você está tentando converter.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Converte uma data de um fuso horário em outro. | <ul><li>DATA: **Obrigatório** A data em que você está tentando converter.</li><li>ZONA: **Obrigatório** O fuso horário para o qual você está tentando converter a data.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### Hierarquias - Objetos {#objects}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| size_of | Retorna o tamanho da entrada. | <ul><li>ENTRADA: **Obrigatório** O objeto do qual você está tentando encontrar o tamanho.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Verifica se um objeto está vazio ou não. | <ul><li>ENTRADA: **Obrigatório** O objeto que você está tentando verificar está vazio.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | Cria uma lista de objetos. | <ul><li>ENTRADA: **Obrigatório** Um agrupamento de pares de chave e matriz.</li></ul> | arrays_to_object(INPUT) | amostra necessária | amostra necessária |
| to_object | Cria um objeto com base nos pares de chave/valor simples fornecidos. | <ul><li>ENTRADA: **Obrigatório** Uma lista simples de pares de chave/valor.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Cria um objeto a partir da string de entrada. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string que está sendo analisada para criar um objeto.</li><li>VALUE_DELIMITITER: *Opcional* O delimitador que separa um campo do valor. O delimitador padrão é `:`.</li><li>FIELD_DELIMITADOR: *Opcional* O delimitador que separa pares de valores de campo. O delimitador padrão é `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | phone - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| contains_key | Verifica se o objeto existe nos dados de origem. **Observação:** Essa função substitui a função obsoleta `is_set()` . | <ul><li>ENTRADA: **Obrigatório** O caminho a ser verificado se existir nos dados de origem.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| nula | Define o valor do atributo como `null`. Isso deve ser usado quando você não deseja copiar o campo para o schema de destino. |  | nullify() | nullify() | `null` |
| get_keys | Analisa os pares de chave/valor e retorna todas as chaves. | <ul><li>OBJETO: **Obrigatório** O objeto do qual as chaves serão extraídas.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Orgulho e Preconceito&quot;, &quot;livro2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analisa os pares de chave/valor e retorna o valor da string, com base na chave fornecida. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string que você deseja analisar.</li><li>CHAVE: **Obrigatório** A chave para a qual o valor deve ser extraído.</li><li>VALUE_DELIMITITER: **Obrigatório** O delimitador que separa o campo e o valor. Se uma `null` ou uma string vazia for fornecida, esse valor será `:`.</li><li>FIELD_DELIMITADOR: *Opcional* O delimitador que separa pares de campos e valores. Se uma `null` ou uma string vazia for fornecida, esse valor será `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |

{style=&quot;table-layout:auto&quot;}

### Hierarquias - Matrizes {#arrays}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Retorna o primeiro objeto não nulo em uma matriz específica. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o primeiro objeto não nulo.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;Second&quot;) | &quot;first&quot; |
| first | Recupera o primeiro elemento da matriz em questão. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o primeiro elemento.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera o último elemento da matriz. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o último elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Adiciona elementos ao final da matriz. | <ul><li>MATRIZ: **Obrigatório** A matriz à qual você está adicionando elementos.</li><li>VALORES: Os elementos que você deseja anexar à matriz.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&quot;a&quot;, &quot;b&quot;], &#39;c&#39;, &#39;d&#39;) | [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;] |
| join_arrays | Combina os arrays uns com os outros. | <ul><li>MATRIZ: **Obrigatório** A matriz à qual você está adicionando elementos.</li><li>VALORES: As matrizes que você deseja anexar à matriz principal.</li></ul> | join_arrays &#x200B;(ARRAY, VALUES) | join_arrays &#x200B;([&quot;a&quot;, &quot;b&quot;], [&quot;c&quot;], [&quot;d&quot;, &quot;e&quot;]) | [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;] |
| to_array | Obtém uma lista de entradas e a converte em uma matriz. | <ul><li>INCLUDE_NULLS: **Obrigatório** Um valor booleano para indicar se deve ou não incluir valores nulos na matriz de resposta.</li><li>VALORES: **Obrigatório** Os elementos que devem ser convertidos em uma matriz.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

{style=&quot;table-layout:auto&quot;}

### Operadores lógicos {#logical-operators}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decodificação | Dada uma chave e uma lista de pares de valores chave nivelados como uma matriz, a função retornará o valor se a chave for encontrada ou retornará um valor padrão se estiver presente na matriz. | <ul><li>CHAVE: **Obrigatório** A chave a ser correspondida.</li><li>OPTIONS: **Obrigatório** Uma matriz nivelada de pares de chave/valor. Opcionalmente, um valor padrão pode ser colocado no final.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pensilvânia&quot;, &quot;N/A&quot;) | Se o stateCode fornecido for &quot;ca&quot;, &quot;Califórnia&quot;.<br>Se o stateCode fornecido for &quot;pa&quot;, &quot;Pensilvânia&quot;.<br>Se o stateCode não corresponder ao seguinte, &quot;N/A&quot;. |
| iif | Avalia uma determinada expressão booleana e retorna o valor especificado com base no resultado. | <ul><li>EXPRESSÃO: **Obrigatório** A expressão booleana que está sendo avaliada.</li><li>TRUE_VALUE: **Obrigatório** O valor que é retornado se a expressão for avaliada como true.</li><li>FALSE_VALUE: **Obrigatório** O valor que é retornado se a expressão for avaliada como false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Verdadeiro&quot; |

{style=&quot;table-layout:auto&quot;}

### Agregação {#aggregation}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Retorna o mínimo dos argumentos fornecidos. Usa ordenação natural. | <ul><li>OPTIONS: **Obrigatório** Um ou mais objetos que podem ser comparados entre si.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Retorna o máximo dos argumentos fornecidos. Usa ordenação natural. | <ul><li>OPTIONS: **Obrigatório** Um ou mais objetos que podem ser comparados entre si.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### Tipo de conversões {#type-conversions}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Converte uma cadeia de caracteres em um BigInteger. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres a ser convertida em um BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Converte uma cadeia de caracteres em um Double. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string que deve ser convertida em um Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Converte uma string em um Flutuante. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string que deve ser convertida em um Flutuante.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Converte uma cadeia de caracteres em um número inteiro. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string que deve ser convertida em um Número inteiro.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### Funções JSON {#json}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Desserialize o conteúdo JSON da string especificada. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A string JSON a ser desserializada.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}) | Um objeto que representa o JSON. |

{style=&quot;table-layout:auto&quot;}

### Operações especiais {#special-operations}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Gera uma ID pseudo-aleatória. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### Funções do agente do usuário {#user-agent}

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrai o nome do sistema operacional da sequência de agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A sequência de agente do usuário.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrai a versão principal do sistema operacional da sequência de agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A sequência de agente do usuário.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrai a versão do sistema operacional da sequência de agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A sequência de agente do usuário.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1. |
| ua_os_name_version | Extrai o nome e a versão do sistema operacional da sequência de agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A sequência de agente do usuário.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrai a versão do agente da sequência de agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A sequência de agente do usuário.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1. |
| ua_agent_version_major | Extrai o nome do agente e a versão principal da sequência de agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A sequência de agente do usuário.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrai o nome do agente da sequência de agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A sequência de agente do usuário.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrai a classe do dispositivo da sequência de agente do usuário. | <ul><li>USER_AGENT: **Obrigatório** A sequência de agente do usuário.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versão/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefone |

{style=&quot;table-layout:auto&quot;}
