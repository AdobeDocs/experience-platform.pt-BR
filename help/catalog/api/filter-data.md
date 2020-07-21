---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Filtrar dados do catálogo usando parâmetros de query
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 1%

---


# Filtrar [!DNL Catalog] dados usando parâmetros de query

A [!DNL Catalog Service] API permite que os dados de resposta sejam filtrados por meio do uso de parâmetros de query de solicitação. Parte das práticas recomendadas para [!DNL Catalog] o é usar filtros em todas as chamadas de API, já que elas reduzem a carga na API e ajudam a melhorar o desempenho geral.

Esse documento descreve os métodos mais comuns para filtrar [!DNL Catalog] objetos na API. É recomendável consultar esse documento ao ler o guia [do desenvolvedor do](getting-started.md) Catálogo para saber mais sobre como interagir com a [!DNL Catalog] API. Para obter informações mais gerais sobre [!DNL Catalog Service], consulte a visão geral [do](../home.md)catálogo.

## Limitar objetos retornados

O parâmetro `limit` query restringe o número de objetos retornados em uma resposta. [!DNL Catalog] as respostas são medidas automaticamente de acordo com os limites configurados:

* Se um `limit` parâmetro não for especificado, o número máximo de objetos por carga de resposta será 20.
* Para query de conjunto de dados, se `observableSchema` for solicitado usando o parâmetro `properties` query, o número máximo de conjuntos de dados retornados será 20.
* O limite global para todos os outros query de Catálogo é de 100 objetos.
* Parâmetros inválidos (incluindo `limit` `limit=0`) resultam em respostas de erro de nível 400 que descrevem intervalos adequados.
* Os limites ou deslocamentos que são passados como parâmetros de query têm prioridade sobre os que são passados como cabeçalhos.

**Formato da API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Um número inteiro que indica o número de objetos a serem retornados, variando de 1 a 100. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados enquanto limita a resposta a três objetos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de conjuntos de dados, limitados ao número indicado pelo parâmetro do `limit` query.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Limitar propriedades exibidas

Mesmo ao filtrar o número de objetos retornados usando o `limit` parâmetro, os próprios objetos retornados muitas vezes podem conter mais informações do que você realmente precisa. Para reduzir ainda mais a carga no sistema, a prática recomendada é filtrar as respostas para incluir apenas as propriedades de que você precisa.

O `properties` parâmetro filtros objetos de resposta para retornar somente um conjunto de propriedades especificadas. O parâmetro pode ser definido para retornar uma ou várias propriedades.

O `properties` parâmetro só aceita propriedades de objetos de nível superior, o que significa que para o seguinte objeto de amostra, você pode aplicar filtros para `name`, `description`e `subItem`, mas NÃO para `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**Formato da API**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | O nome de um atributo a ser incluído no corpo da resposta. |
| `{OBJECT_ID}` | O identificador exclusivo de um [!DNL Catalog] objeto específico que está sendo recuperado. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados. A lista separada por vírgulas dos nomes de propriedade fornecida sob o `properties` parâmetro indica as propriedades a serem retornadas na resposta. Um `limit` parâmetro também é incluído, o que limita o número de conjuntos de dados retornados. Se a solicitação não incluísse um `limit` parâmetro, a resposta conteria no máximo 20 objetos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de [!DNL Catalog] objetos com apenas as propriedades solicitadas exibidas.

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

Com base na resposta acima, pode inferir-se o seguinte:

* Se um objeto não tiver nenhuma propriedade solicitada, ele só mostrará as propriedades solicitadas que ele incluir. (`Dataset1`)
* Se um objeto não incluir nenhuma das propriedades solicitadas, ele aparecerá como um objeto vazio. (`Dataset2`)
* Um conjunto de dados pode retornar uma propriedade solicitada como um objeto vazio se ela contiver a propriedade, mas não houver valor. (`Dataset3`)
* Caso contrário, o conjunto de dados exibirá o valor total de todas as propriedades solicitadas. (`Dataset4`)

## Índice inicial de compensação da lista de resposta

O parâmetro `start` query desloca a lista de resposta para frente por um número especificado, usando numeração com base em zero. Por exemplo, `start=2` compensaria a resposta ao start no terceiro objeto listado.

Se o `start` parâmetro não estiver emparelhado com um `limit` parâmetro, o número máximo de objetos retornados será 20.

**Formato da API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto Catalog a ser recuperado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Um número inteiro que indica o número de objetos pelos quais a resposta deve ser deslocada. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, compensando o quinto objeto (`start=4`) e limitando a resposta a dois conjuntos de dados retornados (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta inclui um objeto JSON que contém dois itens de nível superior (`limit=2`), um para cada conjunto de dados e seus detalhes (os detalhes foram condensados no exemplo). A resposta é alterada por quatro (`start=4`), o que significa que os conjuntos de dados mostrados são os números cinco e seis cronologicamente.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrar por tag

Alguns objetos de Catálogo oferecem suporte ao uso de um `tags` atributo. As tags podem anexar informações a um objeto e depois podem ser usadas para recuperar esse objeto. A escolha de quais tags usar e como aplicá-las depende de seus processos organizacionais.

Há algumas limitações a serem consideradas ao usar tags:

* Os únicos objetos de Catálogo que atualmente suportam tags são conjuntos de dados, lotes e conexões.
* Os nomes das tags são exclusivos à sua organização IMS.
* Os processos da Adobe podem aproveitar as tags para determinados comportamentos. Os nomes dessas tags recebem o prefixo &quot;adobe&quot; como padrão. Portanto, você deve evitar essa convenção ao declarar nomes de tags.
* Os seguintes nomes de tags são reservados para uso em toda a empresa [!DNL Experience Platform], pelo que não podem ser declarados como um nome de tag para sua organização:
   * `unifiedProfile`: Esse nome de tag é reservado para que conjuntos de dados sejam assimilados [!DNL Real-time Customer Profile](../../profile/home.md).
   * `unifiedIdentity`: Esse nome de tag é reservado para que conjuntos de dados sejam assimilados [!DNL Identity Service](../../identity-service/home.md).

Abaixo está um exemplo de um conjunto de dados que contém uma `tags` propriedade. As tags dentro dessa propriedade assumem a forma de pares de valores chave, com cada valor de tag exibido como uma matriz contendo uma única string:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**Formato da API**

Os valores do `tags` parâmetro assumem a forma de pares de valores chave, usando o formato `{TAG_NAME}:{TAG_VALUE}`. Vários pares de valores chave podem ser fornecidos na forma de uma lista separada por vírgulas. Quando várias tags são fornecidas, uma relação E é assumida.

O parâmetro suporta caracteres curinga (`*`) para valores de tag. Por exemplo, uma string de pesquisa de `test*` retorna qualquer objeto em que o valor da tag começa com &quot;test&quot;. Uma string de pesquisa que consiste apenas em um caractere curinga pode ser usada para filtrar objetos com base em se eles contêm ou não uma tag específica, independentemente do seu valor.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | O nome da tag para filtrar. |
| `{TAG_VALUE}` | O valor da tag para filtrar. Suporta caracteres curingas (`*`). |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, filtrando por uma tag que tem um valor específico E a segunda tag que está presente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de conjuntos de dados que contêm `sampleTag` um valor de &quot;123456&quot;, E `secondTag` com qualquer valor. A menos que um limite também seja especificado, a resposta contém um máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtrar por intervalo de datas

Alguns pontos de extremidade na [!DNL Catalog] API têm parâmetros de query que permitem query variados, na maioria das vezes no caso de datas.

**Formato da API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{TIMESTAMP }` | Um número inteiro datetime na época Unix. |

**Solicitação**

A solicitação a seguir recupera uma lista de lotes criados durante o mês de abril de 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de [!DNL Catalog] objetos que estão dentro do intervalo de datas especificado. A menos que um limite também seja especificado, a resposta contém um máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Classificar por propriedade

O parâmetro de `orderBy` query permite que você classifique (ordene) os dados de resposta com base em um valor de propriedade especificado. Esse parâmetro requer uma &quot;direção&quot; (`asc` para ascendente ou `desc` descendente), seguida por dois pontos (`:`) e uma propriedade para classificar os resultados. Se uma direção não for especificada, a direção padrão será crescente.

Várias propriedades de classificação podem ser fornecidas em uma lista separada por vírgulas. Se a primeira propriedade de classificação produzir vários objetos que contenham o mesmo valor para essa propriedade, a segunda propriedade de classificação será usada para classificar ainda mais esses objetos correspondentes.

Por exemplo, considere o seguinte query: `orderBy=name,desc:created`. Os resultados são classificados em ordem crescente com base na primeira propriedade de classificação, `name`. Nos casos em que vários registros compartilham a mesma `name` propriedade, esses registros correspondentes são classificados pela segunda propriedade de classificação, `created`. Se nenhum registro retornado compartilhar o mesmo `name`, a `created` propriedade não terá influência na classificação.


**Formato da API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto Catalog a ser recuperado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | O nome de uma propriedade para classificar os resultados. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados classificados por sua `name` propriedade. Se algum conjunto de dados compartilhar o mesmo `name`, esses conjuntos de dados, por sua vez, serão ordenados por sua `updated` propriedade em ordem decrescente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de [!DNL Catalog] objetos que são classificados de acordo com o `orderBy` parâmetro. A menos que um limite também seja especificado, a resposta contém um máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtrar por propriedade

[!DNL Catalog] fornece dois métodos de filtragem por propriedade, que são descritos mais detalhadamente nas seções a seguir:

* [Usando filtros](#using-simple-filters)simples: Filtre se uma propriedade específica corresponde a um valor específico.
* [Uso do parâmetro](#using-the-property-parameter)property: Use expressões condicionais para filtrar com base na existência de uma propriedade ou se o valor de uma propriedade corresponde, aproxima ou se compara a outro valor especificado ou a outra expressão regular.

### Uso de filtros simples {#using-simple-filters}

filtros simples permitem filtrar respostas com base em valores de propriedade específicos. Um filtro simples assume a forma de `{PROPERTY_NAME}={VALUE}`.

Por exemplo, o query `name=exampleName` retorna somente objetos cuja `name` propriedade contenha um valor de &quot;exampleName&quot;. Por outro lado, o query `name=!exampleName` retorna somente objetos cuja `name` propriedade **não** é &quot;exampleName&quot;.

Além disso, filtros simples suportam a capacidade de query para vários valores para uma única propriedade. Quando vários valores são fornecidos, a resposta retorna objetos cuja propriedade corresponde a **qualquer** um dos valores na lista fornecida. É possível inverter um query de vários valores prefixando um `!` caractere na lista, retornando somente objetos cujo valor de propriedade **não** está na lista fornecida (por exemplo, `name=!exampleName,anotherName`).

**Formato da API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | O nome da propriedade cujo valor você deseja filtrar. |
| `{VALUE}` | Um valor de propriedade que determina quais resultados incluir (ou excluir, dependendo do query). |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, filtrados para incluir somente conjuntos de dados cuja `name` propriedade tenha um valor de &quot;exampleName&quot; ou &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de conjuntos de dados, excluindo quaisquer conjuntos de dados cujo nome `name` seja &quot;exampleName&quot; ou &quot;anotherName&quot;. A menos que um limite também seja especificado, a resposta contém um máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### Uso do `property` parâmetro {#using-the-property-parameter}

O parâmetro `property` query oferece mais flexibilidade para a filtragem baseada em propriedades do que filtros simples. Além da filtragem com base no fato de uma propriedade ter um valor específico, o `property` parâmetro pode usar outros operadores de comparação (como &quot;mais que&quot; (`>`) e &quot;menos que&quot; (`<`)), bem como expressões regulares para filtrar por valores de propriedade. Também pode filtrar se uma propriedade existe ou não, independentemente de seu valor.

O `property` parâmetro só aceita propriedades de objetos de nível superior, o que significa que para o seguinte objeto de amostra, você pode filtrar por propriedade para `name`, `description`e `subItem`, mas NÃO para `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**Formato da API**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Uma expressão condicional que indica para qual propriedade deve ser query e como seu valor deve ser avaliado. Os exemplos são fornecidos abaixo. |

O valor do `property` parâmetro suporta vários tipos diferentes de expressões condicionais. A tabela a seguir descreve a sintaxe básica das expressões suportadas:

| Símbolo(s) | Descrição | Exemplo |
| --- | --- | --- |
| (None) | A indicação do nome da propriedade sem operador retorna somente objetos onde a propriedade existe, independentemente de seu valor. | `property=name` |
| ! | Prefixar um &quot;`!`&quot; no valor de um `property` parâmetro retorna somente objetos onde a propriedade **não** existe. | `property=!name` |
| ~ | Retorna somente objetos cujos valores de propriedade (string) correspondem a uma expressão regular fornecida após o símbolo tilde (`~`). | `property=name~^example` |
| == | Retorna somente objetos cujos valores de propriedade correspondam exatamente à string fornecida após o símbolo duplo igual (`==`). | `property=name==exampleName` |
| != | Retorna somente objetos cujos valores de propriedade **não** correspondem à string fornecida após o símbolo não igual (`!=`). | `property=name!=exampleName` |
| &lt; | Retorna somente objetos cujos valores de propriedade sejam menores que (mas não iguais a) uma quantia informada. | `property=version<1.0.0` |
| &lt;= | Retorna somente objetos cujos valores de propriedade sejam menores que (ou iguais a) uma quantia informada. | `property=version<=1.0.0` |
| > | Retorna somente objetos cujos valores de propriedade sejam maiores que (mas não iguais a) uma quantia informada. | `property=version>1.0.0` |
| >= | Retorna somente objetos cujos valores de propriedade sejam maiores que (ou iguais a) uma quantia informada. | `property=version>=1.0.0` |

>[!NOTE]
>
>A `name` propriedade suporta o uso de um curinga `*`, seja como a string de pesquisa inteira ou como parte dela. Caracteres curingas correspondem a caracteres vazios, de modo que a string de pesquisa `te*st` corresponda ao valor &quot;test&quot;. Os asteriscos são evitados duplicando-os (`**`). Um duplo-asterisco em uma string de pesquisa representa um único asterisco como uma string literal.

**Solicitação**

A solicitação a seguir retornará todos os conjuntos de dados com um número de versão maior que 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de conjuntos de dados cujos números de versão são maiores que 1.0.3. A menos que um limite também seja especificado, a resposta contém um máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Combinar vários filtros

Usando um E comercial (`&`), você pode combinar vários filtros em uma única solicitação. Quando condições adicionais são adicionadas a uma solicitação, uma relação E é assumida.

**Formato da API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
