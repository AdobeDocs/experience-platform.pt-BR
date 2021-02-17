---
keywords: Experience Platform;home;popular topics;schema;Schema;mixin;Mixin;Mixins;mixins;tipo de dados;tipos de dados;Tipo de dados;Tipo de dados;Tipo de dados;Tipo de dados;Tipo de dados;Tipo de dados;Tipo de dados;schemas;Design do Schema;mapa;Mapa;schema;home;popular topics;;known topics;datatype;data type;Data type;;Schemas;design;map;Map;Map;
solution: Experience Platform
title: Restrições de Tipo de Campo XDM
topic: overview
description: Uma referência para restrições de tipo de campo no Experience Data Model (XDM), incluindo os outros formatos de serialização para os quais eles podem ser mapeados e como definir seus próprios tipos de campo na API.
translation-type: tm+mt
source-git-commit: c9ea7471bb18c92443a5e45c14c8505ef3ccf30d
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 3%

---


# Restrições de tipo de campo XDM

Em schemas do Experience Data Model (XDM), o tipo de campo restringe o tipo de dados que o campo pode conter. Este documento fornece uma visão geral de cada tipo de campo principal, incluindo os outros formatos de serialização para os quais eles podem ser mapeados e como definir seus próprios tipos de campo na API para impor restrições diferentes.

## Introdução

Antes de usar este guia, reveja as [noções básicas da composição do schema](./composition.md) para obter uma introdução aos schemas, classes e misturas XDM.

Se você planeja definir seus próprios tipos de campo na API, é altamente recomendável que você faça o start do [guia do desenvolvedor do Registro do Schema](../api/getting-started.md) para saber como criar combinações e tipos de dados para incluir seus campos personalizados. Se você estiver usando a interface do Experience Platform para criar schemas, consulte o guia em [definindo campos na interface do usuário](../ui/fields/overview.md) para saber como implementar restrições em campos que você define em combinações personalizadas e tipos de dados.

## Estrutura de base e exemplos

O XDM é construído sobre o Schema JSON e, portanto, os campos XDM herdam uma sintaxe semelhante ao definir seu tipo. Entender como diferentes tipos de campo são representados no Schema JSON pode ajudar a indicar as restrições básicas de cada tipo.

>[!NOTE]
>
>Consulte o [Guia de fundamentos da API](../../landing/api-fundamentals.md#json-schema) para obter mais informações sobre o Schema JSON e outras tecnologias subjacentes em APIs de plataforma.

A tabela a seguir descreve como cada tipo XDM é representado no Schema JSON, juntamente com um exemplo de valor que está em conformidade com o tipo:

<table>
  <thead>
    <tr>
      <th>Tipo XDM</th>
      <th>Schema JSON</th>
      <th>Exemplo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!String UICONTROL]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!Duplo UICONTROL]</td>
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
{
  "Tipo": "integer",
  "Máximo": 9007199254740991,
  "mínimo": -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "Tipo": "integer",
  "Máximo": 2147483648
  "mínimo": -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "Tipo": "integer",
  "Máximo": 32768
  "mínimo": -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!Byte UICONTROL]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "Tipo": "integer",
  "Máximo": 128
  "mínimo": -128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!Data UICONTROL]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "Tipo": "string",
  "format": "date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "Tipo": "string",
  "format": "date-time"
}</pre>
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

**Todas as strings formatadas por data devem estar em conformidade com o padrão ISO 8601 ([RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mapeamento de tipos XDM para outros formatos

As seções abaixo descrevem como cada tipo XDM mapeia para outros formatos de serialização comuns:

* [Parquet, Spark SQL e Java](#parquet)
* [Scala, .NET e CosmosDB](#scala)
* [MongoDB, Aerospike e Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Entre os tipos XDM padrão listados nas tabelas abaixo, o tipo [!UICONTROL Mapa] também é incluído. Os mapas são usados em schemas padrão quando os dados são representados como chaves que mapeiam para determinados valores, ou quando as chaves não podem ser incluídas em um schema estático e devem ser tratadas como valores de dados.
>
>Campos tipo mapa são reservados para uso do setor e do schema do fornecedor e, portanto, não podem ser usados em recursos personalizados que você define. A inclusão do tipo de mapa nas tabelas abaixo destina-se apenas a ajudar você a determinar como mapear seus dados existentes para XDM se eles estiverem armazenados atualmente em qualquer um dos formatos listados abaixo.

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
| [!UICONTROL Mapa] | `MAP`-grupo<br><br> anotado(`<key-type>` deve ser  `STRING`) | `MapType`<br><br>(`keyType` deve ser  `StringType`) | `java.util.Map` |

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

### MongoDB, Aerospike e Protobuf 2 {#mongo}

| Tipo XDM | MongoDB | Aerospie | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Duplo] | `double` | `Double` | `double` |
| [!UICONTROL Longo] | `long` | `Integer` | `int64` |
| [!UICONTROL Número inteiro] | `int` | `Integer` | `int32` |
| [!UICONTROL Curto] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Data] | `date` | `Integer`<br>(milissegundos do Unix) | `int64`<br>(milissegundos do Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(milissegundos do Unix) | `int64`<br>(milissegundos do Unix) |
| [!UICONTROL Booleano] | `bool` | `Integer`<br>(0/1 binário) | `bool` |
| [!UICONTROL Mapa] | `object` | `map` | `map<key_type, value_type>` |

## Definição de tipos de campos XDM na API {#define-fields}

Todos os campos XDM são definidos usando as restrições padrão [JSON Schema](https://json-schema.org/) que se aplicam ao tipo de campo, com restrições adicionais para nomes de campo que são impostas por [!DNL Experience Platform]. A API do Registro de Schemas permite que você defina tipos de campos adicionais usando formatos e restrições opcionais. Os tipos de campos XDM são expostos pelo atributo de nível de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` é um valor gerado pelo sistema e, portanto, não é necessário adicionar essa propriedade ao JSON para seu campo ao usar a API. A prática recomendada é usar os tipos de Schemas JSON (como `string` e `integer`) com as restrições mínimas/máximas apropriadas, conforme definido na tabela abaixo.

A tabela a seguir descreve a formatação apropriada para definir tipos de campos diferentes, incluindo aqueles com propriedades opcionais. Mais informações sobre propriedades opcionais e palavras-chave específicas do tipo estão disponíveis na [documentação do Schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para começar, localize o tipo de campo desejado e use o código de amostra fornecido para criar sua solicitação de API para [criar uma mistura](../api/mixins.md#create) ou [criar um tipo de dados](../api/data-types.md#create).

<table>
  <tr>
    <th>Tipo XDM</th>
    <th>Propriedades opcionais</th>
    <th>Exemplo</th>
  </tr>
  <tr>
    <td>[!String UICONTROL]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
    "Tipo": "string",
    "padrão": "^[A-Z]{2}$",
    "maxLength": 2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "string",
  "format": "uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>Valores de enumeração restritos são fornecidos sob a matriz <code>enum</code>, enquanto rótulos opcionais voltados para o cliente para cada valor podem ser fornecidos em <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Valor 1",
      "value2": "Valor 2",
      "value3": "Valor 3"
  },
  "padrão": "value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "número"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "integer",
  "mínimo": -9007199254740992,
  "Máximo": 9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "integer",
  "mínimo": -2147483648,
  "Máximo": 2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "integer",
  "mínimo": -32768
  "Máximo": 32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!Byte UICONTROL]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "integer",
  "mínimo": -128,
  "Máximo": 128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Boolean]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "booleano",
  "padrão": false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Date]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "string",
  "format": "date",
  "Exemplos": ["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "string",
  "format": "date-time",
  "Exemplos": ["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Uma matriz de tipos escalares básicos (por exemplo, strings):
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "array",
  "Itens": {
    "Tipo": "string"
  }
}</pre>
      Uma matriz de objetos definidos por outro schema:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "array",
  "Itens": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Object]</td>
    <td></td>
    <td>O atributo <code>type</code> de cada subcampo definido em <code>properties</code> pode ser definido usando qualquer tipo escalar:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "object",
  "Propriedades": {
    "field1": {
      "Tipo": "string"
    },
    "field2": {
      "Tipo": "número"
    }
  }
}</pre>
      Os campos do tipo de objeto podem ser definidos referenciando <code>$id</code> de um tipo de dados:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "object",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Um mapa <strong>não deve</strong> definir quaisquer propriedades. Ele <strong>deve</strong> definir um único schema <code>additionalProperties</code> para descrever o tipo de valores contidos no mapa (cada mapa só pode conter um único tipo de dados). Os valores podem ser qualquer atributo XDM <code>type</code> válido ou uma referência a outro schema usando um atributo <code>$ref</code>.<br/><br/>Um campo de mapa com valores do tipo string:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "object",
  "additionalProperties":{
    "Tipo": "string"
  }
}</pre>
    Um campo de mapa com matrizes de sequências de caracteres para valores:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "object",
  "additionalProperties":{
    "Tipo": "array",
    "Itens": {
      "Tipo": "string"
    }
  }
}</pre>
    Um campo de mapa que faz referência a outro tipo de dados:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "Tipo": "object",
  "additionalProperties":{
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
