---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, grupo de campos, grupo de campos, grupos de campos, grupos de campos, tipo de dados, tipos de dados, tipo de dados, design de esquema, tipo de dados, tipo de dados, tipo de dados, tipo de dados, esquemas, esquemas, design de esquema, mapa, mapa;
solution: Experience Platform
title: Restrições de Tipo de Campo XDM
topic-legacy: overview
description: Uma referência para restrições de tipo de campo no Experience Data Model (XDM), incluindo os outros formatos de serialização para os quais podem ser mapeados e como definir seus próprios tipos de campo na API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 684237122e7384f6c611e1c602c30af2518aba58
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 3%

---

# Restrições do tipo de campo XDM

Nos esquemas do Experience Data Model (XDM), o tipo de campo restringe o tipo de dados que o campo pode conter. Este documento fornece uma visão geral de cada tipo de campo principal, incluindo os outros formatos de serialização para os quais podem ser mapeados e como definir seus próprios tipos de campo na API para impor restrições diferentes.

## Introdução

Antes de usar este guia, reveja o [noções básicas da composição do schema](./composition.md) para obter uma introdução a esquemas, classes e grupos de campos do esquema XDM.

Se você planeja definir seus próprios tipos de campo na API, é altamente recomendável começar com a variável [Guia do desenvolvedor do Registro de Schema](../api/getting-started.md) para saber como criar grupos de campos e tipos de dados para incluir campos personalizados no. Se você estiver usando a interface do usuário do Experience Platform para criar seus esquemas, consulte o guia em [definição de campos na interface do usuário](../ui/fields/overview.md) para saber como implementar restrições em campos definidos em grupos de campos e tipos de dados personalizados.

## Estrutura básica e exemplos

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

Todos os campos XDM são definidos usando o padrão [Esquema JSON](https://json-schema.org/) restrições que se aplicam ao tipo de campo, com restrições adicionais para nomes de campo que são aplicadas por [!DNL Experience Platform]. A API de Registro de Esquema permite definir tipos de campo adicionais por meio do uso de formatos e restrições opcionais. Os tipos de campo XDM são expostos pelo atributo de nível de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` é um valor gerado pelo sistema e, portanto, você não é obrigado a adicionar essa propriedade ao JSON do seu campo ao usar a API. A prática recomendada é usar tipos de Esquema JSON (como `string` e `integer`) com as restrições mínimas/máximas apropriadas, conforme definido na tabela abaixo.

A tabela a seguir descreve a formatação apropriada para definir tipos de campos diferentes, incluindo aqueles com propriedades opcionais. Mais informações sobre propriedades opcionais e palavras-chave específicas do tipo estão disponíveis no [Documentação do Esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para começar, encontre o tipo de campo desejado e use o código de amostra fornecido para criar sua solicitação de API para [criação de um grupo de campos](../api/field-groups.md#create) ou [criação de um tipo de dados](../api/data-types.md#create).

<table style="table-layout:auto">
  <tr>
    <th>Tipo XDM</th>
    <th>Propriedades opcionais</th>
    <th>Exemplo</th>
  </tr>
  <tr>
    <td>[!UICONTROL String]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "uri" }</pre>
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
    <td>Os valores de enum restritos são fornecidos sob a variável <code>enum</code> , enquanto etiquetas opcionais voltadas para o cliente para cada valor podem ser fornecidas em <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Valor 1", "valor 2": "Value 2", "value3": "Value 3" }, "default": "value1" }</pre>
    <br>Observe que a variável <code>meta:enum</code> valor faz <strong>not</strong> declare uma enumeração ou direcione qualquer validação de dados sozinha. Na maioria dos casos, as cadeias de caracteres fornecidas em <code>meta:enum</code> são igualmente fornecidas nos termos do <code>enum</code> para garantir que os dados sejam restritos. No entanto, existem alguns casos de uso em que <code>meta:enum</code> é fornecido sem um <code>enum</code> matriz. Veja o tutorial em <a href="../tutorials/extend-soft-enum.md">extensão de enumerações suaves</a> para obter mais informações.
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Número]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "number" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Longo]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "Minimum": -9007199254740992, "máximo": 9007199254740992 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Número inteiro]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "Minimum": -2147483648, "máximo": 2147483648 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Curto]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "Minimum": -32768, "máximo": 32768 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "Minimum": -128, "máximo": 128 }</pre>
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
"sampleField": { "type": "booleano", "padrão": false }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Data]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date", "example": ["2004-10-23"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date-time", "example": ["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Uma matriz de tipos escalares básicos (por exemplo, strings):
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "type": "string" }</pre>
      Uma matriz de objetos definidos por outro schema:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "$ref": "https://ns.adobe.com/xdm/data/paymentitem" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Objeto]</td>
    <td></td>
    <td>O <code>type</code> atributo de cada subcampo definido em <code>properties</code> pode ser definido usando qualquer tipo escalar:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" }</pre>
      Os campos do tipo objeto podem ser definidos fazendo referência à variável <code>$id</code> de um tipo de dados:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Um mapa <strong>não deve</strong> defina quaisquer propriedades. It <strong>must</strong> defina uma <code>additionalProperties</code> para descrever o tipo de valores contidos no mapa (cada mapa só pode conter um único tipo de dados). Os valores podem ser qualquer XDM válido <code>type</code> ou uma referência a outro schema usando um <code>$ref</code> atributo.<br/><br/>Um campo de mapa com valores do tipo string:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "type": "string" }</pre>
    Um campo de mapa com matrizes de sequências para valores:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "type": "array", "items": { "type": "string" } }</pre>
    Um campo de mapa que faz referência a outro tipo de dados:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "$ref": "https://ns.adobe.com/xdm/data/paymentitem" }</pre>
    </td>
  </tr>
</table>
