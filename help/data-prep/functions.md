---
keywords: Experience Platform;página inicial;tópicos populares;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia de interface do usuário;mapeador;mapeamento;mapear campos;mapear funções;
solution: Experience Platform
title: Funções de mapeamento de preparação de dados
description: Este documento apresenta as funções de mapeamento usadas com o Preparo de dados.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '6009'
ht-degree: 1%

---

# Funções de mapeamento de Preparo de dados

As funções de Preparo de dados podem ser usadas para calcular e calcular valores com base no que é inserido em campos de origem.

## Campos

Um nome de campo pode ser qualquer identificador legal - uma sequência ilimitada de letras e dígitos Unicode, começando com uma letra, o cifrão (`$`) ou o caractere de sublinhado (`_`). Os nomes de variáveis também fazem distinção entre maiúsculas e minúsculas.

Se um nome de campo não segue essa convenção, o nome do campo deve ser colocado entre `${}`. Portanto, por exemplo, se o nome do campo for &quot;Nome&quot; ou &quot;Nome.Nome&quot;, o nome deverá ser encapsulado como `${First Name}` ou `${First\.Name}` respectivamente.

>[!TIP]
>
>Ao interagir com hierarquias, se um atributo filho tiver um ponto (`.`), você deverá usar uma barra invertida (`\`) para usar escape em caracteres especiais. Para obter mais informações, leia o manual sobre [como escapar caracteres especiais](home.md#escape-special-characters).

Se um nome de campo for **qualquer** das seguintes palavras-chave reservadas, ele deverá ser empacotado com `${}{}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

Além disso, as palavras-chave reservadas também incluem qualquer uma das funções do mapeador listadas nesta página.

Os dados em subcampos podem ser acessados usando a notação de pontos. Por exemplo, se havia um objeto `name`, para acessar o campo `firstName`, use `name.firstName`.

## Lista de funções

As tabelas a seguir listam todas as funções de mapeamento compatíveis, incluindo expressões de amostra e suas saídas resultantes.

### Funções de string {#string}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Concatena as sequências de caracteres fornecidas. | <ul><li>STRING: as cadeias de caracteres que serão concatenadas.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explodir | Divide a sequência de caracteres com base em um regex e retorna uma matriz de partes. Opcionalmente, pode incluir regex para dividir a cadeia de caracteres. Por padrão, a divisão é resolvida como &quot;,&quot;. Os seguintes delimitadores **precisam** de escape com `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Se você incluir vários caracteres como delimitador, ele será tratado como um delimitador de vários caracteres. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres que precisa ser dividida.</li><li>REGEX: *Opcional* A expressão regular que pode ser usada para dividir a cadeia de caracteres.</li></ul> | explode(STRING, REGEX) | explode(&quot;Olá!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Retorna o local/índice de uma substring. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres que está sendo pesquisada.</li><li>SUBSTRING: **Obrigatório** A subcadeia de caracteres que está sendo pesquisada na cadeia de caracteres.</li><li>START_POSITION: *Opcional* O local de onde começar a pesquisar na cadeia de caracteres.</li><li>OCORRÊNCIA: *Opcional* A enésima ocorrência a ser procurada a partir da posição inicial. Por padrão, é definido como 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacester | Substitui a cadeia de caracteres de pesquisa, se presente na cadeia de caracteres original. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres de entrada.</li><li>TO_FIND: **Obrigatório** A cadeia de caracteres a ser pesquisada na entrada.</li><li>TO_REPLACE: **Obrigatório** A cadeia de caracteres que substituirá o valor em &quot;TO_FIND&quot;.</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;Isto é uma sequência de caracteres re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Este é um teste de substituição de cadeia de caracteres&quot; |
| substr | Retorna uma substring de um determinado comprimento. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres de entrada.</li><li>START_INDEX: **Obrigatório** O índice da cadeia de caracteres de entrada em que a subsequência de caracteres é iniciada.</li><li>LENGTH: **Required** O comprimento da subcadeia de caracteres.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;Este é um teste de substring&quot;, 7, 8) | &quot;um subconjunto&quot; |
| lower /<br>lcase | Converte uma cadeia de caracteres em minúsculas. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres que será convertida em minúsculas.</li></ul> | lower(INPUT) | lower(&quot;HeLL&quot;)<br>lcase(&quot;HeLL&quot;) | &quot;olá&quot; |
| upper /<br>ucase | Converte uma cadeia de caracteres em maiúsculas. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres que será convertida em maiúsculas.</li></ul> | upper(ENTRADA) | upper(&quot;HeLL&quot;)<br>ucase(&quot;HeLL&quot;) | &quot;OLÁ&quot; |
| split | Divide uma cadeia de caracteres de entrada em um separador. O seguinte separador **precisa** de escape com `\`: `\`. Se você incluir vários delimitadores, a cadeia de caracteres será dividida em **qualquer** dos delimitadores presentes na cadeia de caracteres. **Observação:** esta função retorna apenas índices não nulos da cadeia de caracteres, independentemente da presença do separador. Se todos os índices, incluindo nulos, forem necessários na matriz resultante, use a função &quot;explodir&quot;. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres de entrada que será dividida.</li><li>SEPARATOR: **Obrigatório** A cadeia de caracteres usada para dividir a entrada.</li></ul> | split(ENTRADA, SEPARADOR) | split(&quot;Olá mundo&quot;, &quot; &quot;) | `["Hello", "world"]` |
| ingressar | Une uma lista de objetos usando o separador. | <ul><li>SEPARATOR: **Obrigatório** A cadeia de caracteres que será usada para unir os objetos.</li><li>OBJETOS: **Obrigatório** Uma matriz de cadeias de caracteres que serão unidas.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Olá, mundo&quot; |
| lpad | Preenche o lado esquerdo de uma cadeira de caracteres com a outra cadeira de caracteres especificada. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres a ser preenchida. Esta cadeia de caracteres pode ser nula.</li><li>COUNT: **Obrigatório** O tamanho da cadeia de caracteres a ser preenchida.</li><li>PREENCHIMENTO: **Obrigatório** A cadeia de caracteres com a qual preencher a entrada. Se for nulo ou estiver vazio, será tratado como um único espaço.</li></ul> | lpad(ENTRADA, CONTAGEM, PREENCHIMENTO) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Preenche o lado direito de uma cadeia de caracteres com a outra cadeia de caracteres fornecida. | <ul><li>ENTRADA: **Obrigatório** A cadeia de caracteres a ser preenchida. Esta cadeia de caracteres pode ser nula.</li><li>COUNT: **Obrigatório** O tamanho da cadeia de caracteres a ser preenchida.</li><li>PREENCHIMENTO: **Obrigatório** A cadeia de caracteres com a qual preencher a entrada. Se for nulo ou estiver vazio, será tratado como um único espaço.</li></ul> | rpad(ENTRADA, CONTAGEM, PREENCHIMENTO) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Obtém os primeiros caracteres &quot;n&quot; da cadeira de caracteres fornecida. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres para a qual você está obtendo os primeiros caracteres &quot;n&quot;.</li><li>COUNT: **Obrigatório** Os caracteres &quot;n&quot; que você deseja obter da cadeia de caracteres.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| direita | Obtém os últimos caracteres &quot;n&quot; da cadeira de caracteres fornecida. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres para a qual você está obtendo os últimos caracteres &quot;n&quot;.</li><li>COUNT: **Obrigatório** Os caracteres &quot;n&quot; que você deseja obter da cadeia de caracteres.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Remove o espaço em branco do início da cadeira de caracteres. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres da qual você deseja remover o espaço em branco.</li></ul> | ltrim(STRING) | ltrim(&quot; Olá&quot;) | &quot;olá&quot; |
| rtrim | Remove o espaço em branco do final da cadeira de caracteres. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres da qual você deseja remover o espaço em branco.</li></ul> | rtrim(STRING) | rtrim(&quot;alô&quot;) | &quot;olá&quot; |
| trim | Remove o espaço em branco do início e do fim da sequência de caracteres. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres da qual você deseja remover o espaço em branco.</li></ul> | trim(STRING) | trim(&quot; olá &quot;) | &quot;olá&quot; |
| igual a | Compara duas strings para confirmar se são iguais. Esta função diferencia maiúsculas de minúsculas. | <ul><li>STRING1: **Obrigatório** A primeira cadeia de caracteres que você deseja comparar.</li><li>CADEIA DE CARACTERES2: **Obrigatório** A segunda cadeia de caracteres que você deseja comparar.</li></ul> | STRING1.&#x200B;equals(&#x200B;STRING2) | &quot;string1&quot;.&#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Compara duas strings para confirmar se são iguais. Esta função **não** diferencia maiúsculas de minúsculas. | <ul><li>STRING1: **Obrigatório** A primeira cadeia de caracteres que você deseja comparar.</li><li>CADEIA DE CARACTERES2: **Obrigatório** A segunda cadeia de caracteres que você deseja comparar.</li></ul> | STRING1.&#x200B;equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;.&#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### Funções de expressão regular

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrai grupos da string de entrada, com base em uma expressão regular. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres da qual você está extraindo os grupos.</li><li>REGEX: **Obrigatório** A expressão regular que você deseja que o grupo corresponda.</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(&quot;E259,E259B_009,1_1&quot;&#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Verifica se a string corresponde à expressão regular inserida. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres que você está verificando corresponde à expressão regular.</li><li>REGEX: **Obrigatório** A expressão regular com a qual você está comparando.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

{style="table-layout:auto"}

### Funções de hash {#hashing}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Pega uma entrada e produz um valor de hash usando o Algoritmo de hash seguro 1 (SHA-1). | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser hash.</li><li>CHARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha1(ENTRADA, CHARSET) | sha1(&quot;meu texto&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24&#x200B;48690840c5dfcce3c80 |
| sha256 | Pega uma entrada e produz um valor de hash usando o Algoritmo de hash seguro 256 (SHA-256). | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser hash.</li><li>CHARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha256(ENTRADA, CHARSET) | sha256(&quot;meu texto&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Pega uma entrada e produz um valor de hash usando o Algoritmo de hash seguro 512 (SHA-512). | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser hash.</li><li>CHARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha512(ENTRADA, CHARSET) | sha512(&quot;meu texto&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb107 2a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Pega uma entrada e produz um valor de hash usando MD5. | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser hash.</li><li>CHARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII. </li></ul> | md5(ENTRADA, CHARSET) | md5(&quot;meu texto&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | Pega uma entrada e usa um algoritmo de verificação de redundância cíclica (CRC) para produzir um código cíclico de 32 bits. | <ul><li>ENTRADA: **Obrigatório** O texto sem formatação a ser hash.</li><li>CHARSET: *Opcional* O nome do conjunto de caracteres. Os valores possíveis incluem UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;meu texto&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### Funções de URL {#url}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Retorna o protocolo do URL fornecido. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** A URL da qual o protocolo precisa ser extraído.</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform&#x200B;.adobe.com/home&quot;) | https |
| get_url_host | Retorna o host do URL fornecido. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** A URL da qual o host precisa ser extraído.</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform&#x200B;.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Retorna a porta do URL fornecido. Se a entrada for inválida, retornará null. | <ul><li>URL: **Obrigatório** A URL da qual a porta precisa ser extraída.</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/&#x200B;joe/employee.csv&quot;) | 22 |
| get_url_path | Retorna o caminho do URL fornecido. Por padrão, o caminho completo é retornado. | <ul><li>URL: **Obrigatório** A URL da qual o caminho precisa ser extraído.</li><li>FULL_PATH: *Opcional* Um valor booliano que determina se o caminho completo é retornado. Se definido como false, somente o final do caminho é retornado.</li></ul> | get_url_path&#x200B;(URL, CAMINHO_COMPLETO) | get_url_path&#x200B;(&quot;sftp://example.com//&#x200B;home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B;employee.csv&quot; |
| get_url_query_str | Retorna a cadeia de caracteres de consulta de um determinado URL como um mapa de nome de cadeia de caracteres de consulta e valor de cadeia de caracteres de consulta. | <ul><li>URL: **Obrigatório** A URL da qual você está tentando obter a cadeia de caracteres de consulta.</li><li>ÂNCORA: **Obrigatório** Determina o que será feito com a âncora na cadeia de caracteres de consulta. Pode ser um destes três valores: &quot;keep&quot;, &quot;remove&quot; ou &quot;append&quot;.<br><br>Se o valor for &quot;reter&quot;, a âncora será anexada ao valor retornado.<br>Se o valor for &quot;remover&quot;, a âncora será removida do valor retornado.<br>Se o valor for &quot;append&quot;, a âncora será retornada como um valor separado.</li></ul> | get_url_query_str&#x200B;(URL, ÂNCORA) | get_url_query&#x200B;(&quot;foo://example.com foo://example.com:8042&#x200B;/over/there?name=&#x200B;ferret#ferret&quot;, &quot;reter&quot;)<br>get url_str&#x200B; &#x200B; &#x200B; &#x200B; &#x200B; &#x200B;(&quot;2}acima/lá?name=ferrett&quot;, &quot;remove&quot;:8042get url_query_str(&quot;foo://example.com4}/acima/ali?name=ferret#nariz&quot;, &quot;append&quot;)<br>:8042 | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | Essa função pega uma URL como entrada e substitui ou codifica os caracteres especiais por caracteres ASCII. Para obter mais informações sobre caracteres especiais, leia a [lista de caracteres especiais](#special-characters) no apêndice deste documento. | <ul><li>URL: **Obrigatório** A URL de entrada com caracteres especiais que você deseja substituir ou codificar com caracteres ASCII.</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>://example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | Essa função pega uma URL como entrada e decodifica os caracteres ASCII em caracteres especiais.  Para obter mais informações sobre caracteres especiais, leia a [lista de caracteres especiais](#special-characters) no apêndice deste documento. | <ul><li>URL: **Obrigatório** A URL de entrada com caracteres ASCII que você deseja decodificar em caracteres especiais.</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>://example.com/partneralliance_asia-pacific_2022 |

{style="table-layout:auto"}

### Funções de data e hora {#date-and-time}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela. Mais informações sobre a função `date` podem ser encontradas na seção de datas do [guia de manipulação de formato de dados](./data-handling.md#dates).

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Recupera a hora atual. | | now() | now() | `2021-10-26T10:10:24Z` |
| carimbo de data e hora | Recupera o horário Unix atual. | | timestamp() | timestamp() | 1571850624571 |
| formato | Formata a data de entrada de acordo com um formato especificado. | <ul><li>DATE: **Obrigatório** A data de entrada, como um objeto ZonedDateTime, que você deseja formatar.</li><li>FORMATO: **Obrigatório** O formato para o qual você deseja alterar a data.</li></ul> | format(DATA, FORMATO) | format(2019-10-23T11:24:00+00:00, &quot;`yyyy-MM-dd HH:mm:ss`&quot;) | `2019-10-23 11:24:35` |
| dformat | Converte um carimbo de data e hora em uma cadeia de caracteres de data de acordo com um formato especificado. | <ul><li>CARIMBO DE DATA/HORA: **Obrigatório** O carimbo de data/hora que você deseja formatar. Isso é gravado em milissegundos.</li><li>FORMATO: **Obrigatório** O formato em que você deseja que o carimbo de data/hora se torne.</li></ul> | dformat(CARIMBO DE DATA E HORA, FORMATO) | dformat(1571829875000, &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`&quot;) | `2019-10-23T11:24:35.000Z` |
| data | Converte uma string de data em um objeto ZonedDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A cadeia de caracteres que representa a data.</li><li>FORMATO: **Obrigatório** A cadeia de caracteres que representa o formato da data de origem.**Observação:** **não** representa o formato em que você deseja converter a cadeia de caracteres de data. </li><li>DEFAULT_DATE: **Obrigatório** A data padrão retornada, se a data fornecida for nula.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| data | Converte uma string de data em um objeto ZonedDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A cadeia de caracteres que representa a data.</li><li>FORMATO: **Obrigatório** A cadeia de caracteres que representa o formato da data de origem.**Observação:** **não** representa o formato em que você deseja converter a cadeia de caracteres de data. </li></ul> | date(DATA, FORMATO) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| data | Converte uma string de data em um objeto ZonedDateTime (formato ISO 8601). | <ul><li>DATA: **Obrigatório** A cadeia de caracteres que representa a data.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Recupera as partes da data. Os seguintes valores de componentes são compatíveis: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;w<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br> | <ul><li>COMPONENTE: **Obrigatório** Uma cadeia de caracteres que representa a parte da data. </li><li>DATE: **Obrigatório** A data, em um formato padrão.</li></ul> | date_part&#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;10-17-2019:55:12&quot;)) | 10 |
| set_date_part | Substitui um componente em uma determinada data. Os seguintes componentes foram aceitos: <br><br>&quot;year&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPONENTE: **Obrigatório** Uma cadeia de caracteres que representa a parte da data. </li><li>VALUE: **Required** O valor a ser definido para o componente em uma determinada data.</li><li>DATE: **Obrigatório** A data, em um formato padrão.</li></ul> | set_date_part&#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;04/2016/09T11:44:44Z&quot; |
| make_date_time | Cria uma data a partir de partes. Essa função também pode ser induzida usando make_timestamp. | <ul><li>ANO: **Obrigatório** O ano, gravado em quatro dígitos.</li><li>MÊS: **Obrigatório** O mês. Os valores permitidos são de 1 a 12.</li><li>DIA: **Obrigatório** O dia. Os valores permitidos são de 1 a 31.</li><li>HORA: **Necessário** A hora. Os valores permitidos são de 0 a 23.</li><li>MINUTO: **Necessário** O minuto. Os valores permitidos são de 0 a 59.</li><li>NANOSECOND: **Obrigatório** Os valores de nanossegundos. Os valores permitidos são de 0 a 99999999.</li><li>FUSO HORÁRIO: **Obrigatório** O fuso horário da data e hora.</li></ul> | make_date_time&#x200B;(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;América/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Converte uma data em qualquer fuso horário em uma data em UTC. | <ul><li>DATA: **Obrigatório** A data que você está tentando converter.</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Converte uma data de um fuso horário em outro. | <ul><li>DATA: **Obrigatório** A data que você está tentando converter.</li><li>ZONA: **Obrigatório** O fuso horário para o qual você está tentando converter a data.</li></ul> | zone_date_to_zone&#x200B;(DATA, ZONA) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Hierarquias - Objetos {#objects}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Verifica se um objeto está ou não vazio. | <ul><li>ENTRADA: **Obrigatório** O objeto que você está tentando verificar está vazio.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | Cria uma lista de objetos. | <ul><li>ENTRADA: **Obrigatório** Um agrupamento de pares de chaves e matrizes.</li></ul> | arrays_to_object(ENTRADA) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Cria um objeto com base nos pares de chave/valor simples fornecidos. | <ul><li>ENTRADA: **Obrigatório** Uma lista simples de pares de chave/valor.</li></ul> | to_object(ENTRADA) | to_object&#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Cria um objeto a partir da cadeia de caracteres de entrada. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres que está sendo analisada para criar um objeto.</li><li>VALUE_DELIMITER: *Opcional* O delimitador que separa um campo do valor. O delimitador padrão é `:`.</li><li>FIELD_DELIMITER: *Opcional* O delimitador que separa pares de valores de campo. O delimitador padrão é `,`.</li></ul> | str_to_object&#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Observação**: é possível usar a função `get()` juntamente com `str_to_object()` para recuperar valores para as chaves na cadeia de caracteres. | <ul><li>Exemplo #1: str_to_object(&quot;firstName - John ; lastName - ; - 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>Exemplo #2: str_to_object(&quot;firstName - John ; lastName - ; phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;).get(&quot;firstName&quot;)</li></ul> | <ul><li>Exemplo #1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Exemplo #2: &quot;John&quot;</li></ul> |
| contains_key | Verifica se o objeto existe nos dados de origem. **Observação:** esta função substitui a função `is_set()` obsoleta. | <ul><li>ENTRADA: **Obrigatório** O caminho a ser verificado se ele existir nos dados de origem.</li></ul> | contains_key(ENTRADA) | contains_key(&quot;evars.evar.field1&quot;) | true |
| nullify | Define o valor do atributo para `null`. Isso deve ser usado quando você não deseja copiar o campo para o schema de destino. | | nullify() | nullify() | `null` |
| get_keys | Analisa os pares chave/valor e retorna todas as chaves. | <ul><li>OBJETO: **Obrigatório** O objeto do qual as chaves serão extraídas.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Orgulho e Preconceito&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analisa os pares chave/valor e retorna o valor da string, com base na chave fornecida. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres que você deseja analisar.</li><li>KEY: **Obrigatório** A chave para a qual o valor deve ser extraído.</li><li>VALUE_DELIMITER: **Obrigatório** O delimitador que separa o campo e o valor. Se for fornecido um `null` ou uma cadeia de caracteres vazia, este valor será `:`.</li><li>FIELD_DELIMITER: *Opcional* O delimitador que separa pares de campo e valor. Se for fornecido um `null` ou uma cadeia de caracteres vazia, este valor será `,`.</li></ul> | get_values(STRING, CHAVE, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |
| map_get_values | Pega um mapa e uma entrada de chave. Se a entrada for uma única chave, a função retornará o valor associado a essa chave. Se a entrada for uma matriz de sequência, a função retornará todos os valores correspondentes às chaves fornecidas. Se o mapa de entrada tiver chaves duplicadas, o valor de retorno deverá desduplicar as chaves e retornar valores exclusivos. | <ul><li>MAPA: **Obrigatório** Os dados do mapa de entrada.</li><li>KEY: **Obrigatório** A chave pode ser uma única cadeia de caracteres ou uma matriz de cadeia de caracteres. Se qualquer outro tipo primitivo (dados / número) for fornecido, ele será tratado como uma string.</li></ul> | get_values(MAP, KEY) | Consulte o [apêndice](#map_get_values) para obter uma amostra de código. | |
| map_has_keys | Se uma ou mais chaves de entrada forem fornecidas, a função retornará true. Se uma matriz de string for fornecida como entrada, a função retornará true na primeira chave encontrada. | <ul><li>MAPA: **Obrigatório** Os dados do mapa de entrada</li><li>KEY: **Obrigatório** A chave pode ser uma única cadeia de caracteres ou uma matriz de cadeia de caracteres. Se qualquer outro tipo primitivo (dados / número) for fornecido, ele será tratado como uma string.</li></ul> | map_has_keys(MAP, KEY) | Consulte o [apêndice](#map_has_keys) para obter uma amostra de código. | |
| add_to_map | Aceita pelo menos duas entradas. Qualquer número de mapas pode ser fornecido como entrada. O Preparo de dados retorna um único mapa que tem todos os pares de valores-chave de todas as entradas. Se uma ou mais chaves forem repetidas (no mesmo mapa ou entre mapas), o Preparo de dados desduplica as chaves para que o primeiro par de valores-chave persista na ordem em que foram passadas na entrada. | MAPA: **Obrigatório** Os dados do mapa de entrada. | add_to_map(MAP 1, MAP 2, MAP 3, ...) | Consulte o [apêndice](#add_to_map) para obter uma amostra de código. | |
| object_to_map (Sintaxe 1) | Use esta função para criar tipos de dados de Mapa. | <ul><li>KEY: **Obrigatório** As chaves devem ser uma cadeia de caracteres. Se quaisquer outros valores primitivos, como números inteiros ou datas, forem fornecidos, eles serão convertidos automaticamente em cadeias de caracteres e serão tratados como cadeias de caracteres.</li><li>ANY_TYPE: **Obrigatório** Refere-se a qualquer tipo de dados XDM com suporte, exceto Mapas.</li></ul> | object_to_map(CHAVE, ANY_TYPE, CHAVE, ANY_TYPE, ... ) | Consulte o [apêndice](#object_to_map) para obter uma amostra de código. | |
| object_to_map (Sintaxe 2) | Use esta função para criar tipos de dados de Mapa. | <ul><li>OBJETO: **Obrigatório** Você pode fornecer um objeto de entrada ou uma matriz de objetos e apontar para um atributo dentro do objeto como chave.</li></ul> | object_to_map(OBJECT) | Consulte o [apêndice](#object_to_map) para obter uma amostra de código. |
| object_to_map (Sintaxe 3) | Use esta função para criar tipos de dados de Mapa. | <ul><li>OBJETO: **Obrigatório** Você pode fornecer um objeto de entrada ou uma matriz de objetos e apontar para um atributo dentro do objeto como chave.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | Consulte o [apêndice](#object_to_map) para obter uma amostra de código. |

{style="table-layout:auto"}

Para obter informações sobre o recurso de cópia de objeto, consulte a seção [abaixo](#object-copy).

### Hierarquias - Matrizes {#arrays}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalescência | Retorna o primeiro objeto não nulo em uma determinada matriz. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o primeiro objeto não nulo.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;primeiro&quot;, null, &quot;segundo&quot;) | &quot;first&quot; |
| primeiro | Recupera o primeiro elemento da matriz especificada. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o primeiro elemento.</li></ul> | first(ENTRADA) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| últimos | Recupera o último elemento da matriz especificada. | <ul><li>ENTRADA: **Obrigatório** A matriz da qual você deseja encontrar o último elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Adiciona elementos ao final da matriz. | <ul><li>ARRAY: **Obrigatório** A matriz à qual você está adicionando elementos.</li><li>VALORES: os elementos que você deseja anexar à matriz.</li></ul> | add_to_array&#x200B;(MATRIZ, VALORES) | add_to_array&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Combina os arrays entre si. | <ul><li>ARRAY: **Obrigatório** A matriz à qual você está adicionando elementos.</li><li>VALORES: a(s) matriz(es) que você deseja anexar à matriz principal.</li></ul> | join_arrays&#x200B;(MATRIZ, VALORES) | join_arrays&#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Pega uma lista de entradas e a converte em uma matriz. | <ul><li>INCLUDE_NULLS: **Obrigatório** Um valor booliano para indicar se os nulos devem ou não ser incluídos na matriz de resposta.</li><li>VALORES: **Obrigatório** Os elementos a serem convertidos em uma matriz.</li></ul> | to_array&#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Retorna o tamanho da entrada. | <ul><li>ENTRADA: **Obrigatório** O objeto do qual você está tentando encontrar o tamanho.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Esta função é usada para anexar todos os elementos na matriz de entrada inteira ao final da matriz no Perfil. Esta função é **somente** aplicável durante atualizações. Se usada no contexto de inserções, essa função retorna a entrada como está. | <ul><li>ARRAY: **Obrigatório** A matriz à qual anexar a matriz no Perfil.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | Esta função é usada para substituir elementos em uma matriz. Esta função é **somente** aplicável durante atualizações. Se usada no contexto de inserções, essa função retorna a entrada como está. | <ul><li>ARRAY: **Obrigatório** A matriz para substituir a matriz no Perfil.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |
| [!BADGE Somente destinos]{type=Informative} array_to_string | Une as representações de cadeia de caracteres dos elementos em uma matriz usando o separador especificado. Se a matriz for multidimensional, ela será nivelada antes de ser unida. **Observação**: esta função é usada em destinos. Leia a [documentação](../destinations/ui/export-arrays-maps-objects.md) para obter mais informações. | <ul><li>SEPARATOR: **Obrigatório** O separador usado para unir os elementos na matriz.</li><li>ARRAY: **Obrigatório** A matriz que será unida (após nivelamento).</li></ul> | array_to_string(SEPARADOR, MATRIZ) | `array_to_string(";", ["Hello", "world"])` | &quot;Olá;mundo&quot; |
| [!BADGE Somente destinos]{type=Informative} filterArray* | Filtra a matriz especificada com base em um predicado. **Observação**: esta função é usada em destinos. Leia a [documentação](../destinations/ui/export-arrays-maps-objects.md) para obter mais informações. | <ul><li>ARRAY: **Obrigatório** A matriz a ser filtrada</li><li>PREDICATE: **Obrigatório** O predicado a ser aplicado em cada elemento da matriz especificada. | filterArray(MATRIZ, PREDICADO) | `filterArray([5, -6, 0, 7], x -> x > 0)` | [5, 7] |
| [!BADGE Somente destinos]{type=Informative} transformArray* | Transforma a matriz especificada com base em um predicado. **Observação**: esta função é usada em destinos. Leia a [documentação](../destinations/ui/export-arrays-maps-objects.md) para obter mais informações. | <ul><li>ARRAY: **Obrigatório** A matriz a ser transformada.</li><li>PREDICATE: **Obrigatório** O predicado a ser aplicado em cada elemento da matriz especificada. | transformArray(MATRIZ, PREDICADO) | ` transformArray([5, 6, 7], x -> x + 1)` | [6, 7, 8] |
| [!BADGE Somente destinos]{type=Informative} flattenArray* | Nivela a matriz dada (multidimensional) para uma matriz unidimensional. **Observação**: esta função é usada em destinos. Leia a [documentação](../destinations/ui/export-arrays-maps-objects.md) para obter mais informações. | <ul><li>ARRAY: **Obrigatório** A matriz a ser nivelada.</li></ul> | flattenArray(MATRIZ) | flattenArray([[&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;, &#39;d&#39;]], [[&#39;e&#39;], [&#39;f&#39;]]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;, &#39;f&#39;] |

{style="table-layout:auto"}

### Hierarquias - Mapa {#map}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | Esta função pega uma matriz de objetos e uma chave como entrada e retorna um mapa do campo da chave com o valor como chave e o elemento da matriz como valor. | <ul><li>ENTRADA: **Obrigatório** A matriz de objetos da qual você deseja encontrar o primeiro objeto não nulo.</li><li>KEY: **Obrigatório** A chave deve ser um nome de campo na matriz de objetos e o objeto como valor.</li></ul> | array_to_map(OBJECT[] INPUTS, KEY) | Leia o [apêndice](#object_to_map) para obter uma amostra de código. |
| object_to_map | Essa função pega um objeto como argumento e retorna um mapa de pares de valores-chave. | <ul><li>ENTRADA: **Obrigatório** A matriz de objetos da qual você deseja encontrar o primeiro objeto não nulo.</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address) onde a entrada é &quot; + &quot;address: {line1 : \&quot;345 park ave\&quot;,line2: \&quot;bldg 2\&quot;,City : \&quot;san jose\&quot;,State : \&quot;CA\&quot;,type: \&quot;office\&quot;}&quot; | Retorna um mapa com determinado nome de campo e pares de valores ou nulo se a entrada for nula. Por exemplo: `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | Esta função pega uma lista de pares de valor-chave e retorna um mapa de pares de valor-chave. | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;, \&quot;John\&quot;, \&quot;lastName\&quot;, \&quot;Doe\&quot;)&quot; | Retorna um mapa com determinado nome de campo e pares de valores ou nulo se a entrada for nula. Por exemplo: `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### Operadores lógicos {#logical-operators}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decodificar | Dada uma chave e uma lista de pares de valores chave nivelados como uma matriz, a função retorna o valor se a chave for encontrada ou retorna um valor padrão se presente na matriz. | <ul><li>KEY: **Obrigatório** A chave a ser correspondida.</li><li>OPTIONS: **Obrigatório** Uma matriz nivelada de pares de chave/valor. Opcionalmente, um valor padrão pode ser colocado no final.</li></ul> | decode(CHAVE, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;Califórnia&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Se o stateCode fornecido for &quot;ca&quot;, &quot;California&quot;.<br>Se o stateCode fornecido for &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Se stateCode não corresponder ao seguinte, &quot;N/A&quot;. |
| iif | Avalia uma determinada expressão booleana e retorna o valor especificado com base no resultado. | <ul><li>EXPRESSION: **Required** A expressão booleana que está sendo avaliada.</li><li>TRUE_VALUE: **Obrigatório** O valor retornado se a expressão for avaliada como verdadeira.</li><li>FALSE_VALUE: **Obrigatório** O valor retornado se a expressão for avaliada como falsa.</li></ul> | iif(EXPRESSÃO, VALOR_VERDADEIRO, VALOR_FALSO) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### Agregação {#aggregation}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Retorna o mínimo dos argumentos fornecidos. Usa a ordenação natural. | <ul><li>OPTIONS: **Obrigatório** Um ou mais objetos que podem ser comparados entre si.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Retorna o máximo dos argumentos fornecidos. Usa a ordenação natural. | <ul><li>OPTIONS: **Obrigatório** Um ou mais objetos que podem ser comparados entre si.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Conversões de tipo {#type-conversions}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Converte uma cadeia de caracteres em um BigInteger. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres a ser convertida em um BigInteger.</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Converte uma cadeia de caracteres em um Duplo. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres a ser convertida em Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Converte uma cadeia de caracteres em um flutuante. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres a ser convertida em Float.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Converte uma string em um inteiro. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres a ser convertida em um inteiro.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### Funções JSON {#json}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Desserialize o conteúdo JSON da string fornecida. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres JSON a ser desserializada.</li></ul> | json_to_object&#x200B;(STRING) | `json_to_object&#x200B;({"info":{"firstName":"John","lastName": "Doe"}})` | Um objeto que representa o JSON. |

{style="table-layout:auto"}

### Operações especiais {#special-operations}

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Gera uma ID pseudo-aleatória. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | Essa função pega uma sequência de caracteres FPID e a converte em uma ECID para ser usada em aplicativos Adobe Experience Platform e Adobe Experience Cloud. | <ul><li>CADEIA DE CARACTERES: **Obrigatório** A cadeia de caracteres FPID a ser convertida em ECID.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### Funções do agente do usuário {#user-agent}

Qualquer uma das funções do agente do usuário contidas na tabela abaixo pode retornar um dos seguintes valores:

* Telefone - um dispositivo móvel com tela pequena (geralmente &lt; 7 pol)
* Dispositivo móvel - Um dispositivo móvel que ainda não foi identificado. Esse dispositivo móvel pode ser um eReader, um tablet, um telefone, um relógio etc.

Para obter mais informações sobre valores de campo de dispositivo, leia a [lista de valores de campo de dispositivo](#device-field-values) no apêndice deste documento.

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrai o nome do sistema operacional da sequência de agente do usuário. | <ul><li>USER_AGENT: **Necessário** A sequência de agente do usuário.</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrai a versão principal do sistema operacional da sequência de agente do usuário. | <ul><li>USER_AGENT: **Necessário** A sequência de agente do usuário.</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrai a versão do sistema operacional da sequência de agente do usuário. | <ul><li>USER_AGENT: **Necessário** A sequência de agente do usuário.</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrai o nome e a versão do sistema operacional da sequência de agente do usuário. | <ul><li>USER_AGENT: **Necessário** A sequência de agente do usuário.</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrai a versão do agente da sequência de agente do usuário. | <ul><li>USER_AGENT: **Necessário** A sequência de agente do usuário.</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extrai o nome do agente e a versão principal da sequência de agente do usuário. | <ul><li>USER_AGENT: **Necessário** A sequência de agente do usuário.</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrai o nome do agente da sequência de agente do usuário. | <ul><li>USER_AGENT: **Necessário** A sequência de agente do usuário.</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrai a classe de dispositivo da sequência de agente do usuário. | <ul><li>USER_AGENT: **Necessário** A sequência de agente do usuário.</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefone |

{style="table-layout:auto"}

### Funções do Analytics {#analytics}

>[!NOTE]
>
>Você só pode usar as seguintes funções de análise para fluxos do WebSDK e do Adobe Analytics.

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | Extrai a ID de evento de uma string de evento do Analytics. | <ul><li>EVENT_STRING: **Obrigatório** A cadeia de caracteres de evento do Analytics separada por vírgulas.</li><li>EVENT_NAME: **Obrigatório** O nome do evento do qual extrair e ID.</li></ul> | aa_get_event_id(EVENT_STRING, EVENT_NAME) | aa_get_event_id(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 123456 |
| aa_get_event_value | Extrai o valor de evento de uma string de evento do Analytics. Se o valor do evento não for especificado, 1 será retornado. | <ul><li>EVENT_STRING: **Obrigatório** A cadeia de caracteres de evento do Analytics separada por vírgulas.</li><li>EVENT_NAME: **Obrigatório** O nome do evento do qual extrair um valor.</li></ul> | aa_get_event_value(EVENT_STRING, EVENT_NAME) | aa_get_event_value(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 5 |
| aa_get_product_categories | Extrai a categoria de produto de uma string de produtos do Analytics. | <ul><li>PRODUCTS_STRING: **Obrigatório** A cadeia de caracteres de produtos do Analytics.</li></ul> | aa_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories(&quot;;Exemplo de produto 1;1;3.50,Exemplo de categoria 2;Exemplo de produto 2;1;5.99&quot;) | [null,&quot;Exemplo de categoria 2&quot;] |
| aa_get_product_names | Extrai o nome do produto de uma string de produtos do Analytics. | <ul><li>PRODUCTS_STRING: **Obrigatório** A cadeia de caracteres de produtos do Analytics.</li></ul> | aa_get_product_names(PRODUCTS_STRING) | aa_get_product_names(&quot;;Exemplo produto 1;1;3.50,Exemplo categoria 2;Exemplo produto 2;1;5.99&quot;) | [&quot;Exemplo de produto 1&quot;,&quot;Exemplo de produto 2&quot;] |
| aa_get_product_quantity | Extrai as quantidades de uma string de produtos do Analytics. | <ul><li>PRODUCTS_STRING: **Obrigatório** A cadeia de caracteres de produtos do Analytics.</li></ul> | aa_get_product_quantity(PRODUCTS_STRING) | aa_get_product_quantity(&quot;;Exemplo produto 1;1;3.50,Exemplo categoria 2;Exemplo produto 2&quot;) | [&quot;1&quot;, nulo] |
| aa_get_product_price | Extrai o preço de uma string de produtos do Analytics. | <ul><li>PRODUCTS_STRING: **Obrigatório** A cadeia de caracteres de produtos do Analytics.</li></ul> | aa_get_product_price(PRODUCTS_STRING) | aa_get_product_price(&quot;;Exemplo produto 1;1;3.50,Exemplo categoria 2;Exemplo produto 2&quot;) | [&quot;3.50&quot;, nulo] |
| aa_get_product_event_values | Extrai valores para o evento nomeado da string de produtos como uma matriz de strings. | <ul><li>PRODUCTS_STRING: **Obrigatório** A cadeia de caracteres de produtos do Analytics.</li><li>EVENT_NAME: **Obrigatório** O nome do evento do qual extrair valores.</li></ul> | aa_get_product_event_values(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_values(&quot;;Exemplo produto 1;1;4.20;event1=2.3\|event2=5:1,;Exemplo produto 2;1;4.20;event1=3\|event2=2:2&quot;, &quot;event1&quot;) | [&quot;2.3&quot;, &quot;3&quot;] |
| aa_get_product_evars | Extrai os valores de evar do evento nomeado da string de produtos como uma matriz de strings. | <ul><li>PRODUCTS_STRING: **Obrigatório** A cadeia de caracteres de produtos do Analytics.</li><li>EVAR_NAME: **Obrigatório** O nome do eVar a ser extraído.</li></ul> | aa_get_product_evars(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_evars(&quot;;Exemplo de produto;1;6.69;;eVar1=valor de merchandising&quot;, &quot;eVar1&quot;) | [&quot;Valor de merchandising&quot;] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### Cópia do objeto {#object-copy}

>[!TIP]
>
>O recurso de cópia de objeto é aplicado automaticamente quando um objeto na origem é mapeado para um objeto no XDM. Nenhuma ação adicional necessária por parte dos usuários.

Você pode usar o recurso de cópia de objeto para copiar atributos automaticamente de um objeto sem fazer alterações no mapeamento. Por exemplo, se os dados de origem tiverem uma estrutura de:

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

e uma estrutura XDM de:

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

Em seguida, o mapeamento se torna:

```json
address -> addr
address.line1 -> addr.addrLine1
```

No exemplo acima, os atributos `city` e `state` também são assimilados automaticamente em tempo de execução porque o objeto `address` está mapeado para `addr`. Se você tiver que criar um atributo `line2` na estrutura XDM e seus dados de entrada também contiverem um `line2` no objeto `address`, ele também será assimilado automaticamente, sem a necessidade de alterar manualmente o mapeamento.

Para garantir que o mapeamento automático funcione, os seguintes pré-requisitos devem ser atendidos:

* Objetos de nível primário devem ser mapeados;
* Novos atributos devem ter sido criados no esquema XDM;
* Os novos atributos devem ter nomes correspondentes no esquema de origem e no esquema XDM.

Se qualquer um dos pré-requisitos não for atendido, você deverá mapear manualmente o esquema de origem para o esquema XDM usando o preparo de dados.

## Apêndice

Veja a seguir informações adicionais sobre o uso das funções de mapeamento do Preparo de dados

### Caracteres especiais {#special-characters}

A tabela abaixo descreve uma lista de caracteres reservados e seus caracteres codificados correspondentes.

| Caractere reservado | Caractere codificado |
| --- | --- |
| espaço | %20 |
| ! | %21 |
| &quot; | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| &#39; | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| : | %3A |
| ; | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| ` | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### Valores do campo Dispositivo {#device-field-values}

A tabela abaixo descreve uma lista de valores de campo de dispositivo e suas descrições correspondentes.

| Dispositivo | Descrição |
| --- | --- |
| Desktop | Um tipo de dispositivo Desktop ou Laptop. |
| Anônimo | Um dispositivo anônimo. Em alguns casos, são `useragents` que foram alterados por um software de anonimização. |
| Desconhecido | Um dispositivo desconhecido. Normalmente, são `useragents` que não contêm informações sobre o dispositivo. |
| Dispositivo móvel | Um dispositivo móvel que ainda não foi identificado. Esse dispositivo móvel pode ser um eReader, um tablet, um telefone, um relógio etc. |
| Tablet | Um dispositivo móvel com tela grande (geralmente > 7 pol). |
| Telefone | Um dispositivo móvel com tela pequena (geralmente &lt; 7 pol). |
| Observar | Um dispositivo móvel com uma tela pequena (geralmente &lt; 2 pol). Esses dispositivos normalmente funcionam como uma tela adicional para um dispositivo do tipo telefone/tablet. |
| Realidade aumentada | Um dispositivo móvel com recursos de AR. |
| Realidade virtual | Um dispositivo móvel com recursos VR. |
| eReader | Um dispositivo semelhante a um tablet, mas geralmente com uma tela [!DNL eInk]. |
| Decodificador de sinais | Um dispositivo conectado que permite a interação através de uma tela dimensionada para TV. |
| TV | Um dispositivo semelhante ao decodificador de sinais, mas integrado à TV. |
| Equipamento doméstico | Um aparelho doméstico (geralmente grande), como uma geladeira. |
| Console de jogos | Um sistema de jogos fixo como o [!DNL Playstation] ou o [!DNL XBox]. |
| Console de jogos portátil | Um sistema móvel de jogos como o [!DNL Nintendo Switch]. |
| Voz | Um dispositivo orientado por voz, como um [!DNL Amazon Alexa] ou um [!DNL Google Home]. |
| Carro | Um navegador baseado em veículo. |
| Robô | Robôs que visitam um site. |
| Robot Mobile | Robôs que visitam um site, mas indicam que desejam ser vistos como um visitante móvel. |
| Robot Imitator | Robôs que visitam um site, fingindo que são robôs como [!DNL Google], mas não são. **Observação**: na maioria dos casos, os Robot Imitators são realmente robôs. |
| Nuvem | Um aplicativo baseado em nuvem. Eles não são robôs nem hackers, mas são aplicativos que precisam se conectar. Isso inclui [!DNL Mastodon] servidores. |
| Hacker | Este valor de dispositivo é usado caso scripts sejam detectados na cadeia de caracteres `useragent`. |

{style="table-layout:auto"}

### Amostras de código {#code-samples}

#### map_get_values {#map-get-values}

+++Selecione para exibir o exemplo

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++Selecione para exibir o exemplo

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++Selecione para exibir o exemplo

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++

#### object_to_map {#object_to_map}

**Sintaxe 1**

+++Selecione para exibir o exemplo

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**Sintaxe 2**

+++Selecione para exibir o exemplo

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**Sintaxe 3**

+++Selecione para exibir o exemplo

```json
example = "object_to_map(addresses,type)" +
        "\n" +
        "[\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "]" ,
result = "{\n" +
        "    \"home\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    \"work\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    \"office\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "}" 
```

+++

#### array_to_map {#array_to_map}

+++Selecione para exibir o exemplo

```json
example = "array_to_map(addresses, \"type\") where addresses is\n" +
  "\n" +
  "[\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "]" ,
result = "{\n" +
  "    \"home\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    \"work\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    \"office\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "}",
returns = "Returns a map with given field name and value pairs or null if input is null"
```

+++

