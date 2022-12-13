---
title: Definir campos XDM na API do Registro de esquema
description: Saiba como definir campos diferentes ao criar recursos personalizados do Experience Data Model (XDM) na API do Registro de Schema.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 0947eb38bdb18cb3783723cb11be79d3d32a3b76
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# Definir campos XDM na API do Registro de Esquema

Todos os campos do Experience Data Model (XDM) são definidos usando o padrão [Esquema JSON](https://json-schema.org/) restrições que se aplicam ao tipo de campo, com restrições adicionais para nomes de campo que são aplicadas pelo Adobe Experience Platform. A API de Registro de Esquema permite definir campos personalizados em seus esquemas usando formatos e restrições opcionais. Os tipos de campo XDM são expostos pelo atributo de nível de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` é um valor gerado pelo sistema e, portanto, você não é obrigado a adicionar essa propriedade ao JSON do seu campo ao usar a API (exceto quando [criação de tipos de mapa personalizado](#custom-maps)). A prática recomendada é usar tipos de Esquema JSON (como `string` e `integer`) com as restrições mínimas/máximas apropriadas, conforme definido na tabela abaixo.

Este guia descreve a formatação apropriada para definir tipos de campos diferentes, incluindo aqueles com propriedades opcionais. Mais informações sobre propriedades opcionais e palavras-chave específicas do tipo estão disponíveis no [Documentação do Esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para começar, encontre o tipo de campo desejado e use o código de amostra fornecido para criar sua solicitação de API para [criação de um grupo de campos](../api/field-groups.md#create) ou [criação de um tipo de dados](../api/data-types.md#create).

## [!UICONTROL String] {#string}

[!UICONTROL String] os campos são indicados por `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Opcionalmente, é possível restringir quais tipos de valores podem ser inseridos para a cadeia de caracteres por meio das seguintes propriedades adicionais:

* `pattern`: Um padrão regex para restringir.
* `minLength`: Um comprimento mínimo para a string.
* `maxLength`: Um comprimento máximo para a string.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

[!UICONTROL URI] os campos são indicados por `type: string` com um `format` propriedade definida como `uri`. Nenhuma outra propriedade é aceita.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] os campos devem usar `type: string`, com os valores de enum fornecidos em um `enum` array:

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

É possível fornecer rótulos opcionais voltados para o cliente para cada valor em um `meta:enum` , com cada rótulo vinculado a um `enum` valor.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  }
}
```

>[!NOTE]
>
>O `meta:enum` valor faz **not** declare uma enumeração ou direcione qualquer validação de dados sozinha. Na maioria dos casos, as cadeias de caracteres fornecidas em `meta:enum` são igualmente fornecidas nos termos do `enum` para garantir que os dados sejam restritos. No entanto, existem alguns casos de uso em que `meta:enum` é fornecido sem um `enum` matriz. Veja o tutorial em [definição de valores sugeridos](../tutorials/suggested-values.md) para obter mais informações.

Como opção, você pode fornecer uma `default` propriedade para indicar o padrão `enum` valor que o campo usará se nenhum valor for fornecido.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  },
  "default": "value1"
}
```

>[!IMPORTANT]
>
>Se não `default` é fornecido e o campo enum é definido como `required`, qualquer registro que não tenha um valor aceito para esse campo falhará na validação após a assimilação.

## [!UICONTROL Número] {#number}

Os campos de número são indicados por `type: number` e não têm outras propriedades necessárias.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` são usados para qualquer tipo numérico, seja inteiro ou número de ponto flutuante, enquanto [`integer` tipos](#integer) são utilizadas especificamente para números integrais. Consulte a [Documentação do Esquema JSON em tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obter mais informações sobre os casos de uso para cada tipo.

## [!UICONTROL Número inteiro] {#integer}

[!UICONTROL Número inteiro] os campos são indicados por `type: integer` e não tem outros campos obrigatórios.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Ao `integer` os tipos se referem especificamente aos números integrais, [`number` tipos](#number) são usados para qualquer tipo numérico, seja inteiro ou números de ponto flutuante. Consulte a [Documentação do Esquema JSON em tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obter mais informações sobre os casos de uso para cada tipo.

Opcionalmente, é possível restringir o intervalo do inteiro adicionando `minimum` e `maximum` à definição. Vários outros tipos numéricos compatíveis com a interface do usuário do Construtor de esquemas são apenas `integer` tipos com `minimum` e `maximum` restrições, como [[!UICONTROL Longo]](#long), [[!UICONTROL Curto]](#short)e [[!UICONTROL Byte]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Longo] {#long}

O equivalente de um [!UICONTROL Longo] o campo criado por meio da interface do usuário do Construtor de esquemas é um [`integer` campo de tipo](#integer) com `minimum` e `maximum` valores (`-9007199254740992` e `9007199254740992`, respectivamente).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL Curto] {#short}

O equivalente de um [!UICONTROL Curto] o campo criado por meio da interface do usuário do Construtor de esquemas é um [`integer` campo de tipo](#integer) com `minimum` e `maximum` valores (`-32768` e `32768`, respectivamente).

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL Byte] {#byte}

O equivalente de um [!UICONTROL Byte] o campo criado por meio da interface do usuário do Construtor de esquemas é um [`integer` campo de tipo](#integer) com `minimum` e `maximum` valores (`-128` e `128`, respectivamente).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Booleano] {#boolean}

[!UICONTROL Booleano] os campos são indicados por `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Como opção, você pode fornecer uma `default` valor que o campo usará quando nenhum valor explícito for fornecido durante a assimilação.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>Se não `default` é fornecido e o campo booleano é definido como `required`, qualquer registro que não tenha um valor aceito para esse campo falhará na validação após a assimilação.

## [!UICONTROL Data] {#date}

[!UICONTROL Data] os campos são indicados por `type: string` e `format: date`. Opcionalmente, também é possível fornecer uma matriz de `examples` para utilizar o nos casos em que você deseja exibir uma string de data de amostra para os usuários que inserem os dados manualmente.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

[!UICONTROL DateTime] os campos são indicados por `type: string` e `format: date-time`. Opcionalmente, também é possível fornecer uma matriz de `examples` para aproveitar os casos em que você deseja exibir uma string de data e hora de amostra para os usuários que inserem os dados manualmente.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL Matriz] {#array}

[!UICONTROL Matriz] os campos são indicados por `type: array` e um `items` que define o esquema dos itens que a matriz aceitará.

Você pode definir itens de matriz usando tipos primitivos, como uma matriz de strings:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

Também é possível definir os itens de matriz com base em um tipo de dados existente, referindo-se à variável `$id` do tipo de dados através de um `$ref` propriedade. Veja a seguir uma matriz de [!UICONTROL Item de Pagamento] objetos:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL Objeto] {#object}

[!UICONTROL Objeto] os campos são indicados por `type: object` e `properties` objeto que define subpropriedades para o campo schema .

Cada subcampo definido em `properties` pode ser definido usando qualquer primitivo `type` ou referenciando um tipo de dados existente por meio de um `$ref` propriedade apontando para a `$id` do tipo de dados em questão:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

Também é possível definir o objeto inteiro fazendo referência a um tipo de dados, desde que o tipo de dados em questão esteja definido como `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Mapa] {#map}

Um campo de mapa é essencialmente um [`object`campo -type](#object) com um conjunto de chaves sem restrições. Como objetos, mapas têm uma `type` valor de `object`, mas seus `meta:xdmType` está explicitamente definido como `map`.

Um mapa **não deve** defina quaisquer propriedades. It **must** defina uma `additionalProperties` para descrever o tipo de valores contidos no mapa (cada mapa só pode conter um único tipo de dados). O `type` deve ser `string` ou `integer`.

Por exemplo, um campo de mapa com valores do tipo string seria definido da seguinte maneira:

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

Consulte a seção abaixo para obter mais detalhes sobre a criação de campos de mapa personalizados.

### Criação de tipos de mapa personalizado {#custom-maps}

Para oferecer suporte a dados &quot;semelhantes ao mapa&quot; com eficiência no XDM, os objetos podem receber anotações com um `meta:xdmType` defina como `map` para deixar claro que um objeto deve ser gerenciado como se o conjunto de chaves não estivesse restrito. Os dados assimilados em campos de mapa devem usar chaves de string e somente valores de string ou inteiros (como determinado por `additionalProperties.type`).

O XDM coloca as seguintes restrições sobre o uso dessa dica de armazenamento:

* Os tipos de mapa DEVEM ser do tipo `object`.
* Os tipos de mapa NÃO DEVEM ter propriedades definidas (em outras palavras, eles definem objetos &quot;vazios&quot;).
* Os tipos de mapa DEVEM incluir uma `additionalProperties.type` que descreve os valores que podem ser colocados no mapa, `string` ou `integer`.

Certifique-se de que você esteja usando apenas campos do tipo mapa quando for absolutamente necessário, pois eles apresentam as seguintes desvantagens de desempenho:

* Tempo de resposta de [Serviço de query Adobe Experience Platform](../../query-service/home.md) decai de três segundos para dez segundos para 100 milhões de registros.
* Os mapas devem ter menos de 16 chaves ou, caso contrário, arriscam mais degradação.

A interface do usuário da Platform também tem limitações em como extrair as chaves dos campos do tipo mapa. Embora os campos do tipo de objeto possam ser expandidos, os mapas são exibidos como um único campo.

## Próximas etapas

Este guia cobriu como definir diferentes tipos de campo na API. Para obter mais informações sobre como os tipos de campos XDM são formatados, consulte o guia em [Restrições do tipo de campo XDM](../schema/field-constraints.md).
