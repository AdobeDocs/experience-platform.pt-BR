---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, grupo de campos, grupo de campos, grupos de campos, grupos de campos, tipo de dados, tipos de dados, tipo de dados, design de esquema, tipo de dados, tipo de dados, tipo de dados, tipo de dados, esquemas, esquemas, design de esquema, mapa, mapa;
solution: Experience Platform
title: Restrições de Tipo de Campo XDM
topic-legacy: overview
description: Uma referência para restrições de tipo de campo no Experience Data Model (XDM), incluindo os outros formatos de serialização para os quais podem ser mapeados e como definir seus próprios tipos de campo na API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 6%

---

# Restrições do tipo de campo XDM

Nos esquemas do Experience Data Model (XDM), o tipo de campo restringe o tipo de dados que o campo pode conter. Este documento fornece uma visão geral de cada tipo de campo principal, incluindo os outros formatos de serialização para os quais podem ser mapeados e como definir seus próprios tipos de campo na API para impor restrições diferentes.

## Introdução

Antes de usar este guia, reveja o [noções básicas da composição do schema](./composition.md) para obter uma introdução a esquemas, classes e grupos de campos do esquema XDM.

Se você planeja definir seus próprios tipos de campo na API, é altamente recomendável começar com a variável [Guia do desenvolvedor do Registro de Schema](../api/getting-started.md) para saber como criar grupos de campos e tipos de dados para incluir campos personalizados no. Se você estiver usando a interface do usuário do Experience Platform para criar seus esquemas, consulte o guia em [definição de campos na interface do usuário](../ui/fields/overview.md) para saber como implementar restrições em campos definidos em grupos de campos e tipos de dados personalizados.

## Estrutura básica e exemplos {#basic-types}

O XDM é criado sobre o Esquema JSON e, portanto, os campos XDM herdam uma sintaxe semelhante ao definir seu tipo. Entender como diferentes tipos de campo são representados no Esquema JSON pode ajudar a indicar as restrições básicas de cada tipo.

>[!NOTE]
>
>Consulte a [Guia de fundamentos da API](../../landing/api-fundamentals.md#json-schema) para obter mais informações sobre o Esquema JSON e outras tecnologias subjacentes nas APIs da plataforma.

A tabela a seguir descreve como cada tipo de XDM é representado no Esquema JSON, juntamente com um exemplo de valor que está em conformidade com o tipo :

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
      <td>[!UICONTROL Duplo]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "número"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Longo]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 9007199254740991, "mínimo": -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Número inteiro]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 2147483648, "mínimo": -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Curto]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 32768, "mínimo": -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 128, "mínimo": -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Data]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date-time" }</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Todas as strings formatadas na data devem estar em conformidade com o padrão ISO 8601 ([RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mapeamento de tipos XDM para outros formatos

As seções abaixo descrevem como cada tipo XDM mapeia para outros formatos de serialização comuns:

* [Parquet, Spark SQL e Java](#parquet)
* [Scala, .NET e CosmosDB](#scala)
* [MongoDB, Aerospike e Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Entre os tipos XDM padrão listados nas tabelas abaixo, a variável [!UICONTROL Mapa] também está incluído. Os mapas são usados em esquemas padrão quando os dados são representados como chaves que mapeiam para determinados valores ou quando as chaves não podem razoavelmente ser incluídas em um schema estático e devem ser tratadas como valores de dados.
>
>Os campos do tipo mapa são reservados para uso do setor e do schema do fornecedor e, portanto, não podem ser usados em recursos personalizados definidos por você. A inclusão do tipo de mapa nas tabelas abaixo destina-se apenas a ajudar você a determinar como mapear os dados existentes para XDM se eles estiverem armazenados atualmente em qualquer um dos formatos listados abaixo.

### Parquet, Spark SQL e Java {#parquet}

| Tipo XDM | Parquet | SQL Spark | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Tipo: `BYTE_ARRAY`<br>Anotação: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Duplo] | Tipo: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Longo] | Tipo: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Número inteiro] | Tipo: `INT32`<br>Anotação: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Curto] | Tipo: `INT32`<br>Anotação: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Tipo: `INT32`<br>Anotação: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Data] | Tipo: `INT32`<br>Anotação: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Tipo: `INT64`<br>Anotação: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Booleano] | Tipo: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Mapa] | `MAP`-grupo anotado<br><br>(`<key-type>` deve ser `STRING`) | `MapType`<br><br>(`keyType` deve ser `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET e CosmosDB {#scala}

| Tipo XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Duplo] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Longo] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Número inteiro] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Curto] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Data] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Booleano] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Mapa] | `Map` | (N/D) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike e Protobuf 2 {#mongo}

| Tipo XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Duplo] | `double` | `Double` | `double` |
| [!UICONTROL Longo] | `long` | `Integer` | `int64` |
| [!UICONTROL Número inteiro] | `int` | `Integer` | `int32` |
| [!UICONTROL Curto] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Data] | `date` | `Integer`<br>(Milissegundos do Unix) | `int64`<br>(Milissegundos do Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Milissegundos do Unix) | `int64`<br>(Milissegundos do Unix) |
| [!UICONTROL Booleano] | `bool` | `Integer`<br>(0/1 binário) | `bool` |
| [!UICONTROL Mapa] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Definição de tipos de campo XDM na API {#define-fields}

A API de Registro de Esquema permite definir campos personalizados usando formatos e restrições opcionais. Consulte o guia sobre [definição de campos personalizados na API do Registro de esquema](../tutorials/custom-fields-api.md) para obter mais informações.
