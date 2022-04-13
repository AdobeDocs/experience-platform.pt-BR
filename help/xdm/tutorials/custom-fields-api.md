---
title: Definir campos XDM na API do Registro de esquema
description: Saiba como definir campos diferentes ao criar recursos personalizados do Experience Data Model (XDM) na API do Registro de Schema.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Definir campos XDM na API do Registro de Esquema

Todos os campos do Experience Data Model (XDM) são definidos usando o padrão [Esquema JSON](https://json-schema.org/) restrições que se aplicam ao tipo de campo, com restrições adicionais para nomes de campo que são aplicadas pelo Adobe Experience Platform. A API de Registro de Esquema permite definir campos personalizados em seus esquemas usando formatos e restrições opcionais. Os tipos de campo XDM são expostos pelo atributo de nível de campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` é um valor gerado pelo sistema e, portanto, você não é obrigado a adicionar essa propriedade ao JSON do seu campo ao usar a API (exceto quando [criação de tipos de mapa personalizado](#maps)). A prática recomendada é usar tipos de Esquema JSON (como `string` e `integer`) com as restrições mínimas/máximas apropriadas, conforme definido na tabela abaixo.

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
    <br>Observe que a variável <code>meta:enum</code> valor faz <strong>not</strong> declare uma enumeração ou direcione qualquer validação de dados sozinha. Na maioria dos casos, as cadeias de caracteres fornecidas em <code>meta:enum</code> são igualmente fornecidas nos termos do <code>enum</code> para garantir que os dados sejam restritos. No entanto, existem alguns casos de uso em que <code>meta:enum</code> é fornecido sem um <code>enum</code> matriz. Veja o tutorial em <a href="../tutorials/suggested-values.md">definição de valores sugeridos</a> para obter mais informações.
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
    <td>Um campo do tipo mapa é essencialmente um campo do tipo objeto com um conjunto não restrito de chaves. Como objetos, mapas têm uma <code>type</code> valor de <code>object</code>, mas seus <code>meta:xdmType</code> está explicitamente definido como <code>map</code>.<br><br>Um mapa <strong>não deve</strong> defina quaisquer propriedades. It <strong>must</strong> defina uma <code>additionalProperties</code> para descrever o tipo de valores contidos no mapa (cada mapa só pode conter um único tipo de dados). O <code>type</code> deve ser <code>string</code> ou <code>integer</code>.<br/><br/>Um campo de mapa com valores do tipo string:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "meta:xdmType": "map", "additionalProperties":{ "type": "string" }</pre>
    Consulte a seção abaixo para obter mais informações sobre a criação de tipos de mapa personalizado no XDM.
    </td>
  </tr>
</table>

## Criação de tipos de mapa personalizado {#maps}

Para oferecer suporte a dados &quot;semelhantes ao mapa&quot; com eficiência no XDM, os objetos podem receber anotações com um `meta:xdmType` defina como `map` para deixar claro que um objeto deve ser gerenciado como se o conjunto de chaves não estivesse restrito. Os dados assimilados em campos de mapa devem usar chaves de string e somente valores de string ou inteiros (como determinado por `additionalProperties.type`).

O XDM coloca as seguintes restrições sobre o uso dessa dica de armazenamento:

* Os tipos de mapa DEVEM ser do tipo `object`.
* Os tipos de mapa NÃO DEVEM ter propriedades definidas (em outras palavras, eles definem objetos &quot;vazios&quot;).
* Os tipos de mapa DEVEM incluir uma `additionalProperties.type` que descreve os valores que podem ser colocados no mapa, `string` ou `integer`.

Certifique-se de que você esteja usando apenas campos do tipo mapa quando for absolutamente necessário, pois eles apresentam as seguintes desvantagens de desempenho:

* O tempo de resposta do Serviço de query da Adobe Experience Platform diminui de três segundos para dez segundos para 100 milhões de registros.
* Os mapas devem ter menos de 16 chaves ou, caso contrário, arriscam mais degradação.

A interface do usuário da Platform também tem limitações em como extrair as chaves dos campos do tipo mapa. Embora os campos do tipo de objeto possam ser expandidos, os mapas são exibidos como um único campo.

## Próximas etapas

Este guia cobriu como definir diferentes tipos de campo na API. Para obter mais informações sobre como os tipos de campos XDM são formatados, consulte o guia em [Restrições do tipo de campo XDM](../schema/field-constraints.md).
