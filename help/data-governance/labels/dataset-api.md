---
keywords: Experience Platform;home;popular topics;dataset api;gerenciar o uso de dados;api de uso de dados
solution: Experience Platform
title: 'Gerenciar rótulos de uso de dados para conjuntos de dados usando APIs '
topic: developer guide
description: A API de Serviço de Conjunto de Dados permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API do serviço de catálogo que gerencia os metadados do conjunto de dados.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---


# Gerenciar rótulos de uso de dados para conjuntos de dados usando APIs

O [[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) permite que você aplique e edite rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API [!DNL Catalog Service] que gerencia os metadados do conjunto de dados.

Este documento aborda como gerenciar rótulos para conjuntos de dados e campos usando o [!DNL Dataset Service API]. Para obter etapas sobre como gerenciar os próprios rótulos de uso de dados usando chamadas de API, consulte o [guia de ponto final de rótulos](../api/labels.md) para o [!DNL Policy Service API].

## Introdução

Antes de ler este guia, siga as etapas descritas na seção [introdução](../../catalog/api/getting-started.md) no guia do desenvolvedor do Catálogo para coletar as credenciais necessárias para fazer chamadas para [!DNL Platform] APIs.

Para fazer chamadas para os pontos de extremidade contornados neste documento, é necessário ter o valor `id` exclusivo para um conjunto de dados específico. Se você não tiver esse valor, consulte o guia em [listando objetos de catálogo](../../catalog/api/list-objects.md) para localizar as IDs dos conjuntos de dados existentes.

## Procurar etiquetas para um conjunto de dados {#look-up}

Você pode pesquisar os rótulos de uso de dados que foram aplicados a um conjunto de dados existente, fazendo uma solicitação de GET para a API [!DNL Dataset Service].

**Formato da API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O valor exclusivo `id` do conjunto de dados cujos rótulos você deseja pesquisar. |

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

## Aplicar rótulos a um conjunto de dados {#apply}

Você pode criar um conjunto de rótulos para um conjunto de dados, fornecendo-os na carga de uma solicitação POST ou PUT para a API [!DNL Dataset Service]. O uso de qualquer um desses métodos substitui quaisquer rótulos existentes e os substitui pelos fornecidos na carga.

**Formato da API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O valor exclusivo `id` do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

A solicitação de PUT a seguir atualiza os rótulos existentes para um conjunto de dados, bem como um campo específico nesse conjunto de dados. Os campos fornecidos na carga são os mesmos que seriam necessários para uma solicitação de POST.

>[!IMPORTANT]
>
>Um cabeçalho `If-Match` válido deve ser fornecido ao fazer solicitações de PUT ao ponto de extremidade `/datasets/{DATASET_ID}/labels`. Consulte a seção [apêndice](#if-match) para obter mais informações sobre como usar o cabeçalho necessário.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
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
| `optionalLabels` | Uma lista de qualquer campo individual no conjunto de dados ao qual você deseja adicionar rótulos. Cada item nesta matriz deve ter as seguintes propriedades: <br/><br/>`option`: Um objeto que contém os atributos [!DNL Experience Data Model] (XDM) do campo. As três propriedades a seguir são obrigatórias:<ul><li>id</code>: O valor URI $id</code> do schema associado ao campo.</li><li>contentType</code>: O tipo de conteúdo e o número da versão do schema. Isso deve assumir a forma de um dos <a href="../../xdm/api/getting-started.md#accept">cabeçalhos Accept</a> válidos para uma solicitação de pesquisa XDM.</li><li>schemaPath</code>: O caminho para o campo dentro do schema do conjunto de dados.</li></ul>`labels`: Uma lista de rótulos de uso de dados que você deseja adicionar ao campo. |

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

## Remover rótulos de um conjunto de dados {#remove}

Você pode remover os rótulos aplicados a um conjunto de dados, fazendo uma solicitação DELETE para a API [!DNL Dataset Service].

**Formato da API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O valor exclusivo `id` do conjunto de dados cujos rótulos você deseja remover. |

**Solicitação**

A solicitação a seguir remove os rótulos do conjunto de dados especificado no caminho.

>[!IMPORTANT]
>
>Um cabeçalho `If-Match` válido deve ser fornecido ao fazer solicitações de DELETE ao ponto de extremidade `/datasets/{DATASET_ID}/labels`. Consulte a seção [apêndice](#if-match) para obter mais informações sobre como usar o cabeçalho necessário.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**Resposta**

Uma resposta com êxito HTTP status 200 (OK), indicando que os rótulos foram removidos. Você pode [procurar os rótulos existentes](#look-up) para o conjunto de dados em uma chamada separada para confirmar isso.

## Próximas etapas

Ao ler este documento, você aprendeu a gerenciar rótulos de uso de dados para conjuntos de dados e campos usando a API [!DNL Dataset Service].

Depois de adicionar rótulos de uso de dados no nível do conjunto de dados e do campo, você pode começar a assimilar dados em [!DNL Experience Platform]. Para saber mais, leia a documentação de [ingestão de dados](../../ingestion/home.md).

Agora você também pode definir políticas de uso de dados com base nos rótulos aplicados. Para obter mais informações, consulte a [visão geral das políticas de uso de dados](../policies/overview.md).

Para obter mais informações sobre como gerenciar conjuntos de dados em [!DNL Experience Platform], consulte [visão geral dos conjuntos de dados](../../catalog/datasets/overview.md).

## Apêndice {#appendix}

A seção a seguir contém informações adicionais sobre como trabalhar com rótulos usando a API de Serviço de Conjunto de Dados.

### [!DNL If-Match] header  {#if-match}

Ao fazer chamadas de API que atualizam os rótulos existentes de um conjunto de dados (PUT e DELETE), um cabeçalho `If-Match` que indica a versão atual da entidade dataset-label no Serviço de Conjunto de Dados deve ser incluído. Para evitar colisões de dados, o serviço só atualizará a entidade do conjunto de dados se a string `If-Match` incluída corresponder à tag da versão mais recente gerada pelo sistema para esse conjunto de dados.

>[!NOTE]
>
>Se não houver etiquetas para o conjunto de dados em questão, as novas etiquetas só poderão ser adicionadas por meio de uma solicitação POST, o que não requer um cabeçalho `If-Match`. Depois que os rótulos forem adicionados a um conjunto de dados, um valor `etag` será atribuído e poderá ser usado para atualizar ou remover os rótulos posteriormente.

Para recuperar a versão mais recente da entidade de rótulo do conjunto de dados, faça uma [solicitação de GET](#look-up) para o terminal `/datasets/{DATASET_ID}/labels`. O valor atual é retornado na resposta em um cabeçalho `etag`. Ao atualizar rótulos de conjunto de dados existentes, a prática recomendada é primeiro executar uma solicitação de pesquisa para o conjunto de dados para obter o valor `etag` mais recente antes de usar esse valor no cabeçalho `If-Match` da solicitação PUT ou DELETE subsequente.