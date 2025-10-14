---
title: Definir campos XDM na API do registro de esquema
description: Saiba como definir campos diferentes ao criar recursos personalizados do Experience Data Model (XDM) na API do registro de esquema.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 6c6104a6aa0a80c886f4f02486a7645eb95da781
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# Definir campos XDM na API do registro de esquema

Todos os campos do Experience Data Model (XDM) são definidos usando as restrições padrão do [Esquema JSON](https://json-schema.org/) que se aplicam ao tipo de campo, com restrições adicionais para nomes de campo impostos pelo Adobe Experience Platform. A API do Registro de esquema permite definir campos personalizados em seus esquemas por meio do uso de formatos e restrições opcionais. Os tipos de campo XDM são expostos pelo atributo de nível de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` é um valor gerado pelo sistema e, portanto, você não precisa adicionar essa propriedade ao JSON do seu campo ao usar a API (exceto ao [criar tipos de mapa personalizados](#custom-maps)). A prática recomendada é usar tipos de Esquema JSON (como `string` e `integer`) com as restrições mín/máx apropriadas, conforme definido na tabela abaixo.

Este guia descreve a formatação apropriada para definir diferentes tipos de campo, incluindo aqueles com propriedades opcionais. Mais informações sobre propriedades opcionais e palavras-chave específicas do tipo estão disponíveis na [documentação sobre o Esquema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Para começar, encontre o tipo de campo desejado e use o código de exemplo fornecido para criar sua solicitação de API para [criação de um grupo de campos](../api/field-groups.md#create) ou [criação de um tipo de dados](../api/data-types.md#create).

## [!UICONTROL String] {#string}

Os campos [!UICONTROL Cadeia] são indicados por `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Opcionalmente, é possível restringir quais tipos de valores podem ser inseridos para a string por meio das seguintes propriedades adicionais:

* `pattern`: um padrão regex pelo qual restringir.
* `minLength`: Um comprimento mínimo para a cadeia de caracteres. As cadeias de caracteres recebem um valor mínimo de `1` por padrão.
* `maxLength`: Um comprimento máximo para a cadeia de caracteres.

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

Os campos [!UICONTROL URI] são indicados por `type: string` com uma propriedade `format` definida como `uri`. Nenhuma outra propriedade é aceita.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enumeração] {#enum}

Os campos [!UICONTROL Enum] devem usar `type: string`, com os próprios valores de enumeração fornecidos em uma matriz `enum`:

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

Opcionalmente, você pode fornecer rótulos voltados para o cliente para cada valor em uma propriedade `meta:enum`, com cada rótulo digitado para um valor correspondente em `enum`.

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
>O valor `meta:enum` **não** declara uma enumeração ou unidade para qualquer validação de dados por conta própria. Na maioria dos casos, as cadeias de caracteres fornecidas em `meta:enum` também são fornecidas em `enum` para garantir que os dados sejam restritos. No entanto, há alguns casos de uso em que `meta:enum` é fornecido sem uma matriz `enum` correspondente. Consulte o tutorial em [definindo valores sugeridos](../tutorials/suggested-values.md) para obter mais informações.

Opcionalmente, você pode fornecer uma propriedade `default` para indicar o valor `enum` padrão que o campo usará se nenhum valor for fornecido.

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
>Se nenhum valor `default` for fornecido e o campo enum for definido como `required`, qualquer registro sem um valor aceito para esse campo falhará na validação após a assimilação.

## [!UICONTROL Número] {#number}

Campos numéricos são indicados por `type: number` e não têm outras propriedades necessárias.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` tipos são usados para qualquer tipo numérico, seja números inteiros ou números de ponto flutuante, enquanto [`integer` tipos](#integer) são usados especificamente para números integrais. Consulte a [documentação do Esquema JSON sobre tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obter mais informações sobre os casos de uso para cada tipo.

## [!UICONTROL Inteiro] {#integer}

Os campos [!UICONTROL Integer] são indicados por `type: integer` e não têm outros campos obrigatórios.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Embora `integer` tipos se refiram especificamente a números inteiros, [`number` tipos](#number) são usados para qualquer tipo numérico, seja números inteiros ou números de ponto flutuante. Consulte a [documentação do Esquema JSON sobre tipos numéricos](https://json-schema.org/understanding-json-schema/reference/numeric.html) para obter mais informações sobre os casos de uso para cada tipo.

Opcionalmente, é possível restringir o intervalo do inteiro adicionando as propriedades `minimum` e `maximum` à definição. Vários outros tipos numéricos com suporte pela interface do Construtor de Esquemas são apenas `integer` tipos com `minimum` e `maximum` restrições específicas, como [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short) e [[!UICONTROL Byte]](#byte).

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

O equivalente de um campo [!UICONTROL Long] criado por meio da interface do usuário do Construtor de Esquemas é um campo do tipo [`integer` &#x200B;](#integer) com `minimum` e `maximum` valores específicos (`-9007199254740992` e `9007199254740992`, respectivamente).

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

O equivalente de um campo [!UICONTROL Short] criado por meio da interface do usuário do Construtor de Esquemas é um campo do tipo [`integer`](#integer) com `minimum` e `maximum` valores específicos (`-32768` e `32767`, respectivamente).

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32767
}
```

## [!UICONTROL Byte] {#byte}

O equivalente de um campo [!UICONTROL Byte] criado por meio da interface do usuário do Construtor de Esquemas é um campo do tipo [`integer`](#integer) com `minimum` e `maximum` valores específicos (`-128` e `127`, respectivamente).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 127
}
```

## [!UICONTROL Booleano] {#boolean}

Os campos [!UICONTROL booleanos] são indicados por `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Opcionalmente, você pode fornecer um valor `default` que o campo usará quando nenhum valor explícito for fornecido durante a assimilação.

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
>Se nenhum valor `default` for fornecido e o campo booleano for definido como `required`, qualquer registro sem um valor aceito para esse campo falhará na validação após a assimilação.

## [!UICONTROL Data] {#date}

Os campos [!UICONTROL Data] são indicados por `type: string` e `format: date`. Como opção, você também pode fornecer uma matriz de `examples` para usar nos casos em que deseja exibir uma cadeia de caracteres de data de exemplo para usuários que inserem os dados manualmente.

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

Os campos [!UICONTROL DateTime] são indicados por `type: string` e `format: date-time`. Como opção, você também pode fornecer uma matriz de `examples` para usar nos casos em que deseja exibir uma amostra de cadeia de caracteres de data e hora para usuários que inserem os dados manualmente.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## Matriz [!UICONTROL 1&rbrace;] {#array}

Os campos [!UICONTROL Matriz] são indicados por `type: array` e um objeto `items` que define o esquema dos itens que a matriz aceitará.

Você pode definir itens de matriz usando tipos primitivos, como uma matriz de sequências de caracteres:

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

Você também pode definir os itens de matriz com base em um tipo de dados existente referenciando o `$id` do tipo de dados por meio de uma propriedade `$ref`. Esta é uma matriz de objetos [!UICONTROL Item de Pagamento]:

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

Os campos [!UICONTROL Object] são indicados por `type: object` e um objeto `properties` que define subpropriedades para o campo de esquema.

Cada subcampo definido em `properties` pode ser definido usando qualquer `type` primitivo ou fazendo referência a um tipo de dados existente por meio de uma propriedade `$ref` que aponte para `$id` do tipo de dados em questão:

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

Você também pode definir o objeto inteiro por meio do referenciando um tipo de dados, desde que o tipo de dados em questão seja definido como `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Mapa] {#map}

Um campo de mapa é essencialmente um campo do tipo [`object`](#object) com um conjunto de chaves não restrito. Como objetos, os mapas têm um valor `type` de `object`, mas seu `meta:xdmType` é explicitamente definido como `map`.

Um mapa **não deve** definir propriedades. Ele **deve** definir um único esquema `additionalProperties` para descrever o tipo de valores contidos no mapa (cada mapa só pode conter um único tipo de dados). O valor `type` deve ser `string` ou `integer`.

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

Consulte a seção abaixo para obter mais detalhes sobre como criar campos de mapa personalizados.

### Criação de tipos de mapa personalizados {#custom-maps}

Para oferecer suporte a dados &quot;semelhantes a mapas&quot; com eficiência no XDM, os objetos podem ser anotados com um `meta:xdmType` definido como `map` para deixar claro que um objeto deve ser gerenciado como se o conjunto de chaves não estivesse restrito. Os dados assimilados em campos de mapa devem usar chaves de cadeia de caracteres e somente valores de cadeia de caracteres ou inteiros (conforme determinado por `additionalProperties.type`).

O XDM impõe as seguintes restrições ao uso dessa dica de armazenamento:

* Os tipos de mapa DEVEM ser do tipo `object`.
* Os tipos de mapa NÃO DEVEM ter propriedades definidas (em outras palavras, eles definem objetos &quot;vazios&quot;).
* Os tipos de mapa DEVEM incluir um campo `additionalProperties.type` que descreva os valores que podem ser colocados no mapa, `string` ou `integer`.

Certifique-se de que você só esteja usando campos do tipo mapa quando for absolutamente necessário, pois eles apresentam as seguintes desvantagens de desempenho:

* O tempo de resposta do [Serviço de Consulta do Adobe Experience Platform](../../query-service/home.md) degrada de três segundos a dez segundos para 100 milhões de registros.
* Os mapas devem ter menos de 16 chaves, caso contrário, haverá risco de degradação adicional.

A interface do usuário do Experience Platform também tem limitações na forma como pode extrair as chaves de campos do tipo mapa. Enquanto os campos do tipo objeto podem ser expandidos, os mapas são exibidos como um único campo.

## Próximas etapas

Este guia abordou como definir diferentes tipos de campo na API. Para obter mais informações sobre como os tipos de campo XDM são formatados, consulte o manual sobre [Restrições de tipo de campo XDM](../schema/field-constraints.md).
