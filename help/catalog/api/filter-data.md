---
keywords: Experience Platform, home, tópicos populares, filtro, filtro, filtrar dados, filtrar dados, intervalo de datas
solution: Experience Platform
title: Filtrar dados do catálogo usando parâmetros de consulta
topic-legacy: developer guide
description: A API do Serviço de catálogo permite que os dados de resposta sejam filtrados por meio do uso de parâmetros de consulta de solicitação. Parte das práticas recomendadas para o Catálogo é usar filtros em todas as chamadas de API, pois eles reduzem a carga na API e ajudam a melhorar o desempenho geral.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 2%

---

# Filtro [!DNL Catalog] dados que usam parâmetros de consulta

O [!DNL Catalog Service] A API permite que os dados de resposta sejam filtrados por meio do uso de parâmetros de solicitação de consulta. Parte das práticas recomendadas para [!DNL Catalog] O é usar filtros em todas as chamadas de API, pois eles reduzem a carga na API e ajudam a melhorar o desempenho geral.

Este documento descreve os métodos mais comuns para filtragem [!DNL Catalog] na API. É recomendável fazer referência a este documento ao ler o [Guia do desenvolvedor do catálogo](getting-started.md) para saber mais sobre como interagir com o [!DNL Catalog] API. Para obter informações mais gerais sobre [!DNL Catalog Service], consulte o [[!DNL Catalog] visão geral](../home.md).

## Limitar objetos retornados

O `limit` parâmetro de consulta restringe o número de objetos retornados em uma resposta. [!DNL Catalog] as respostas são medidas automaticamente de acordo com os limites configurados:

* Se uma `limit` não for especificado, o número máximo de objetos por carga de resposta é 20.
* Para consultas de conjunto de dados, se `observableSchema` é solicitado usando o `properties` parâmetro de consulta , o número máximo de conjuntos de dados retornados é 20.
* O limite global para todas as outras consultas do Catálogo é de 100 objetos.
* Inválido `limit` parâmetros (incluindo `limit=0`) resulta em respostas de erro em nível de 400 que destacam intervalos adequados.
* Os limites ou deslocamentos passados como parâmetros de consulta têm prioridade sobre aqueles que são passados como cabeçalhos.

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

Mesmo ao filtrar o número de objetos retornados usando a variável `limit` , os próprios objetos retornados geralmente podem conter mais informações do que você realmente precisa. Para reduzir ainda mais a carga no sistema, é uma prática recomendada filtrar respostas para incluir apenas as propriedades necessárias.

O `properties` O parâmetro filtra objetos de resposta para retornar somente um conjunto de propriedades especificadas. O parâmetro pode ser definido para retornar uma ou várias propriedades.

O `properties` aceita apenas propriedades de objetos de nível superior, o que significa que para o seguinte objeto de amostra, você pode aplicar filtros para `name`, `description`e `subItem`, mas NÃO para `sampleKey`.

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

A solicitação a seguir recupera uma lista de conjuntos de dados. A lista separada por vírgulas de nomes de propriedades fornecida no `properties` indica as propriedades a serem retornadas na resposta. A `limit` também é incluído, o que limita o número de conjuntos de dados retornados. Se a solicitação não tiver incluído um `limit` , a resposta conteria no máximo 20 objetos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de [!DNL Catalog] objetos com apenas as propriedades solicitadas.

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

Com base na resposta acima, o seguinte pode ser inferido:

* Se um objeto não tiver nenhuma propriedade solicitada, ele só mostrará as propriedades solicitadas que ele incluir. (`Dataset1`)
* Se um objeto não incluir nenhuma das propriedades solicitadas, ele aparecerá como um objeto vazio. (`Dataset2`)
* Um conjunto de dados pode retornar uma propriedade solicitada como um objeto vazio se ela contiver a propriedade, mas não houver valor. (`Dataset3`)
* Caso contrário, o conjunto de dados exibirá o valor total de todas as propriedades solicitadas. (`Dataset4`)

>[!NOTE]
>
>No `schemaRef` para cada conjunto de dados, o número da versão indica a versão secundária mais recente do esquema. Consulte a seção sobre [versão do schema](../../xdm/api/getting-started.md#versioning) no guia da API XDM para obter mais informações.

## Índice inicial de compensação da lista de resposta

O `start` O parâmetro de consulta desloca a lista de resposta para frente por um número especificado, usando a numeração baseada em zero. Por exemplo, `start=2` compensaria a resposta para iniciar no terceiro objeto listado.

Se a variável `start` não está emparelhado com um `limit` , o número máximo de objetos retornados é 20.

**Formato da API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto Catálogo a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Um número inteiro que indica o número de objetos para deslocar a resposta. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, compensando para o quinto objeto (`start=4`) e limitando a resposta a dois conjuntos de dados retornados (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta inclui um objeto JSON contendo dois itens de nível superior (`limit=2`), um para cada conjunto de dados e seus detalhes (os detalhes foram condensados no exemplo). A resposta é alterada em quatro (`start=4`), o que significa que os conjuntos de dados mostrados são os cinco e seis cronologicamente.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrar por tag

Alguns objetos de catálogo oferecem suporte para o uso de um `tags` atributo. As tags podem anexar informações a um objeto e, em seguida, ser usadas posteriormente para recuperar esse objeto. A escolha de quais tags usar e como aplicá-las depende de seus processos organizacionais.

Há algumas limitações a serem consideradas ao usar tags:

* Os únicos objetos do Catálogo que atualmente suportam tags são conjuntos de dados, lotes e conexões.
* Nomes de tag são exclusivos de sua organização IMS.
* Os processos do Adobe podem aproveitar as tags para determinados comportamentos. Os nomes dessas tags recebem o prefixo &quot;adobe&quot; como padrão. Portanto, você deve evitar essa convenção ao declarar nomes de tags.
* Os seguintes nomes de tag são reservados para uso em [!DNL Experience Platform]e, portanto, não pode ser declarado como um nome de tag para sua organização:
   * `unifiedProfile`: Esse nome de tag é reservado para que os conjuntos de dados sejam assimilados por [[!DNL Real-time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: Esse nome de tag é reservado para que os conjuntos de dados sejam assimilados por [[!DNL Identity Service]](../../identity-service/home.md).

Abaixo está um exemplo de um conjunto de dados que contém um `tags` propriedade. As tags dessa propriedade assumem a forma de pares de valores chave, com cada valor de tag exibido como uma matriz contendo uma única string:

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

Valores para o `tags` assume a forma de pares de valores chave, usando o formato `{TAG_NAME}:{TAG_VALUE}`. Vários pares de valores chave podem ser fornecidos na forma de uma lista separada por vírgulas. Quando várias tags são fornecidas, uma relação AND é assumida.

O parâmetro suporta caracteres curingas (`*`) para valores de tag. Por exemplo, uma string de pesquisa de `test*` retorna qualquer objeto no qual o valor da tag começa com &quot;teste&quot;. Uma string de pesquisa que consiste apenas em um curinga pode ser usada para filtrar objetos com base no fato de eles conterem ou não uma tag específica, independentemente do seu valor.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de [!DNL Catalog] objeto a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | O nome da tag para filtrar. |
| `{TAG_VALUE}` | O valor da tag para filtrar. Suporta caracteres curingas (`*`). |

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

Uma resposta bem-sucedida retorna uma lista de conjuntos de dados que contêm `sampleTag` com um valor de &quot;123456&quot;, E `secondTag` com qualquer valor. A menos que um limite também seja especificado, a resposta conterá um máximo de 20 objetos.

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

Alguns endpoints no [!DNL Catalog] As APIs têm parâmetros de consulta que permitem consultas variadas, na maioria das vezes no caso de datas.

**Formato da API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{TIMESTAMP }` | Um número inteiro de data e hora na época Unix. |

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

Uma resposta bem-sucedida contém uma lista de [!DNL Catalog] objetos que estão dentro do intervalo de datas especificado. A menos que um limite também seja especificado, a resposta conterá um máximo de 20 objetos.

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

O `orderBy` O parâmetro de consulta permite classificar dados de resposta (ordem) com base em um valor de propriedade especificado. Esse parâmetro requer uma &quot;direção&quot; (`asc` em ordem crescente ou `desc` para decrescente), seguido por dois pontos (`:`) e, em seguida, uma propriedade para classificar os resultados. Se uma direção não for especificada, a direção padrão será crescente.

Várias propriedades de classificação podem ser fornecidas em uma lista separada por vírgulas. Se a primeira propriedade de classificação produzir vários objetos que contenham o mesmo valor para essa propriedade, a segunda propriedade de classificação será usada para classificar ainda mais os objetos correspondentes.

Por exemplo, considere a seguinte consulta: `orderBy=name,desc:created`. Os resultados são classificados em ordem crescente com base na primeira propriedade de classificação, `name`. Nos casos em que vários registros compartilham o mesmo `name` , esses registros correspondentes são classificados pela segunda propriedade de classificação, `created`. Se nenhum registro retornado compartilhar o mesmo `name`, o `created` não afeta a classificação.


**Formato da API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto Catálogo a ser recuperado. Os objetos válidos são: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | O nome de uma propriedade para classificar os resultados. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados classificados por seus `name` propriedade. Se qualquer conjunto de dados compartilhar o mesmo `name`, esses conjuntos de dados, por sua vez, serão ordenados por seus `updated` em ordem decrescente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de [!DNL Catalog] objetos que são classificados de acordo com a variável `orderBy` parâmetro. A menos que um limite também seja especificado, a resposta conterá um máximo de 20 objetos.

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

* [Uso de filtros simples](#using-simple-filters): Filtre se uma propriedade específica corresponde a um valor específico.
* [Uso do parâmetro de propriedade](#using-the-property-parameter): Use expressões condicionais para filtrar com base em se uma propriedade existe ou se o valor de uma propriedade corresponde, se aproxima ou se compara a outro valor especificado ou a outra expressão regular.

### Uso de filtros simples {#using-simple-filters}

Filtros simples permitem filtrar respostas com base em valores de propriedade específicos. Um filtro simples assume a forma de `{PROPERTY_NAME}={VALUE}`.

Por exemplo, o query `name=exampleName` retorna somente objetos cujo `name` contém um valor de &quot;exampleName&quot;. Por outro lado, o query `name=!exampleName` retorna somente objetos cujo `name` a propriedade é **not** &quot;exampleName&quot;.

Além disso, filtros simples oferecem suporte à capacidade de consultar vários valores para uma única propriedade. Quando vários valores são fornecidos, a resposta retorna objetos cuja propriedade corresponde a **any** dos valores na lista fornecida. Você pode inverter um query de vários valores prefixando um `!` para a lista, retornando somente objetos cujo valor de propriedade é **not** na lista fornecida (por exemplo, `name=!exampleName,anotherName`).

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
| `{VALUE}` | Um valor de propriedade que determina quais resultados incluir (ou excluir, dependendo da query). |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, filtrada para incluir somente conjuntos de dados cujo `name` tem um valor de &quot;exampleName&quot; ou &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de conjuntos de dados, excluindo qualquer conjunto de dados cujo `name` é &quot;exampleName&quot; ou &quot;anotherName&quot;. A menos que um limite também seja especificado, a resposta conterá um máximo de 20 objetos.

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

O `property` o parâmetro de consulta fornece mais flexibilidade para a filtragem baseada em propriedade do que os filtros simples. Além da filtragem com base em se uma propriedade tem um valor específico, a variável `property` pode usar outros operadores de comparação (como &quot;mais do que&quot; (`>`) e &quot;menor que&quot; (`<`)), bem como expressões regulares para filtrar por valores de propriedade. Ela também pode filtrar se uma propriedade existe ou não, independentemente do seu valor.

O `property` aceita apenas propriedades de objetos de nível superior, o que significa que para o seguinte objeto de amostra, você pode filtrar por propriedade para `name`, `description`e `subItem`, mas NÃO para `sampleKey`.

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
| `{CONDITION}` | Uma expressão condicional que indica qual propriedade consultar e como seu valor deve ser avaliado. Os exemplos são apresentados abaixo. |

O valor da variável `property` O parâmetro suporta vários tipos diferentes de expressões condicionais. A tabela a seguir descreve a sintaxe básica para expressões suportadas:

| Símbolo(s) | Descrição | Exemplo |
| --- | --- | --- |
| (None) | Indicar o nome da propriedade sem operador retorna somente objetos em que a propriedade existe, independentemente do valor. | `property=name` |
| ! | Prefixar um &quot;`!`&quot; para o valor de um `property` parâmetro retorna somente objetos em que a propriedade retorna **not** existe. | `property=!name` |
| ~ | Retorna apenas objetos cujos valores de propriedade (string) correspondem a uma expressão regular fornecida após o til (`~`). | `property=name~^example` |
| == | Retorna somente objetos cujos valores de propriedade correspondam exatamente à string fornecida após o símbolo de dupla igualdade (`==`). | `property=name==exampleName` |
| != | Retorna somente objetos cujos valores de propriedade **not** string de correspondência fornecida após o símbolo não é igual (`!=`). | `property=name!=exampleName` |
| &lt; | Retorna apenas objetos cujos valores de propriedade sejam inferiores a (mas não iguais a) uma quantia declarada. | `property=version<1.0.0` |
| &lt;= | Retorna apenas objetos cujos valores de propriedade sejam inferiores (ou iguais a) a uma quantia declarada. | `property=version<=1.0.0` |
| > | Retorna apenas objetos cujos valores de propriedade são maiores que (mas não iguais a) uma quantidade declarada. | `property=version>1.0.0` |
| >= | Retorna apenas objetos cujos valores de propriedade sejam maiores que (ou iguais a) uma quantidade declarada. | `property=version>=1.0.0` |

>[!NOTE]
>
>O `name` A propriedade suporta o uso de um curinga `*`, como a string de pesquisa inteira ou como parte dela. Os curingas correspondem a caracteres vazios, de modo que a sequência de pesquisa `te*st` corresponderá ao valor &quot;teste&quot;. Os asteriscos são escapados duplicando-os (`**`). Um asterisco duplo em uma string de pesquisa representa um único asterisco como uma string literal.

**Solicitação**

A solicitação a seguir retornará qualquer conjunto de dados com um número de versão maior que 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de conjuntos de dados cujos números de versão são maiores que 1.0.3. A menos que um limite também seja especificado, a resposta conterá um máximo de 20 objetos.

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

Usar um e comercial (`&`), é possível combinar vários filtros em uma única solicitação. Quando condições adicionais são adicionadas a uma solicitação, um relacionamento E é assumido.

**Formato da API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
