---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;grupo de campos;Grupo de campos;Grupos de campos;grupos de campos;tipo de dados;tipos de dados;Tipos de dados;tipo de dados;design de esquema;tipo de dados;tipo de dados;Tipo de dados;esquemas;Esquemas;Design de esquema;mapa;Mapa;
solution: Experience Platform
title: Restrições de tipo de campo XDM
description: Uma referência para restrições de tipo de campo no Experience Data Model (XDM), incluindo os outros formatos de serialização aos quais eles podem ser mapeados e como definir seus próprios tipos de campo na API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 8ddedb5ff8c12b05cdf39fa8dc2b59258389e522
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# Restrições de tipo de campo XDM

Em esquemas do Experience Data Model (XDM), o tipo de um campo restringe o tipo de dados que o campo pode conter. Este documento fornece uma visão geral de cada tipo de campo principal, incluindo os outros formatos de serialização aos quais eles podem ser mapeados e como definir seus próprios tipos de campo na API para aplicar restrições diferentes.

## Introdução

Antes de usar este guia, revise as [noções básicas da composição de esquema](./composition.md) para obter uma introdução aos esquemas XDM, classes e grupos de campos de esquema.

Se você planeja definir seus próprios tipos de campo na API, é altamente recomendável começar com o [guia do desenvolvedor do Registro de Esquema](../api/getting-started.md) para saber como criar grupos de campos e tipos de dados para incluir seus campos personalizados no. Se você estiver usando a interface do Experience Platform para criar seus esquemas, consulte o manual em [definindo campos na interface](../ui/fields/overview.md) para saber como implementar restrições em campos definidos em grupos de campos personalizados e tipos de dados.

## Estrutura básica e exemplos {#basic-types}

O XDM é criado sobre o Esquema JSON e, portanto, os campos XDM herdam uma sintaxe semelhante ao definir seu tipo. Entender como os diferentes tipos de campo são representados no Esquema JSON pode ajudar a indicar as restrições básicas de cada tipo. Os nomes de campos personalizados não diferenciam maiúsculas de minúsculas e devem ter nomes diferentes no mesmo nível no esquema.

>[!NOTE]
>
>Consulte o [guia de fundamentos de API](../../landing/api-fundamentals.md#json-schema) para obter mais informações sobre o Esquema JSON e outras tecnologias subjacentes nas APIs do Experience Platform.

A tabela a seguir descreve como cada tipo de XDM é representado no Esquema JSON, juntamente com um valor de exemplo que está em conformidade com o tipo:

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>Tipo XDM</th>
      <th>Esquema JSON</th>
      <th>Exemplo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Number]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 9007199254740991,
  "mínimo": -9007199254740991
&rbrace;</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "máximo": 2147483648,
  "minimum": -2147483648
&rbrace;</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 32767,
  "minimum": -32768
&rbrace;</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 128,
  "minimum": -128
&rbrace;</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "string",
  "format": "date"
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "string",
  "format": "date-time"
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "boolean"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Todas as cadeias de caracteres formatadas por data devem estar em conformidade com o padrão ISO 8601 ([RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mapeamento tipos XDM para outros formatos

As seções abaixo descrevem como cada tipo de XDM é mapeado para outros formatos de serialização comuns:

* [Parquet, Spark SQL e Java](#parquet)
* [Scala, .NET e CosmosDB](#scala)
* [MongoDB, Aerospike e Protobuf 2](#mongo)

>[!NOTE]
>
>Entre os tipos XDM padrão listados nas tabelas abaixo, o tipo [!UICONTROL Map] também é incluído. Os mapas são usados em esquemas padrão quando os dados são representados como chaves que mapeiam para determinados valores ou quando as chaves não podem ser incluídas razoavelmente em um esquema estático e devem ser tratadas como valores de dados.
>
>Muitos componentes XDM padrão usam tipos de mapa, e você também pode [definir campos de mapa personalizados](../tutorials/custom-fields-api.md#custom-maps), se desejar. A inclusão do tipo de mapa nas tabelas abaixo tem como objetivo ajudar você a determinar como mapear os dados existentes para o XDM se eles estiverem armazenados em qualquer um dos formatos listados abaixo.

### Parquet, Spark SQL e Java {#parquet}

| Tipo XDM | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Tipo: `BYTE_ARRAY`<br>Anotação: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Number] | Tipo: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Tipo: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Tipo: `INT32`<br>Anotação: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | Tipo: `INT32`<br>Anotação: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Tipo: `INT32`<br>Anotação: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Tipo: `INT32`<br>Anotação: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Tipo: `INT64`<br>Anotação: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | Tipo: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | Grupo `MAP` anotado<br><br>(`<key-type>` deve ser `STRING`) | `MapType`<br><br>(`keyType` deve ser `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala, .NET e CosmosDB {#scala}

| Tipo XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Number] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (N/D) | `object` |

{style="table-layout:auto"}

### MongoDB, Aerospike e Protobuf 2 {#mongo}

| Tipo XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Number] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(Unix milissegundos) | `int64`<br>(Unix milissegundos) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix milissegundos) | `int64`<br>(Unix milissegundos) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>(0/1 binário) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## Definição de tipos de campo XDM na API {#define-fields}

A API do Registro de esquema permite definir campos personalizados por meio do uso de formatos e restrições opcionais. Consulte o manual sobre [definição de campos personalizados na API do Registro de Esquema](../tutorials/custom-fields-api.md) para obter mais informações.
