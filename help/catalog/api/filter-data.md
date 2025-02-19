---
keywords: Experience Platform;página inicial;tópicos populares;filtro;Filtrar;filtrar dados;Filtrar dados;intervalo de datas;;home;popular topics;filter;filter data;Filter data;Filter data;date range
solution: Experience Platform
title: Filtrar dados do catálogo usando parâmetros de consulta
description: Use parâmetros de consulta para filtrar dados de resposta na API do Serviço de catálogo e recuperar apenas as informações necessárias. Aplique filtros às chamadas de API para reduzir a carga e melhorar o desempenho, garantindo uma recuperação de dados mais rápida e eficiente.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 14ecb971af3f6cdcc605caa05ef6609ecb9b38fd
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 2%

---

# Filtrar dados [!DNL Catalog] usando parâmetros de consulta

Para melhorar o desempenho e recuperar resultados relevantes, use parâmetros de consulta para filtrar os dados de resposta da API [!DNL Catalog Service].

Saiba mais sobre métodos de filtragem comuns para [!DNL Catalog] objetos na API. Use este documento junto com o [Guia do Desenvolvedor do Catálogo](getting-started.md) para obter mais detalhes sobre as interações da API. Para obter informações gerais sobre [!DNL Catalog Service], consulte a [[!DNL Catalog] visão geral](../home.md).

## Limitar objetos retornados {#limit-returned-objects}

O parâmetro de consulta `limit` restringe o número de objetos retornados em uma resposta. [!DNL Catalog] respostas seguem limites predefinidos:

* Se o parâmetro `limit` não for especificado, o número máximo de objetos por resposta será 20.
* Para consultas de conjunto de dados, se `observableSchema` for solicitado usando o parâmetro de consulta `properties`, o número máximo de conjuntos de dados retornados será 20.
* Para tokens de usuário, o limite máximo é 1.
* Para tokens de serviço, o limite máximo é 20.
* O limite global para outras consultas do Catálogo é de 100 objetos.
* Valores de `limit` inválidos (incluindo `limit=0`) resultam em respostas de erro de nível 400 especificando intervalos adequados.
* Os limites ou deslocamentos transmitidos como parâmetros de consulta têm prioridade sobre aqueles em cabeçalhos.

**Formato da API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser recuperado. Objetos válidos: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | Um número inteiro que especifica o número de objetos a serem retornados (intervalo: 1-100). |

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

Uma resposta bem-sucedida retorna uma lista de conjuntos de dados, limitada ao número indicado pelo parâmetro de consulta `limit`.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Limitar propriedades exibidas {#limit-displayed-properties}

Mesmo ao filtrar o número de objetos retornados usando o parâmetro `limit`, os próprios objetos retornados geralmente podem conter mais informações do que você realmente precisa. Para reduzir ainda mais a carga no sistema, é prática recomendada filtrar as respostas para incluir apenas as propriedades necessárias.

O parâmetro `properties` filtra objetos de resposta para retornar apenas um conjunto de propriedades especificadas. O parâmetro pode ser definido para retornar uma ou várias propriedades.

O parâmetro `properties` pode aceitar qualquer propriedade de objeto de nível. `sampleKey` pode ser extraído usando `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser recuperado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | O nome de um atributo a ser incluído no corpo da resposta. |
| `{OBJECT_ID}` | O identificador exclusivo de um objeto [!DNL Catalog] específico que está sendo recuperado. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados. A lista separada por vírgulas de nomes de propriedades fornecida sob o parâmetro `properties` indica as propriedades a serem retornadas na resposta. Um parâmetro `limit` também está incluído, o que limita o número de conjuntos de dados retornados. Se a solicitação não incluísse um parâmetro `limit`, a resposta conteria no máximo 20 objetos.

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
>Na propriedade `schemaRef` de cada conjunto de dados, o número da versão indica a versão secundária mais recente do esquema. Consulte a seção sobre [controle de versão do esquema](../../xdm/api/getting-started.md#versioning) no guia da API XDM para obter mais informações.

## Índice de início de deslocamento da lista de respostas {#offset-starting-index}

O parâmetro de consulta `start` desloca a lista de respostas em direção a um número especificado, usando uma numeração baseada em zero. Por exemplo, `start=2` deslocaria a resposta para iniciar no terceiro objeto listado.

Se o parâmetro `start` não estiver emparelhado com um parâmetro `limit`, o número máximo de objetos retornados será 20.

**Formato da API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto de Catálogo a ser recuperado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

A resposta inclui um objeto JSON contendo dois itens de nível superior (`limit=2`), um para cada conjunto de dados e seus detalhes (os detalhes foram condensados no exemplo). A resposta é deslocada em quatro (`start=4`), o que significa que os conjuntos de dados mostrados são os números cinco e seis cronologicamente.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrar por tag

Alguns objetos de Catálogo oferecem suporte ao uso de um atributo `tags`. As tags podem anexar informações a um objeto e ser usadas posteriormente para recuperá-lo. A escolha de quais tags usar e como aplicá-las depende dos processos organizacionais.

Há algumas limitações a serem consideradas ao usar tags:

* Os únicos objetos do Catálogo que atualmente oferecem suporte a tags são conjuntos de dados, lotes e conexões.
* Os nomes das tags são exclusivos de sua organização.
* Os processos do Adobe podem utilizar tags para determinados comportamentos. Os nomes dessas tags recebem o prefixo &quot;adobe&quot; como padrão. Portanto, você deve evitar essa convenção ao declarar nomes de tag.
* Os seguintes nomes de marcas são reservados para uso em [!DNL Experience Platform] e, portanto, não podem ser declarados como um nome de marca para sua organização:
   * `unifiedProfile`: Este nome de marca é reservado para conjuntos de dados a serem assimilados por [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: Este nome de marca é reservado para conjuntos de dados a serem assimilados por [[!DNL Identity Service]](../../identity-service/home.md).

Veja abaixo um exemplo de um conjunto de dados que contém uma propriedade `tags`. As tags nessa propriedade assumem a forma de pares de valores chave, com cada valor de tag aparecendo como uma matriz contendo uma única string:

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

Os valores do parâmetro `tags` tomam a forma de pares de valores chave, usando o formato `{TAG_NAME}:{TAG_VALUE}`. Vários pares de valores-chave podem ser fornecidos no formato de uma lista separada por vírgulas. Quando várias tags são fornecidas, uma relação AND é presumida.

O parâmetro dá suporte a caracteres curingas (`*`) para valores de marca. Por exemplo, uma cadeia de caracteres de pesquisa de `test*` retorna qualquer objeto em que o valor da marca comece com &quot;test&quot;. Uma string de pesquisa que consiste apenas em um curinga pode ser usada para filtrar objetos com base no fato de eles conterem ou não uma tag específica, independentemente do valor.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser recuperado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | O nome da tag pela qual filtrar. |
| `{TAG_VALUE}` | O valor da tag pela qual filtrar. Suporta caracteres curinga (`*`). |

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

Uma resposta bem-sucedida retorna uma lista de conjuntos de dados que contêm `sampleTag` com o valor &quot;123456&quot;, E `secondTag` com qualquer valor. A menos que um limite também seja especificado, a resposta conterá no máximo 20 objetos.

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
    }
}
```

## Filtrar por intervalo de datas

Alguns pontos de extremidade na API [!DNL Catalog] têm parâmetros de consulta que permitem consultas de intervalo, com mais frequência no caso de datas.

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
    }
}
```

## Classificar por propriedade

O parâmetro de consulta `orderBy` permite classificar (ordenar) dados de resposta com base em um valor de propriedade especificado. Este parâmetro requer uma &quot;direção&quot; (`asc` para crescente ou `desc` para decrescente), seguido por dois-pontos (`:`) e uma propriedade para classificar os resultados. Se uma direção não for especificada, a direção padrão será ascendente.

Várias propriedades de classificação podem ser fornecidas em uma lista separada por vírgulas. Se a primeira propriedade de classificação produzir vários objetos que contêm o mesmo valor para essa propriedade, a segunda propriedade de classificação será usada para classificar ainda mais esses objetos correspondentes.

Por exemplo, considere a seguinte consulta: `orderBy=name,desc:created`. Os resultados são classificados em ordem crescente com base na primeira propriedade de classificação, `name`. Nos casos em que vários registros compartilham a mesma propriedade `name`, esses registros correspondentes são classificados pela segunda propriedade de classificação, `created`. Se nenhum registro retornado compartilhar o mesmo `name`, a propriedade `created` não será considerada na classificação.


**Formato da API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto de Catálogo a ser recuperado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | O nome de uma propriedade pela qual classificar os resultados. |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados classificados por sua propriedade `name`. Se algum conjunto de dados compartilhar o mesmo `name`, ele será ordenado por sua propriedade `updated` em ordem decrescente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de [!DNL Catalog] objetos que estão classificados de acordo com o parâmetro `orderBy`. A menos que um limite também seja especificado, a resposta conterá no máximo 20 objetos.

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
    }
}
```

## Filtrar por propriedade

[!DNL Catalog] fornece dois métodos de filtragem por propriedade, que são descritos nas seções a seguir:

* [Uso de filtros simples](#using-simple-filters): filtre se uma propriedade específica corresponde a um valor específico.
* [Usando o parâmetro de propriedade](#using-the-property-parameter): use expressões condicionais para filtrar com base na existência de uma propriedade ou se o valor de uma propriedade corresponder, se aproximar ou se comparar a outro valor ou expressão regular especificada.

>[!NOTE]
>
>Qualquer atributo de um objeto de Catálogo pode ser usado para filtrar resultados na API do serviço de catálogo.

### Utilização de filtros simples {#using-simple-filters}

Filtros simples permitem filtrar respostas com base em valores de propriedade específicos. Um filtro simples toma a forma de `{PROPERTY_NAME}={VALUE}`.

Por exemplo, a consulta `name=exampleName` retorna somente objetos cuja propriedade `name` contenha um valor de &quot;exampleName&quot;. Por outro lado, a consulta `name=!exampleName` retorna somente objetos cuja propriedade `name` é **não** &quot;exampleName&quot;.

Além disso, filtros simples suportam a capacidade de consultar vários valores para uma única propriedade. Quando vários valores são fornecidos, a resposta retorna objetos cuja propriedade corresponde a **qualquer** dos valores na lista fornecida. Você pode inverter uma consulta de vários valores prefixando um caractere `!` à lista, retornando apenas objetos cujo valor de propriedade é **não** na lista fornecida (por exemplo, `name=!exampleName,anotherName`).

**Formato da API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parâmetro | Descrição |
| --- | --- |
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser recuperado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | O nome da propriedade cujo valor você deseja filtrar. |
| `{VALUE}` | Um valor de propriedade que determina quais resultados incluir (ou excluir, dependendo da consulta). |

**Solicitação**

A solicitação a seguir recupera uma lista de conjuntos de dados, filtrada para incluir apenas conjuntos de dados cuja propriedade `name` tenha um valor de &quot;exampleName&quot; ou &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida contém uma lista de conjuntos de dados, excluindo todos os conjuntos de dados cujo `name` seja &quot;exampleName&quot; ou &quot;anotherName&quot;. A menos que um limite também seja especificado, a resposta conterá no máximo 20 objetos.

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
    }
}
```

### Usando o parâmetro `property` {#using-the-property-parameter}

O parâmetro de consulta `property` oferece mais flexibilidade para filtragem baseada em propriedade do que filtros simples. Além de filtrar com base no fato de uma propriedade ter ou não um valor específico, o parâmetro `property` pode usar outros operadores de comparação (como &quot;maior que&quot; (`>`) e &quot;menor que&quot; (`<`)), bem como expressões regulares para filtrar por valores de propriedade. Também pode filtrar se uma propriedade existe ou não, independentemente do seu valor.

Use um E comercial (`&`) para combinar vários filtros e refinar sua consulta em uma única solicitação. Quando você filtra por vários campos, uma relação `AND` é aplicada por padrão.

>[!NOTE]
>
>Se você combinar vários parâmetros `property` em uma única consulta, pelo menos um deve ser aplicado ao campo `id` ou `created`. A consulta a seguir retorna objetos em que `id` é `abc123` **AND** `name` não é `test`:
>
>```http
>GET /datasets?property=id==abc123&property=name!=test
>```

Se você usar vários parâmetros `property` no mesmo campo, somente o último parâmetro especificado entrará em vigor.

>[!IMPORTANT]
>
>Você **não pode** usar um único parâmetro `property` para filtrar vários campos de uma só vez. Cada campo deve ter seu próprio parâmetro `property`. O exemplo a seguir (`property=id>abc,name==myDataset`) é **não** permitido porque ele tenta aplicar condições a `id` e `name` dentro de um **único `property` parâmetro**.

O parâmetro `property` pode aceitar qualquer propriedade de objeto de nível. `sampleKey` pode ser usado para filtragem usando `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | O tipo de objeto [!DNL Catalog] a ser recuperado. Os objetos válidos são: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | Uma expressão condicional que indica qual propriedade consultar e como seu valor deve ser avaliado. Os exemplos são fornecidos abaixo. |

O valor do parâmetro `property` dá suporte a vários tipos diferentes de expressões condicionais. A tabela a seguir descreve a sintaxe básica para expressões suportadas:

| Símbolo(s) | Descrição | Exemplo |
| --- | --- | --- |
| (Nenhum) | Declarar o nome da propriedade sem operador retorna somente objetos nos quais a propriedade existe, independentemente do seu valor. | `property=name` |
| ! | Prefixar um &quot;`!`&quot; ao valor de um parâmetro `property` retorna somente objetos nos quais a propriedade **não** existe. | `property=!name` |
| ~ | Retorna apenas objetos cujos valores de propriedade (cadeia de caracteres) correspondam a uma expressão regular fornecida após o símbolo de til (`~`). | `property=name~^example` |
| == | Retorna apenas objetos cujos valores de propriedade correspondam exatamente à cadeia de caracteres fornecida após o símbolo de igual duplo (`==`). | `property=name==exampleName` |
| != | Retorna somente objetos cujos valores de propriedade correspondam **não** à cadeia de caracteres fornecida após o símbolo diferente (`!=`). | `property=name!=exampleName` |
| &lt; | Retorna apenas objetos cujos valores de propriedade sejam menores que (mas não iguais a) um valor declarado. | `property=version<1.0.0` |
| &lt;= | Retorna apenas objetos cujos valores de propriedade sejam menores que (ou iguais a) um valor declarado. | `property=version<=1.0.0` |
| > | Retorna apenas objetos cujos valores de propriedade sejam maiores que (mas não iguais a) um valor declarado. | `property=version>1.0.0` |
| >= | Retorna apenas objetos cujos valores de propriedade sejam maiores que (ou iguais a) uma quantidade declarada. | `property=version>=1.0.0` |
| * | Um curinga se aplica a qualquer propriedade de string e corresponde a qualquer sequência de caracteres. Use `**` para escapar um asterisco literal. | `property=name==te*st` |
| &amp; | Combina vários parâmetros `property` com uma relação `AND` entre eles. | `property=id==abc&property=name!=test` |

>[!NOTE]
>
>A propriedade `name` dá suporte ao uso de um curinga `*`, como a cadeia de caracteres de pesquisa inteira ou como parte dela. Os curingas correspondem a caracteres vazios, de modo que a cadeia de caracteres de pesquisa `te*st` corresponderá ao valor &quot;test&quot;. Os asteriscos são escapados duplicando-os (`**`). Um asterisco duplo em uma string de pesquisa representa um único asterisco como uma string literal.

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
    }
}
```

## Filtrar matrizes com o parâmetro de propriedade {#filter-arrays}

Use operadores de igualdade e desigualdade para incluir ou excluir valores específicos ao filtrar resultados com base em propriedades de matriz.

### Filtros de igualdade {#equality-filters}

Para filtrar um campo de matriz por vários valores, use parâmetros de propriedade separados para cada valor. Use filtros de igualdade para retornar somente as entradas nos dados da matriz que correspondem aos valores especificados.

>[!NOTE]
>
>O requisito de incluir `id` ou `created` ao filtrar vários campos **não** se aplica ao filtrar vários valores dentro de um campo de matriz.

A consulta de exemplo abaixo retorna apenas resultados da matriz que inclui `val1` e `val2`.

**Formato da API**

```http
GET /{OBJECT_TYPE}?property=arrayField=val1&property=arrayField=val2
```

### Filtros de desigualdade {#inequality-filters}

Use operadores de desigualdade (`!=`) em um campo de matriz para excluir entradas nos dados em que a matriz contém os valores especificados.

**Formato da API**

```http
GET /{OBJECT_TYPE}?property=arrayField!=val1&property=arrayField!=val2
```

Esta consulta retorna documentos em que arrayField não contém `val1` ou `val2`.

### Limitações do filtro de igualdade e desigualdade {#equality-inequality-limitations}

Você não pode aplicar a igualdade (`=`) e a desigualdade (`!=`) ao mesmo campo em uma única consulta.
