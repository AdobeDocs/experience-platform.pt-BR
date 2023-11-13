---
keywords: Experience Platform;página inicial;tópicos populares;api do conjunto de dados;gerenciar uso de dados;api de uso de dados
solution: Experience Platform
title: Gerenciar rótulos de uso de dados para conjuntos de dados usando APIs
description: A API de serviço do conjunto de dados permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API de serviço de catálogo que gerencia metadados do conjunto de dados.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 9f3fa696ed60ce85fa93515e39716d89ec80f1ec
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 2%

---

# Gerenciar rótulos de uso de dados para conjuntos de dados usando APIs

A variável [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) O permite aplicar e editar rótulos de uso para conjuntos de dados. Isso faz parte dos recursos do catálogo de dados da Adobe Experience Platform, mas é separado da variável [!DNL Catalog Service] API que gerencia metadados do conjunto de dados.

<!-- >[!IMPORTANT]
>
>Applying labels at the dataset level is only supported for data governance use cases. If you are trying to create access policies for the data, you must [apply labels to the schema](../../xdm/tutorials/labels.md) that the dataset is based on. See the overview on [attribute-based access control](../../access-control/abac/overview.md) for more information. -->

Este documento aborda como gerenciar rótulos para conjuntos de dados e campos usando o [!DNL Dataset Service API]. Para obter etapas sobre como gerenciar os próprios rótulos de uso de dados usando chamadas de API, consulte a seção [guia de endpoint de rótulos](../api/labels.md) para o [!DNL Policy Service API].

## Introdução

Antes de ler este guia, siga as etapas descritas na seção [seção de introdução](../../catalog/api/getting-started.md) no guia do desenvolvedor do Catálogo para coletar as credenciais necessárias para fazer chamadas para [!DNL Platform] APIs.

Para fazer chamadas para os endpoints descritos neste documento, você deve ter o `id` para um conjunto de dados específico. Se você não tiver esse valor, consulte o manual sobre [listando objetos do Catálogo](../../catalog/api/list-objects.md) para encontrar as IDs dos conjuntos de dados existentes.

## Pesquisar rótulos para um conjunto de dados {#look-up}

Você pode pesquisar os rótulos de uso de dados que foram aplicados a um conjunto de dados existente fazendo uma solicitação GET para o [!DNL Dataset Service] API.

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

Uma resposta bem-sucedida retorna os rótulos de uso de dados aplicados ao conjunto de dados.

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
| `optionalLabels` | Uma lista de campos individuais no conjunto de dados que têm rótulos de uso de dados aplicados a eles. |

## Aplicar rótulos a um conjunto de dados {#apply}

Você pode aplicar um conjunto de rótulos para um conjunto de dados inteiro fornecendo-os na carga de uma solicitação POST ou PUT para o [!DNL Dataset Service] API. O corpo da solicitação é o mesmo para ambas as chamadas. Não é possível adicionar rótulos a campos de conjunto de dados individuais.

**Formato da API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O único `id` valor do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

O exemplo de solicitação POST abaixo atualiza todo o conjunto de dados com um `C1` rótulo. Os campos fornecidos na carga são os mesmos que seriam necessários para uma solicitação PUT.

<!-- When making API calls that update the existing labels of a dataset (PUT), an `If-Match` header that indicates the current version of the dataset-label entity in Dataset Service must be included. In order to prevent data collisions, the service will only update the dataset entity if the included `If-Match` string matches the latest version tag generated by the system for that dataset. -->

>[!NOTE]
>
>Se houver rótulos para o conjunto de dados em questão, novos rótulos só poderão ser adicionados por meio de uma solicitação PUT, o que requer um `If-Match` cabeçalho. Depois que os rótulos são adicionados a um conjunto de dados, o mais recente `etag` O valor de é necessário para atualizar ou remover os rótulos posteriormente.

Para recuperar a versão mais recente da entidade de rótulo do conjunto de dados, faça uma [solicitação GET](#look-up) para o `/datasets/{DATASET_ID}/labels` terminal. O valor atual é retornado na resposta sob um `etag` cabeçalho. Ao atualizar rótulos de conjuntos de dados existentes, a prática recomendada é executar primeiro uma solicitação de pesquisa para o conjunto de dados para buscar o mais recente `etag` antes de usar esse valor na variável `If-Match` cabeçalho da solicitação PUT subsequente.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": []
      } '
```

| Propriedade | Descrição |
| --- | --- |
| `entityId` | Isso identifica a entidade do conjunto de dados específico que deve ser atualizada. |
| `entityId.namespace` | Isso é usado para evitar colisões de ID. A variável `namespace` é `AEP`. |
| `entityId.id` | A ID do recurso sendo atualizado. Refere-se ao `datasetId`. |
| `entityId.type` | O tipo do recurso que está sendo atualizado. Isso sempre será `dataset`. |
| `labels` | Uma lista de rótulos de uso de dados que você deseja adicionar ao conjunto de dados inteiro. |
| `parents` | A variável `parents` matriz contém uma lista de `entityId`para que esse conjunto de dados herde rótulos do. Os conjuntos de dados podem herdar rótulos de esquemas e/ou conjuntos de dados. |

**Resposta**

Uma resposta bem-sucedida retorna o conjunto atualizado de rótulos para o conjunto de dados.

>[!IMPORTANT]
>
>A variável `optionalLabels` A propriedade foi descontinuada para uso com solicitações POST. Não é mais possível adicionar rótulos de dados a campos de conjunto de dados. Uma operação POST emitirá um erro se uma `optionalLabel` valor está presente. No entanto, é possível excluir rótulos de campos individuais usando uma solicitação PUT e a variável `optionalLabels` propriedade. Para obter mais informações, consulte a seção sobre [remoção de rótulos de um conjunto de dados](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## Remover rótulos de um conjunto de dados {#remove}

Você pode remover qualquer rótulo de campo aplicado anteriormente atualizando o existente `optionalLabels` valor(es) com um subconjunto dos rótulos de campo existentes ou uma lista vazia para removê-los totalmente. Faça uma solicitação PUT para o [!DNL Dataset Service] API para atualizar ou remover rótulos aplicados anteriormente.

**Formato da API**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O único `id` valor do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

O conjunto de dados abaixo no qual a operação PUT é aplicada tinha C1 optionalLabel no campo properties/person/properties/address e C1, C2 optionalLabels no campo /properties/person/properties/name/properties/fullName. Após a operação put, o primeiro campo não terá rótulo (o rótulo C1 foi removido) e o segundo campo terá apenas o rótulo C1 (o rótulo C2 foi removido)

No exemplo de cenário abaixo, uma solicitação PUT é usada para remover rótulos adicionados a campos individuais. Antes de o pedido ser apresentado, a `fullName` o campo tinha o `C1` e `C2` rótulos aplicados e a variável `address` o campo já tinha um `C1` rótulo aplicado. A solicitação PUT substitui os rótulos existentes `C1, C2` rótulos do `fullName` campo com um `C1` rótulo usando o `optionalLabels.labels` parâmetro. A solicitação também substitui a variável `C1` rótulo do `address` com um conjunto vazio de rótulos de campo.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| Parâmetro | Descrição |
| --- | --- |
| `entityId` | Isso identifica a entidade do conjunto de dados específico que deve ser atualizada. A variável `entityId` deve incluir os três valores a seguir:<br/><br/>`namespace`: é usado para evitar colisões de ID. A variável `namespace` é `AEP`.<br/>`id`: a ID do recurso que está sendo atualizado. Refere-se ao `datasetId`.<br/>`type`: o tipo de recurso que está sendo atualizado. Isso sempre será `dataset`. |
| `labels` | Uma lista de rótulos de uso de dados que você deseja adicionar ao conjunto de dados inteiro. |
| `parents` | A variável `parents` matriz contém uma lista de `entityId`para que esse conjunto de dados herde rótulos do. Os conjuntos de dados podem herdar rótulos de esquemas e/ou conjuntos de dados. |
| `optionalLabels` | Esse parâmetro é usado para remover rótulos aplicados anteriormente a um campo de conjunto de dados. Uma lista de campos individuais no conjunto de dados do qual você deseja remover os rótulos. Cada item nesta matriz deve ter as seguintes propriedades: <br/><br/>`option`: um objeto que contém a variável [!DNL Experience Data Model] Atributos de (XDM) do campo. As três propriedades a seguir são obrigatórias:<ul><li><code>id</code>: O URI <code>$id</code> valor do schema associado ao campo.</li><li><code>contentType</code>: O tipo de conteúdo e o número da versão do esquema. Esta deve assumir a forma de um dos <a href="../../xdm/api/getting-started.md#accept">Aceitar cabeçalhos</a> para uma solicitação de pesquisa XDM.</li><li><code>schemaPath</code>: O caminho para o campo no esquema do conjunto de dados.</li></ul>`labels`: esse valor deve conter um subconjunto dos rótulos de campo existentes aplicados ou estar vazio para remover todos os rótulos de campo existentes. Os métodos PUT ou POST agora retornam um erro se a variável `optionalLabels` O campo tem rótulos novos ou modificados. |

**Resposta**

Uma resposta bem-sucedida retorna o conjunto atualizado de rótulos para o conjunto de dados.

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## Próximas etapas

Ao ler este documento, você aprendeu a gerenciar rótulos de uso de dados para conjuntos de dados e campos usando o [!DNL Dataset Service] API. Agora você pode definir [políticas de uso de dados](../policies/overview.md) e [políticas de controle de acesso](../../access-control/abac/ui/policies.md) com base nos rótulos aplicados.

Para obter mais informações sobre o gerenciamento de conjuntos de dados no [!DNL Experience Platform], consulte o [visão geral dos conjuntos de dados](../../catalog/datasets/overview.md).
