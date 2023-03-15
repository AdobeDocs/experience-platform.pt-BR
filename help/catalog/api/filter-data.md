---
keywords: Experience Platform;página inicial;tópicos populares;filtro;Filtrar;filtrar dados;Filtrar dados;intervalo de datas;;home;popular topics;filter;filter data;Filter data;date range
solution: Experience Platform
title: Filtrar dados do catálogo usando parâmetros de consulta
description: A API do Serviço de catálogo permite que os dados de resposta sejam filtrados por meio do uso de parâmetros de consulta de solicitação. Parte das práticas recomendadas para o Catálogo é usar filtros em todas as chamadas de API, pois reduzem a carga da API e ajudam a melhorar o desempenho geral.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 2%

---

# Filtro [!DNL Catalog] dados usando parâmetros de consulta

A variável [!DNL Catalog Service] A API permite que os dados de resposta sejam filtrados por meio do uso de parâmetros de consulta de solicitação. Parte das práticas recomendadas para [!DNL Catalog] O é usar filtros em todas as chamadas de API, pois eles reduzem a carga da API e ajudam a melhorar o desempenho geral.

Este documento descreve os métodos mais comuns para filtragem [!DNL Catalog] objetos na API. É recomendável que você consulte este documento ao ler a [Guia do desenvolvedor do catálogo](getting-started.md) para saber mais sobre como interagir com o [!DNL Catalog] API. Para obter informações mais gerais sobre [!DNL Catalog Service], consulte o [[!DNL Catalog] visão geral](../home.md).

## Limitar objetos retornados

A variável `limit` o parâmetro de consulta restringe o número de objetos retornados em uma resposta. [!DNL Catalog] as respostas são medidas automaticamente de acordo com os limites configurados:

* Se um `limit` parâmetro não especificado, o número máximo de objetos por carga de resposta é 20.
* Para consultas do conjunto de dados, se `observableSchema` é solicitado usando o `properties` parâmetro de consulta, o número máximo de conjuntos de dados retornados é 20.
* O limite global para todas as outras consultas do catálogo é de 100 objetos.
* Inválido `limit` parâmetros (incluindo `limit=0`) resultam em respostas de erro de nível 400 que descrevem intervalos adequados.
* Os limites ou deslocamentos transmitidos como parâmetros de consulta têm prioridade sobre aqueles transmitidos como cabeçalhos.

**Formato da API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Um número inteiro que indica o número de objetos a serem retornados, variando de 1 a 100. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados enquanto limita a resposta a três objetos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de conjuntos de dados, limitada ao número indicado pela variável `limit` parâmetro de consulta.

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

Mesmo ao filtrar o número de objetos retornados usando o `limit` parâmetro, os próprios objetos retornados geralmente podem conter mais informações do que você realmente precisa. Para reduzir ainda mais a carga no sistema, é prática recomendada filtrar as respostas para incluir apenas as propriedades necessárias.

A variável `properties` os filtros de parâmetro respondem aos objetos para retornar apenas um conjunto de propriedades especificadas. O parâmetro pode ser definido para retornar uma ou várias propriedades.

A variável `properties` O parâmetro só aceita propriedades de objeto de nível superior, o que significa que, para o seguinte objeto de amostra, é possível aplicar filtros para `name`, `description`, e `subItem`, mas NÃO para `sampleKey`.

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
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | O nome de um atributo a ser incluído no corpo da resposta. |
| `{OBJECT_ID}` | O identificador exclusivo de um [!DNL Catalog] objeto sendo recuperado. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados. A lista separada por vírgulas de nomes de propriedades fornecida sob o `properties` indica as propriedades a serem retornadas na resposta. A `limit` também está incluído, o que limita o número de conjuntos de dados retornados. Se o pedido não tiver incluído uma `limit` , a resposta conteria no máximo 20 objetos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Com base na resposta acima, pode-se inferir o seguinte:

* Se um objeto não tiver nenhuma propriedade solicitada, ele mostrará somente as propriedades solicitadas que ele não inclui. (`Dataset1`)
* Se um objeto não incluir nenhuma das propriedades solicitadas, ele aparecerá como um objeto vazio. (`Dataset2`)
* Um conjunto de dados pode retornar uma propriedade solicitada como um objeto vazio se ele contiver a propriedade, mas não houver um valor. (`Dataset3`)
* Caso contrário, o conjunto de dados exibirá o valor completo de todas as propriedades solicitadas. (`Dataset4`)

>[!NOTE]
>
>No `schemaRef` para cada conjunto de dados, o número da versão indica a versão secundária mais recente do esquema. Consulte a seção sobre [controle de versão do esquema](../../xdm/api/getting-started.md#versioning) no guia API XDM para obter mais informações.

## Índice de início de deslocamento da lista de respostas

A variável `start` o parâmetro de consulta desloca a lista de respostas em direção a um número especificado, usando uma numeração baseada em zero. Por exemplo, `start=2` deslocaria a resposta para iniciar no terceiro objeto listado.

Se a variável `start` o parâmetro não está emparelhado com um `limit` parâmetro, o número máximo de objetos retornados é 20.

**Formato da API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto de Catálogo a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Um número inteiro que indica o número de objetos para deslocar a resposta. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, deslocando para o quinto objeto (`start=4`) e limitando a resposta a dois conjuntos de dados retornados (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta inclui um objeto JSON que contém dois itens de nível superior (`limit=2`), um para cada conjunto de dados e seus detalhes (os detalhes foram condensados no exemplo). A resposta é deslocada em quatro (`start=4`), o que significa que os conjuntos de dados mostrados são números cinco e seis cronologicamente.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrar por tag

Alguns objetos do Catálogo suportam o uso de um `tags` atributo. As tags podem anexar informações a um objeto e ser usadas posteriormente para recuperá-lo. A escolha de quais tags usar e como aplicá-las depende dos processos organizacionais.

Há algumas limitações a serem consideradas ao usar tags:

* Os únicos objetos do Catálogo que atualmente oferecem suporte a tags são conjuntos de dados, lotes e conexões.
* Os nomes de tag são exclusivos de sua Organização IMS.
* Os processos de Adobe podem aproveitar as tags para determinados comportamentos. Os nomes dessas tags recebem o prefixo &quot;adobe&quot; como padrão. Portanto, você deve evitar essa convenção ao declarar nomes de tag.
* Os seguintes nomes de tag são reservados para uso em [!DNL Experience Platform]e, portanto, não pode ser declarado como um nome de tag para sua organização:
   * `unifiedProfile`: este nome de tag é reservado para conjuntos de dados que serão assimilados pelo [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: este nome de tag é reservado para conjuntos de dados que serão assimilados pelo [[!DNL Identity Service]](../../identity-service/home.md).

Veja abaixo um exemplo de um conjunto de dados que contém uma `tags` propriedade. As tags nessa propriedade assumem a forma de pares de valores chave, com cada valor de tag aparecendo como uma matriz contendo uma única string:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
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

Valores para o `tags` assumem a forma de pares de valores chave, usando o formato `{TAG_NAME}:{TAG_VALUE}`. Vários pares de valores-chave podem ser fornecidos no formato de uma lista separada por vírgulas. Quando várias tags são fornecidas, uma relação AND é presumida.

O parâmetro aceita caracteres curingas (`*`) para valores de tag. Por exemplo, uma string de pesquisa de `test*` retorna qualquer objeto no qual o valor da tag comece com &quot;test&quot;. Uma string de pesquisa que consiste apenas em um curinga pode ser usada para filtrar objetos com base no fato de eles conterem ou não uma tag específica, independentemente do valor.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | O nome da tag pela qual filtrar. |
| `{TAG_VALUE}` | O valor da tag pela qual filtrar. Suporta caracteres curingas (`*`). |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, filtrando por uma tag com um valor específico E a segunda tag presente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de conjuntos de dados que contêm `sampleTag` com um valor de &quot;123456&quot;, E `secondTag` com qualquer valor. A menos que um limite também seja especificado, a resposta conterá no máximo 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

Alguns endpoints no [!DNL Catalog] As APIs têm parâmetros de consulta que permitem consultas por intervalo, com mais frequência no caso de datas.

**Formato da API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{TIMESTAMP }` | Um inteiro datetime no horário Unix. |

**Solicitação**

A solicitação a seguir recupera uma lista de lotes criados durante o mês de abril de 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de [!DNL Catalog] objetos que estão dentro do intervalo de datas especificado. A menos que um limite também seja especificado, a resposta conterá no máximo 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

A variável `orderBy` o parâmetro de consulta permite classificar (ordenar) dados de resposta com base em um valor de propriedade especificado. Este parâmetro requer uma &quot;direção&quot; (`asc` para ascendente ou `desc` para decrescente), seguido por dois pontos (`:`) e, em seguida, uma propriedade para classificar os resultados. Se uma direção não for especificada, a direção padrão será ascendente.

Várias propriedades de classificação podem ser fornecidas em uma lista separada por vírgulas. Se a primeira propriedade de classificação produzir vários objetos que contêm o mesmo valor para essa propriedade, a segunda propriedade de classificação será usada para classificar ainda mais esses objetos correspondentes.

Por exemplo, considere a seguinte query: `orderBy=name,desc:created`. Os resultados são classificados em ordem crescente com base na primeira propriedade de classificação, `name`. Nos casos em que vários registros compartilham a mesma `name` propriedade, esses registros correspondentes são classificados pela segunda propriedade de classificação, `created`. Se nenhum registro retornado compartilhar o mesmo `name`, o `created` propriedade não leva em consideração na classificação.


**Formato da API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto de Catálogo a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | O nome de uma propriedade pela qual classificar os resultados. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados classificados por `name` propriedade. Se qualquer conjunto de dados compartilhar a mesma `name`, esses conjuntos de dados serão, por sua vez, ordenados por seus `updated` propriedade em ordem decrescente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de [!DNL Catalog] objetos que são classificados de acordo com a `orderBy` parâmetro. A menos que um limite também seja especificado, a resposta conterá no máximo 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

[!DNL Catalog] O fornece dois métodos de filtragem por propriedade, que são descritos mais detalhadamente nas seções a seguir:

* [Utilização de filtros simples](#using-simple-filters): filtre se uma propriedade específica corresponde a um valor específico.
* [Uso do parâmetro de propriedade](#using-the-property-parameter): use expressões condicionais para filtrar com base na existência de uma propriedade ou se o valor de uma propriedade corresponder, se aproximar ou se comparar a outro valor ou expressão regular especificada.

### Utilização de filtros simples {#using-simple-filters}

Filtros simples permitem filtrar respostas com base em valores de propriedade específicos. Um filtro simples assume a forma de `{PROPERTY_NAME}={VALUE}`.

Por exemplo, a query `name=exampleName` retorna somente objetos cujos `name` contém um valor de &quot;exampleName&quot;. Em contrapartida, a questão `name=!exampleName` retorna somente objetos cujos `name` propriedade é **não** &quot;exampleName&quot;.

Além disso, filtros simples suportam a capacidade de consultar vários valores para uma única propriedade. Quando vários valores são fornecidos, a resposta retorna objetos cuja propriedade corresponde **qualquer** dos valores na lista fornecida. É possível inverter uma consulta de vários valores prefixando um `!` caractere para a lista, retornando somente objetos cujo valor de propriedade é **não** na lista fornecida (por exemplo, `name=!exampleName,anotherName`).

**Formato da API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | O nome da propriedade cujo valor você deseja filtrar. |
| `{VALUE}` | Um valor de propriedade que determina quais resultados incluir (ou excluir, dependendo da consulta). |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, filtrados para incluir somente conjuntos de dados cujos `name` tem um valor de &quot;exampleName&quot; ou &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de conjuntos de dados, excluindo todos os conjuntos de dados cujos `name` é &quot;exampleName&quot; ou &quot;anotherName&quot;. A menos que um limite também seja especificado, a resposta conterá no máximo 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

### Usar o `property` parâmetro {#using-the-property-parameter}

A variável `property` o parâmetro de consulta fornece mais flexibilidade para a filtragem baseada em propriedades do que filtros simples. Além da filtragem baseada no fato de uma propriedade ter um valor específico, a variável `property` parâmetro pode usar outros operadores de comparação (como &quot;maior que&quot; (`>`) e &quot;menor que&quot; (`<`), bem como expressões regulares para filtrar por valores de propriedade. Também pode filtrar se uma propriedade existe ou não, independentemente do seu valor.

A variável `property` O parâmetro só aceita propriedades de objeto de nível superior, o que significa que, para o seguinte objeto de amostra, você pode filtrar por propriedade para `name`, `description`, e `subItem`, mas NÃO para `sampleKey`.

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
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Uma expressão condicional que indica qual propriedade consultar e como seu valor deve ser avaliado. Os exemplos são fornecidos abaixo. |

O valor de `property` O parâmetro suporta vários tipos diferentes de expressões condicionais. A tabela a seguir descreve a sintaxe básica para expressões suportadas:

| Símbolo(s) | Descrição | Exemplo |
| --- | --- | --- |
| (None) | Declarar o nome da propriedade sem operador retorna somente objetos nos quais a propriedade existe, independentemente do seu valor. | `property=name` |
| ! | Prefixo de um &quot;`!`&quot; ao valor de um `property` O parâmetro retorna somente objetos nos quais a propriedade retorna **não** existe. | `property=!name` |
| ~ | Retorna somente objetos cujos valores de propriedade (string) correspondam a uma expressão regular fornecida após o til (`~`). | `property=name~^example` |
| == | Retorna somente objetos cujos valores de propriedade correspondam exatamente à cadeia de caracteres fornecida após o símbolo duplo de igual (`==`). | `property=name==exampleName` |
| != | Retorna apenas objetos cujos valores de propriedade **não** string de correspondência fornecida após o símbolo diferente de (`!=`). | `property=name!=exampleName` |
| &lt; | Retorna apenas objetos cujos valores de propriedade sejam menores que (mas não iguais a) um valor declarado. | `property=version<1.0.0` |
| &lt;= | Retorna apenas objetos cujos valores de propriedade sejam menores que (ou iguais a) um valor declarado. | `property=version<=1.0.0` |
| > | Retorna apenas objetos cujos valores de propriedade sejam maiores que (mas não iguais a) um valor declarado. | `property=version>1.0.0` |
| >= | Retorna apenas objetos cujos valores de propriedade sejam maiores que (ou iguais a) uma quantidade declarada. | `property=version>=1.0.0` |

>[!NOTE]
>
>A variável `name` suporta o uso de um curinga `*`, como toda a cadeia de caracteres de pesquisa ou como parte dela. Os curingas correspondem a caracteres vazios, de modo que a sequência de caracteres de pesquisa `te*st` corresponderá ao valor &quot;test&quot;. Os asteriscos são evitados ao serem duplicados (`**`). Um asterisco duplo em uma string de pesquisa representa um único asterisco como uma string literal.

**Solicitação**

A solicitação a seguir retornará qualquer conjunto de dados com um número de versão superior a 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de conjuntos de dados cujos números de versão são maiores que 1.0.3. A menos que um limite também seja especificado, a resposta conterá no máximo 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

Uso de um E comercial (`&`), é possível combinar vários filtros em uma única solicitação. Quando condições adicionais são adicionadas a uma solicitação, uma relação AND é presumida.

**Formato da API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
