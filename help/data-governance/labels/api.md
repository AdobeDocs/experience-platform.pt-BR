---
keywords: Experience Platform, home, tópicos populares, governança de dados, api de etiqueta de uso de dados, api de serviço de política
solution: Experience Platform
title: 'Gerenciar rótulos de uso de dados usando APIs '
topic-legacy: developer guide
description: A API do Serviço de conjunto de dados permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API do Serviço de catálogo que gerencia os metadados do conjunto de dados.
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 3%

---


# Gerenciar rótulos de uso de dados usando APIs

Este documento fornece etapas sobre como gerenciar rótulos de uso de dados usando o [!DNL Policy Service] API e [!DNL Dataset Service] API.

O [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) O fornece vários endpoints que permitem criar e gerenciar rótulos de uso de dados para sua organização.

O [!DNL Dataset Service] A API permite aplicar e editar rótulos de uso para conjuntos de dados. Ele faz parte dos recursos de catálogo de dados do Adobe Experience Platform, mas é separado do [!DNL Catalog Service] API que gerencia metadados do conjunto de dados.

## Introdução

Antes de ler este guia, siga as etapas descritas em [seção introdução](../../catalog/api/getting-started.md) no guia do desenvolvedor do Catálogo para coletar as credenciais necessárias para fazer chamadas para [!DNL Platform] APIs.

Para fazer chamadas para o [!DNL Dataset Service] endpoints descritos neste documento, você deve ter o `id` para um conjunto de dados específico. Se você não tiver esse valor, consulte o guia sobre [listando objetos do catálogo](../../catalog/api/list-objects.md) para encontrar as IDs de seus conjuntos de dados existentes.

## Listar todos os rótulos {#list-labels}

Usar o [!DNL Policy Service] API, é possível listar tudo `core` ou `custom` fazendo uma solicitação de GET para `/labels/core` ou `/labels/custom`, respectivamente.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de rótulos personalizados recuperados do sistema. Como o exemplo de solicitação acima foi feito para `/labels/custom`, a resposta abaixo mostra somente rótulos personalizados.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## Pesquisar um rótulo {#look-up-label}

Você pode procurar um rótulo específico incluindo o `name` no caminho de uma solicitação do GET para a [!DNL Policy Service] API.

**Formato da API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LABEL_NAME}` | O `name` propriedade do rótulo personalizado que deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera o rótulo personalizado `L2`, conforme indicado no caminho.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Para criar ou atualizar um rótulo personalizado, você deve fazer uma solicitação de PUT para o [!DNL Policy Service] API.

**Formato da API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LABEL_NAME}` | O `name` de um rótulo personalizado. Se um rótulo personalizado com esse nome não existir, um novo rótulo será criado. Se existir, esse rótulo será atualizado. |

**Solicitação**

A solicitação a seguir cria um novo rótulo, `L3`, que visa descrever dados que contêm informações relativas aos planos de pagamento selecionados dos clientes.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Um identificador de string exclusivo para o rótulo. Esse valor é usado para fins de pesquisa e aplicação do rótulo a conjuntos de dados e campos, portanto, é recomendável que seja curto e conciso. |
| `category` | A categoria do rótulo. Embora você possa criar suas próprias categorias para rótulos personalizados, é altamente recomendável usar `Custom` se desejar que o rótulo apareça na interface do usuário do . |
| `friendlyName` | Um nome amigável para o rótulo, usado para fins de exibição. |
| `description` | (Opcional) Uma descrição do rótulo para fornecer contexto adicional. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do rótulo personalizado, com código HTTP 200 (OK) se um rótulo existente foi atualizado, ou 201 (Criado) se um novo rótulo foi criado.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
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

## Pesquisar rótulos para um conjunto de dados {#look-up-dataset-labels}

Você pode pesquisar os rótulos de uso de dados que foram aplicados a um conjunto de dados existente fazendo uma solicitação do GET para a variável [!DNL Dataset Service] API.

**Formato da API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O único `id` valor do conjunto de dados cujos rótulos você deseja pesquisar. |

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os rótulos de uso de dados que foram aplicados ao conjunto de dados.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
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
| `optionalLabels` | Uma lista de campos individuais no conjunto de dados que têm rótulos de uso de dados aplicados a eles. As seguintes subpropriedades são obrigatórias:<br/><br/>`option`: Um objeto que contém a variável [!DNL Experience Data Model] (XDM) atributos do campo. As três propriedades a seguir são obrigatórias:<ul><li>`id`: O URI `$id` do schema associado ao campo .</li><li>`contentType`: Indica o formato e a versão do esquema. Consulte a seção sobre [versão do schema](../../xdm/api/getting-started.md#versioning) no guia da API XDM para obter mais informações.</li><li>`schemaPath`: O caminho para a propriedade de schema em questão, escrito em [Ponteiro JSON](../../landing/api-fundamentals.md#json-pointer) sintaxe.</li></ul>`labels`: Uma lista de rótulos de uso de dados que você deseja adicionar ao campo. |

- id: O valor $id de URI para o esquema XDM no qual o conjunto de dados se baseia.
- contentType: Indica o formato e a versão do esquema. Consulte a seção sobre [versão do schema](../../xdm/api/getting-started.md#versioning) no guia da API XDM para obter mais informações.
- schemaPath: O caminho para a propriedade de schema em questão, escrito em [Ponteiro JSON](../../landing/api-fundamentals.md#json-pointer) sintaxe.

## Aplicar rótulos a um conjunto de dados {#apply-dataset-labels}

Você pode criar um conjunto de rótulos para um conjunto de dados, fornecendo-os na carga de uma solicitação de POST ou PUT para o [!DNL Dataset Service] API. O uso de qualquer um desses métodos substitui quaisquer rótulos existentes e os substitui pelos fornecidos no payload.

**Formato da API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O único `id` do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

A solicitação de POST a seguir adiciona uma série de rótulos ao conjunto de dados, bem como um campo específico nesse conjunto de dados. Os campos fornecidos no payload são os mesmos que seriam necessários para uma solicitação de PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `optionalLabels` | Uma lista de quaisquer campos individuais no conjunto de dados ao qual você deseja adicionar rótulos. Cada item nesta matriz deve ter as seguintes propriedades:<br/><br/>`option`: Um objeto que contém a variável [!DNL Experience Data Model] (XDM) atributos do campo. As três propriedades a seguir são obrigatórias:<ul><li>`id`: O URI `$id` do schema associado ao campo .</li><li>`contentType`: Indica o formato e a versão do esquema. Consulte a seção sobre [versão do schema](../../xdm/api/getting-started.md#versioning) no guia da API XDM para obter mais informações.</li><li>`schemaPath`: O caminho para a propriedade de schema em questão, escrito em [Ponteiro JSON](../../landing/api-fundamentals.md#json-pointer) sintaxe.</li></ul>`labels`: Uma lista de rótulos de uso de dados que você deseja adicionar ao campo. |

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

Você pode remover os rótulos aplicados a um conjunto de dados, fazendo uma solicitação de DELETE para a variável [!DNL Dataset Service] API.

**Formato da API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O único `id` valor do conjunto de dados cujos rótulos você deseja remover. |

**Solicitação**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida HTTP status 200 (OK), indicando que os rótulos foram removidos. Você pode [procure os rótulos existentes](#look-up-dataset-labels) para o conjunto de dados em uma chamada separada para confirmar isso.

## Próximas etapas

Ao ler este documento, você aprendeu a gerenciar rótulos de uso de dados usando APIs.

Depois de adicionar rótulos de uso de dados no nível do conjunto de dados e do campo, você pode começar a assimilar dados no [!DNL Experience Platform]. Para saber mais, comece lendo o [documentação de ingestão de dados](../../ingestion/home.md).

Agora, também é possível definir políticas de uso de dados com base nos rótulos aplicados. Para obter mais informações, consulte o [visão geral das políticas de uso de dados](../policies/overview.md).

Para obter mais informações sobre o gerenciamento de conjuntos de dados no [!DNL Experience Platform], consulte o [visão geral dos conjuntos de dados](../../catalog/datasets/overview.md).