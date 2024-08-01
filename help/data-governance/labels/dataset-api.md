---
keywords: Experience Platform;página inicial;tópicos populares;api do conjunto de dados;gerenciar uso de dados;api de uso de dados
solution: Experience Platform
title: Gerenciar rótulos de uso de dados para conjuntos de dados usando APIs
description: A API de serviço do conjunto de dados permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API de serviço de catálogo que gerencia metadados do conjunto de dados.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 9eda7068eb2a3fd5e59fbeff69c85abfad5ccf39
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 2%

---

# Gerenciar rótulos de uso de dados para conjuntos de dados usando APIs

O [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API [!DNL Catalog Service] que gerencia metadados do conjunto de dados.

>[!IMPORTANT]
>
>A aplicação de rótulos no nível do conjunto de dados só é compatível com casos de uso de governança de dados. Se você estiver tentando criar políticas de acesso para os dados, deverá [aplicar rótulos ao esquema](../../xdm/tutorials/labels.md) no qual o conjunto de dados se baseia. Consulte a visão geral no [controle de acesso baseado em atributos](../../access-control/abac/overview.md) para obter mais informações.

Este documento aborda como gerenciar rótulos para conjuntos de dados e campos usando o [!DNL Dataset Service API]. Para obter etapas sobre como gerenciar os próprios rótulos de uso de dados usando chamadas de API, consulte o [manual de ponto de extremidade de rótulos](../api/labels.md) para o [!DNL Policy Service API].

## Introdução

Antes de ler este guia, siga as etapas descritas na [seção de introdução](../../catalog/api/getting-started.md) do guia de desenvolvedor do Catálogo para coletar as credenciais necessárias para fazer chamadas para APIs do [!DNL Platform].

Para fazer chamadas para os pontos de extremidade descritos neste documento, você deve ter o valor `id` exclusivo para um conjunto de dados específico. Se você não tiver esse valor, consulte o manual em [listando objetos de Catálogo](../../catalog/api/list-objects.md) para encontrar as IDs dos seus conjuntos de dados existentes.

## Pesquisar rótulos para um conjunto de dados {#look-up}

Você pode pesquisar os rótulos de uso de dados que foram aplicados a um conjunto de dados existente fazendo uma solicitação GET para a API [!DNL Dataset Service].

**Formato da API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O valor `id` exclusivo do conjunto de dados cujos rótulos você deseja pesquisar. |

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

Você pode aplicar um conjunto de rótulos para um conjunto de dados inteiro fornecendo-os na carga de uma solicitação POST ou PUT para a API [!DNL Dataset Service]. O corpo da solicitação é o mesmo para ambas as chamadas. Não é possível adicionar rótulos a campos de conjunto de dados individuais.

**Formato da API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O valor `id` exclusivo do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

O exemplo de solicitação POST abaixo atualiza todo o conjunto de dados com um rótulo `C1`. Os campos fornecidos na carga são os mesmos que seriam necessários para uma solicitação PUT.

Ao fazer chamadas de API que atualizam os rótulos existentes de um conjunto de dados (PUT), um cabeçalho `If-Match` que indica a versão atual da entidade do rótulo do conjunto de dados no Serviço de conjunto de dados deve ser incluído. Para evitar colisões de dados, o serviço só atualizará a entidade do conjunto de dados se a cadeia de caracteres `If-Match` incluída corresponder à marca da versão mais recente gerada pelo sistema para esse conjunto de dados.

>[!NOTE]
>
>Se houver rótulos para o conjunto de dados em questão, novos rótulos só poderão ser adicionados por meio de uma solicitação PUT, o que requer um cabeçalho `If-Match`. Depois que os rótulos forem adicionados a um conjunto de dados, o valor `etag` mais recente será necessário para atualizar ou remover os rótulos posteriormente<br>Antes de executar o método PUT, execute uma solicitação GET nos rótulos do conjunto de dados. Atualize somente os campos específicos destinados à modificação na solicitação, deixando o restante inalterado. Além disso, verifique se a chamada de PUT mantém as mesmas entidades principais que a chamada de GET. Qualquer discrepância resultaria em um erro para o cliente.

GET Para recuperar a versão mais recente da entidade de rótulo do conjunto de dados, faça uma [solicitação](#look-up) ao ponto de extremidade `/datasets/{DATASET_ID}/labels`. O valor atual é retornado na resposta sob um cabeçalho `etag`. Ao atualizar rótulos de conjuntos de dados existentes, a prática recomendada é executar primeiro uma solicitação de pesquisa para o conjunto de dados para buscar seu valor `etag` mais recente antes de usar esse valor no cabeçalho `If-Match` de sua solicitação PUT subsequente.

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
| `entityId.namespace` | Isso é usado para evitar colisões de ID. O `namespace` é `AEP`. |
| `entityId.id` | A ID do recurso sendo atualizado. Isso se refere ao `datasetId`. |
| `entityId.type` | O tipo do recurso que está sendo atualizado. Isso sempre será `dataset`. |
| `labels` | Uma lista de rótulos de uso de dados que você deseja adicionar ao conjunto de dados inteiro. |
| `parents` | A matriz `parents` contém uma lista de `entityId`s da qual esse conjunto de dados herdará rótulos. Os conjuntos de dados podem herdar rótulos de esquemas e/ou conjuntos de dados. |

**Resposta**

Uma resposta bem-sucedida retorna o conjunto atualizado de rótulos para o conjunto de dados.

>[!IMPORTANT]
>
>A propriedade `optionalLabels` foi descontinuada para uso com solicitações POST. Não é mais possível adicionar rótulos de dados a campos de conjunto de dados. Uma operação POST gerará um erro se um valor `optionalLabel` estiver presente. Entretanto, é possível excluir rótulos de campos individuais usando uma solicitação PUT e a propriedade `optionalLabels`. Para obter mais informações, consulte a seção sobre [remoção de rótulos de um conjunto de dados](#remove).

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

Você pode remover qualquer rótulo de campo aplicado anteriormente atualizando o(s) valor(es) `optionalLabels` existente(s) com um subconjunto dos rótulos de campo existentes ou com uma lista vazia para removê-los totalmente. Faça uma solicitação PUT à API [!DNL Dataset Service] para atualizar ou remover rótulos aplicados anteriormente.

>[!NOTE]
>
>Você pode remover totalmente os rótulos de um conjunto de dados fornecendo uma lista vazia para o parâmetro `labels`. Não é obrigatório que um conjunto de dados retenha rótulos.

**Formato da API**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O valor `id` exclusivo do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

O conjunto de dados abaixo no qual a operação PUT é aplicada tinha C1 optionalLabel no campo properties/person/properties/address e C1, C2 optionalLabels no campo /properties/person/properties/name/properties/fullName. Após a operação put, o primeiro campo não terá rótulo (o rótulo C1 foi removido) e o segundo campo terá apenas o rótulo C1 (o rótulo C2 foi removido)

No exemplo de cenário abaixo, uma solicitação PUT é usada para remover rótulos adicionados a campos individuais. Antes da solicitação ser feita, o campo `fullName` tinha os rótulos `C1` e `C2` aplicados, e o campo `address` já tinha um rótulo `C1` aplicado. A solicitação PUT substitui rótulos `C1, C2` existentes do campo `fullName` por um rótulo `C1` usando o parâmetro `optionalLabels.labels`. A solicitação também substitui o rótulo `C1` do campo `address` por um conjunto vazio de rótulos de campo.

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
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
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
| `entityId` | Isso identifica a entidade do conjunto de dados específico que deve ser atualizada. O `entityId` deve incluir os três valores a seguir:<br/><br/>`namespace`: Isso é usado para evitar colisões de ID. O `namespace` é `AEP`.<br/>`id`: A ID do recurso que está sendo atualizado. Isso se refere ao `datasetId`.<br/>`type`: o tipo de recurso que está sendo atualizado. Isso sempre será `dataset`. |
| `labels` | Uma lista de rótulos de uso de dados que você deseja adicionar ao conjunto de dados inteiro. |
| `parents` | A matriz `parents` contém uma lista de `entityId`s da qual esse conjunto de dados herdará rótulos. Os conjuntos de dados podem herdar rótulos de esquemas e/ou conjuntos de dados. |
| `optionalLabels` | Esse parâmetro é usado para remover rótulos aplicados anteriormente a um campo de conjunto de dados. Uma lista de campos individuais no conjunto de dados do qual você deseja remover os rótulos. Cada item nesta matriz deve ter as seguintes propriedades: <br/><br/>`option`: um objeto que contenha os atributos [!DNL Experience Data Model] (XDM) do campo. As três propriedades a seguir são obrigatórias:<ul><li><code>id</code>: O URI <code>$id</code> valor do schema associado ao campo.</li><li><code>contentType</code>: O tipo de conteúdo e o número da versão do esquema. Isso deve tomar a forma de um dos <a href="../../xdm/api/getting-started.md#accept">cabeçalhos Aceitar</a> válidos para uma solicitação de pesquisa XDM.</li><li><code>schemaPath</code>: O caminho para o campo no esquema do conjunto de dados.</li></ul>`labels`: este valor deve conter um subconjunto dos rótulos de campo existentes aplicados ou estar vazio para remover todos os rótulos de campo existentes. Os métodos PUT ou POST agora retornam um erro se o campo `optionalLabels` tiver rótulos novos ou modificados. |

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

Ao ler este documento, você aprendeu a gerenciar rótulos de uso de dados para conjuntos de dados e campos usando a API [!DNL Dataset Service]. Agora você pode definir [políticas de uso de dados](../policies/overview.md) e [políticas de controle de acesso](../../access-control/abac/ui/policies.md) com base nos rótulos aplicados.

Para obter mais informações sobre como gerenciar conjuntos de dados no [!DNL Experience Platform], consulte a [visão geral sobre conjuntos de dados](../../catalog/datasets/overview.md).
