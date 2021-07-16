---
title: Filtrar respostas na API do reator
description: Saiba como filtrar resultados ao listar recursos na API de reator.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# Filtrar respostas na API do reator

Ao usar endpoints de lista (GET) na API do Reator, talvez seja necessário limitar os resultados retornados a um subconjunto de registros. Para isso, muitos dos endpoints de lista da API são compatíveis com a capacidade de filtrar por atributos específicos. Se, em vez disso, você deseja fazer consultas estruturadas à API, consulte o guia em [search](./search.md).

## Sintaxe do filtro

O exemplo a seguir explica como implementar filtros para suas solicitações do GET.

**Formato da API**

Para filtrar a resposta de um determinado ponto de extremidade de lista, você deve fornecer um parâmetro de consulta `filter` no caminho da solicitação.

>[!NOTE]
>
>O modelo abaixo usa colchetes (`[]`) e caracteres de espaço para legibilidade. Na prática, esses caracteres devem ser codificados por URI, conforme descrito em [RFC 3986](https://tools.ietf.org/html/rfc3986). Um exemplo de um caminho de solicitação corretamente codificado é mostrado posteriormente neste guia.
>
>Observe que se a estrutura dos filtros estiver incorreta, nenhum filtro será aplicado e o conjunto de resultados completo será retornado.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Propriedade | Descrição |
| --- | --- |
| `{ENDPOINT}` | Um endpoint da listagem na API do reator que suporta parâmetros de filtro. |
| `{ATTRIBUTE_NAME}` | O nome de um atributo específico pelo qual filtrar resultados. Lembre-se de que diferentes endpoints suportam atributos diferentes para filtragem. Consulte o guia de referência do endpoint com o qual você está trabalhando para obter uma lista de atributos de filtragem disponíveis. |
| `{OPERATOR}` | O operador que determina como os resultados são avaliados em relação ao `{VALUE}` fornecido. Os operadores suportados estão listados na seção [Apêndice](#supported-operators). |
| `{VALUE}` | O valor para comparar os resultados retornados. Ao comparar para igualdade usando o operador `EQ` , o valor deve ser uma correspondência exata, que diferencia maiúsculas e minúsculas, para ser incluído na resposta. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação de exemplo abaixo recupera uma lista de bibliotecas publicadas aplicando um filtro que requer o atributo `state` da biblioteca para ser igual a `published`.

Antes da codificação do URI, a sintaxe desse filtro no caminho da solicitação seria semelhante ao seguinte:

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

Depois que os parâmetros de caminho e consulta tiverem sido codificados por URI, eles poderão ser usados em solicitações de API, como o abaixo:

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

## Filtragem em vários valores {#multiple-values}

Para filtrar por vários valores para um único atributo, forneça os valores como uma lista separada por vírgulas.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Uso de vários filtros

Para aplicar filtros para vários atributos, forneça um parâmetro `filter` para cada atributo. Os parâmetros devem ser separados por caracteres de E comercial (`&`).

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Se você especificar o mesmo atributo em vários filtros na mesma solicitação, somente o último filtro fornecido para esse atributo será aplicado.

## Apêndice

A seção a seguir contém informações adicionais para trabalhar com filtros na API do Reator.

### Operadores de filtro compatíveis {#operators}

A tabela a seguir lista os valores de operador suportados para parâmetros de filtro. Lembre-se de que, dependendo do atributo que você está filtrando, nem todos os operadores de filtro disponíveis serão aplicáveis, como o uso de operadores &quot;menor que&quot; ou &quot;maior que&quot; para atributos de sequência.

| Operador | Descrição |
| --- | --- |
| `EQ` | O atributo deve ser igual ao valor fornecido. |
| `NOT` | O atributo não deve ser igual ao valor fornecido. |
| `LT` | O atributo deve ser menor que o valor fornecido. |
| `GT` | O atributo deve ser maior que o valor fornecido. |
| `BETWEEN` | O atributo deve estar dentro de um intervalo de valores especificado. Ao usar esse operador, [dois valores](#multiple-values) devem ser fornecidos para indicar os valores mínimo e máximo para o intervalo desejado. |
| `CONTAINS` | O atributo deve conter o valor fornecido, como um conjunto de caracteres em um atributo de string. |
