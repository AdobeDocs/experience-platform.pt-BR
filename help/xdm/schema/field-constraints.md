---
keywords: Experience Platform;home;popular topics;schema;Schema;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;schema design;datatype;Datatype;data type;Data type;schemas;Schemas;Schema design;map;Map;
solution: Experience Platform
title: Restrições de tipo de campo XDM
topic: overview
description: Uma referência para restrições de tipo de campo XDM, incluindo outros formatos de serialização para os quais podem ser mapeados e como definir seus próprios tipos de campo na API.
translation-type: tm+mt
source-git-commit: e92294b9dcea37ae2a4a398c9d3397dcf5aa9b9e
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 6%

---


# Restrições de tipo de campo XDM

Os tipos de campo XDM selecionados para seus schemas restringem quais tipos de dados esses campos podem conter. Este documento fornece uma visão geral de cada tipo de campo principal, incluindo os outros formatos de serialização para os quais eles podem ser mapeados e como definir seus próprios tipos de campo na API para impor restrições diferentes.

## Introdução

Antes de usar este guia, reveja as [noções básicas da composição](./composition.md) do schema para obter uma introdução aos schemas, classes e combinações XDM.

Se você planeja definir seus próprios tipos de campo, é altamente recomendável que você start o guia [do desenvolvedor do Registro de](../api/getting-started.md) Schemas para saber como criar combinações e tipos de dados para incluir seus campos personalizados.

## Mapeamento de tipos XDM para outros formatos

A tabela abaixo descreve o mapeamento entre cada tipo (`meta:xdmType`) de XDM e outros formatos de serialização.

| Tipo<br>XDM(meta:xdmType) | JSON<br>(Schema JSON) | Parquet<br>(tipo/anotação) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospie | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | tipo:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | String | System.String | String | string | String | string |
| número | tipo:número | DUPLO | DoubleType | java.lang.Double | Duplo | System.Double | Número | duplo | Duplo | duplo |
| long | tipo:<br>número inteiro máximo:2^53+1<br>mínimo:-2^53+1 | INT64 | LongType | java.lang.Long | Longo | System.Int64 | Número | long | Número inteiro | int64 |
| int | type:<br>integermaximum:2^31<br>mínimo:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Número | int | Número inteiro | int32 |
| short | type:<br>integermaximum:2^15<br>mínimo:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Curto | System.Int16 | Número | int | Número inteiro | int32 |
| byte | type:<br>integermaximum:2^7<br>mínimo:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Número | int | Número inteiro | int32 |
| booleano | tipo:booleano | BOOLEANO | BooleanType | java.lang.Boolean | Booleano | System.Boolean | Booleano | bool | Número inteiro | Número inteiro | bool |
| data | type:<br>stringformat:date<br>(RFC 3339, seção 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | String | data | Inteiro<br>(unix millis) | int64<br>(unix millis) |
| data e hora | type:<br>stringformat:date-time<br>(RFC 3339, seção 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | String | carimbo de data e hora | Inteiro<br>(unix millis) | int64<br>(unix millis) |
| mapa | objeto | O grupo<br><br>anotado MAP&lt;<span>key_type</span>> DEVE ser STRING<br><br>&lt;<span>value_type</span>> do tipo de valores de mapa | MapType<br><br>&quot;keyType&quot; DEVE ser StringType<br><br>&quot;valueType&quot; é o tipo de valores de mapa. | java.util.Map | Mapa | --- | objeto | objeto | mapa | map&lt;<span>key_type, value_type</span>> |

## Definição de tipos de campos XDM na API {#define-fields}

Os schemas XDM são definidos usando padrões de Schema [JSON e tipos de campo básicos, com restrições adicionais para nomes de campo que são impostas por](https://json-schema.org/) [!DNL Experience Platform]. A API [de Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Schemas permite que você defina tipos de campos adicionais usando formatos e restrições opcionais. Os tipos de campos XDM são expostos pelo atributo de nível de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` é um valor gerado pelo sistema e, portanto, não é necessário adicionar essa propriedade ao JSON para seu campo. A prática recomendada é usar tipos de Schemas JSON (como string e integer) com as restrições mín/máx apropriadas, conforme definido na tabela abaixo.

A tabela a seguir descreve a formatação apropriada para definir tipos de campos escalares e tipos de campos mais específicos usando propriedades opcionais. Mais informações sobre propriedades opcionais e palavras-chave específicas do tipo estão disponíveis na documentação [do Schema](https://json-schema.org/understanding-json-schema/reference/type.html)JSON.

Para começar, localize o tipo de campo desejado e use o código de amostra fornecido para criar sua solicitação de API para [criar uma mistura](../api/mixins.md#create) ou [criar um tipo](../api/data-types.md#create)de dados.

<table>
  <tr>
    <th>Tipo<br/>desejado(meta:xdmType)</th>
    <th>JSON<br/>(Schema JSON)</th>
    <th>Amostra de código</th>
  </tr>
  <tr>
    <td>string</td>
    <td>tipo: propriedades<br/><br/><strong>stringOptional:</strong><br/>
      <ul>
        <li>padrão</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>tipo: formato<br/>de string: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>tipo: propriedade<br/><br/><strong>stringOptional:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>Especifique rótulos de opção voltados para o cliente usando "meta:enum":
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Valor 1", "valor 2": "Valor 2", "valor3": "Valor 3" }, "padrão": "value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>número</td>
    <td>tipo:<br/>número mínimo: ±2,23×10^308<br/>máximo: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>tipo: número<br/>inteiro máximo:2^53+1<br>mínimo:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "número inteiro", "mínimo": -9007199254740992, "máximo": 9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>tipo: número<br/>inteiro máximo:2^31<br>mínimo:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "número inteiro", "mínimo": -2147483648, "máximo": 2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>tipo: número<br/>inteiro máximo:2^15<br>mínimo:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "número inteiro", "mínimo": -32768, "máximo": 32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>tipo: número<br/>inteiro máximo:2^7<br>mínimo:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "número inteiro", "mínimo": -128, "máximo": 128 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>booleano</td>
    <td><br/>tipo: propriedade boolean<br/>{true, false}<br/><br/><strong>Opcional:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "booleano", "padrão": false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>data</td>
    <td>tipo: formato<br/>de string: date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "data", "exemplos": ["2004-10-23"] }
      </pre>
      Data definida pela <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, seção 5.6</a>, em que "data completa" = data-limite "-" data-mês "-" data-dia (AAAA-MM-DD)
    </td>
  </tr>
  <tr>
    <td>data e hora</td>
    <td>tipo: formato<br/>de string: data e hora</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date-time", "exemplos": ["2004-10-23T12:00:00-06:00"] }
      </pre>
      Data e hora, conforme definido pela seção 5.6 <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">da</a>RFC 3339, em que "data e hora" = data completa "T" em tempo integral:<br/>(AAAA-MM-DD'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>matriz</td>
    <td>tipo: matriz</td>
    <td>items.type pode ser definido usando qualquer tipo escalar:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "type": "string" } }
      </pre>
      Matriz de objetos definidos por outro schema:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "$ref": "id" }
      </pre>
      Onde "id" é o {id} do schema de referência.
    </td>
  </tr>
  <tr>
    <td>objeto</td>
    <td>tipo: objeto</td>
    <td>de mídia.{field}.type pode ser definido usando qualquer tipo escalar:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" } }
      </pre>
      Campo do tipo "objeto" definido por um schema de referência:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "$ref": "id" }
      </pre>
      Onde "id" é o {id} do schema de referência.
    </td>
  </tr>
  <tr>
    <td>mapa</td>
    <td>tipo:<br/><br/><strong>objectNote:</strong><br/>o uso do tipo de dados 'map' é reservado para uso pelo setor e pelo schema do fornecedor e não está disponível para uso em campos definidos pelo locatário. É usado em schemas padrão quando os dados são representados como chaves que mapeiam para algum valor, ou quando as chaves não podem ser incluídas em um schema estático e devem ser tratadas como valores de dados.</td>
    <td>UM 'mapa' NÃO DEVE definir nenhuma propriedade. Ele DEVE definir um único schema "[!UICONTROL additionalProperties]" para descrever o tipo de valores contidos no 'map'. Um "mapa" no XDM pode conter apenas um único tipo de dados. Os valores podem ser qualquer definição válida de schema XDM, incluindo uma matriz ou um objeto, ou como referência a outro schema (via $ref).<br/><br/>Mapear campo com valores do tipo 'string':
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "type": "string" } }
      </pre>
    Mapear campo com valores sendo uma matriz de sequências de caracteres:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "type": "array", "items": { "type": "string" } }
      </pre>
    Campo de mapa que faz referência a outro schema:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "$ref": "id" }
      </pre>
      Onde "id" é o {id} do schema de referência.
    </td>
  </tr>
</table>
