---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Gerenciar rótulos de uso de dados usando APIs '
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 3%

---


# Gerenciar rótulos de uso de dados usando APIs

Este documento fornece etapas sobre como gerenciar rótulos de uso de dados usando a [!DNL Policy Service] API e a [!DNL Dataset Service] API.

O [!DNL Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) fornece vários pontos de extremidade que permitem criar e gerenciar rótulos de uso de dados para sua organização.

A [!DNL Dataset Service] API permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados Adobe Experience Platform, mas é separada da [!DNL Catalog Service] API que gerencia os metadados do conjunto de dados.

## Introdução

Antes de ler este guia, siga as etapas descritas na seção [](../../catalog/api/getting-started.md) Introdução no guia do desenvolvedor do Catálogo para coletar as credenciais necessárias para fazer chamadas para [!DNL Platform] APIs.

Para fazer chamadas para os [!DNL Dataset Service] pontos de extremidade contornados neste documento, é necessário ter o `id` valor exclusivo para um conjunto de dados específico. Se você não tiver esse valor, consulte o guia na [listagem de objetos](../../catalog/api/list-objects.md) de Catálogo para localizar as IDs de seus conjuntos de dados existentes.

## Lista de todas as etiquetas {#list-labels}

Usando a [!DNL Policy Service] API, você pode lista todos os rótulos `core` ou `custom` rótulos, fazendo uma solicitação de GET para `/labels/core` ou `/labels/custom`, respectivamente.

**Formato da API**

```http
GET /labels/core
GET /labels/custom
```

**Solicitação**

A solicitação a seguir lista todos os rótulos personalizados criados em sua organização.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de rótulos personalizados recuperados do sistema. Como a solicitação de exemplo acima foi feita para `/labels/custom`, a resposta abaixo mostra somente rótulos personalizados.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Procurar uma etiqueta {#look-up-label}

Você pode procurar um rótulo específico incluindo a propriedade desse rótulo no caminho de uma solicitação de GET para a `name` [!DNL Policy Service] API.

**Formato da API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LABEL_NAME}` | A `name` propriedade do rótulo personalizado que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera o rótulo personalizado `L2`, conforme indicado no caminho.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do rótulo personalizado.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Criar ou atualizar um rótulo personalizado {#create-update-label}

Para criar ou atualizar um rótulo personalizado, é necessário fazer uma solicitação PUT para a [!DNL Policy Service] API.

**Formato da API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LABEL_NAME}` | A `name` propriedade de um rótulo personalizado. Se um rótulo personalizado com esse nome não existir, um novo rótulo será criado. Se existir, esse rótulo será atualizado. |

**Solicitação**

A solicitação a seguir cria um novo rótulo, `L3`que tem como objetivo descrever os dados que contêm informações relacionadas aos planos de pagamento selecionados dos clientes.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | Um identificador de string exclusivo para o rótulo. Esse valor é usado para fins de pesquisa e aplicação do rótulo a conjuntos de dados e campos, portanto, recomenda-se que seja curto e conciso. |
| `category` | A categoria da etiqueta. Embora você possa criar suas próprias categorias para rótulos personalizados, é altamente recomendável usar `Custom` se quiser que o rótulo apareça na interface do usuário. |
| `friendlyName` | Um nome amigável para o rótulo, usado para fins de exibição. |
| `description` | (Opcional) Uma descrição do rótulo para fornecer mais contexto. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do rótulo personalizado, com o código HTTP 200 (OK) se um rótulo existente foi atualizado, ou 201 (Criado) se um novo rótulo foi criado.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Procurar rótulos para um conjunto de dados {#look-up-dataset-labels}

Você pode pesquisar os rótulos de uso de dados que foram aplicados a um conjunto de dados existente, fazendo uma solicitação de GET para a [!DNL Dataset Service] API.

**Formato da API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O `id` valor exclusivo do conjunto de dados cujos rótulos você deseja pesquisar. |

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os rótulos de uso de dados que foram aplicados ao conjunto de dados.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `labels` | Uma lista de rótulos de uso de dados que foram aplicados ao conjunto de dados. |
| `optionalLabels` | Uma lista de campos individuais no conjunto de dados que têm rótulos de uso de dados aplicados a eles. |

## Aplicar rótulos a um conjunto de dados {#apply-dataset-labels}

Você pode criar um conjunto de rótulos para um conjunto de dados, fornecendo-os na carga de uma solicitação de POST ou PUT para a [!DNL Dataset Service] API. O uso de qualquer um desses métodos substitui quaisquer rótulos existentes e os substitui pelos fornecidos na carga.

**Formato da API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O `id` valor exclusivo do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

A solicitação de POST a seguir adiciona uma série de rótulos ao conjunto de dados, bem como um campo específico nesse conjunto de dados. Os campos fornecidos na carga são os mesmos que seriam necessários para uma solicitação de PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `labels` | Uma lista de rótulos de uso de dados que você deseja adicionar ao conjunto de dados. |
| `optionalLabels` | Uma lista de qualquer campo individual no conjunto de dados ao qual você deseja adicionar rótulos. Cada item nesta matriz deve ter as seguintes propriedades: <br/><br/>`option`: Um objeto que contém os atributos [!DNL Experience Data Model] (XDM) do campo. As três propriedades a seguir são obrigatórias:<ul><li>id</code>: O valor URI $id</code> do schema associado ao campo.</li><li>contentType</code>: O tipo de conteúdo e o número da versão do schema. Isso deve assumir a forma de um dos cabeçalhos <a href="../../xdm/api/look-up-resource.md">Accept válidos</a> para uma solicitação de pesquisa XDM.</li><li>schemaPath</code>: O caminho para o campo dentro do schema do conjunto de dados.</li></ul>`labels`: Uma lista de rótulos de uso de dados que você deseja adicionar ao campo. |

**Resposta**

Uma resposta bem-sucedida retorna os rótulos que foram adicionados ao conjunto de dados.

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## Remover rótulos de um conjunto de dados {#remove-dataset-labels}

Você pode remover os rótulos aplicados a um conjunto de dados, fazendo uma solicitação de DELETE para a [!DNL Dataset Service] API.

**Formato da API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O `id` valor exclusivo do conjunto de dados cujos rótulos você deseja remover. |

**Solicitação**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta com êxito HTTP status 200 (OK), indicando que os rótulos foram removidos. Você pode [procurar os rótulos](#look-up-dataset-labels) existentes para o conjunto de dados em uma chamada separada para confirmar isso.

## Próximas etapas

Ao ler este documento, você aprendeu a gerenciar rótulos de uso de dados usando APIs.

Depois de adicionar rótulos de uso de dados no nível do conjunto de dados e do campo, você pode começar a assimilar dados em [!DNL Experience Platform]. Para saber mais, leia a documentação [de ingestão de](../../ingestion/home.md)dados em start.

Agora você também pode definir políticas de uso de dados com base nos rótulos aplicados. Para obter mais informações, consulte a visão geral [das políticas de uso de](../policies/overview.md)dados.

Para obter mais informações sobre como gerenciar conjuntos de dados em [!DNL Experience Platform], consulte a visão geral [](../../catalog/datasets/overview.md)dos conjuntos de dados.