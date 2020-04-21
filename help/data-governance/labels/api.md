---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Gerenciar rótulos de uso de dados usando APIs '
topic: developer guide
translation-type: tm+mt
source-git-commit: cac6ab568f030cf86ee68a1df9e45a3ac9d421cb

---


# Gerenciar rótulos de uso de dados usando APIs

Este documento fornece etapas sobre como gerenciar rótulos de uso de dados no nível do conjunto de dados e do campo usando a API do serviço de catálogo.

## Introdução

Antes de ler este guia, é recomendável ler a visão geral [do serviço de](../../catalog/home.md) catálogo para obter uma introdução mais robusta ao serviço. Além disso, você também deve seguir as etapas descritas na seção [](../../catalog/api/getting-started.md) Introdução no guia do desenvolvedor do Catálogo para coletar as credenciais necessárias para fazer chamadas para a API do Catálogo.

Para fazer chamadas para os pontos finais descritos nas seções abaixo, é necessário ter o `id` valor exclusivo para um conjunto de dados específico. Se você não tiver esse valor, consulte a seção do guia do desenvolvedor na [lista de objetos](../../catalog/api/list-objects.md) do Catálogo para localizar as IDs de seus conjuntos de dados existentes.

## Procurar rótulos para um conjunto de dados {#lookup}

Você pode pesquisar os rótulos de uso de dados que foram aplicados a um conjunto de dados existente fazendo uma solicitação GET.

**Formato da API**

```http
GET /dataSets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O `id` valor exclusivo do conjunto de dados cujos rótulos você deseja pesquisar. |

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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

## Aplicar rótulos a um conjunto de dados

Você pode criar um conjunto de rótulos para um conjunto de dados, fornecendo-os na carga de uma solicitação POST ou PUT. O uso de qualquer um desses métodos substitui quaisquer rótulos existentes e os substitui pelos fornecidos na carga.

**Formato da API**

```http
POST /dataSets/{DATASET_ID}/labels
PUT /dataSets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O `id` valor exclusivo do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

A solicitação POST a seguir adiciona uma série de rótulos ao conjunto de dados, bem como um campo específico nesse conjunto de dados. Os campos fornecidos na carga são os mesmos que seriam necessários para uma solicitação PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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
| `optionalLabels` | Uma lista de qualquer campo individual no conjunto de dados ao qual você deseja adicionar rótulos. Cada item nesta matriz deve ter as seguintes propriedades: <br/><br/>`option`: Um objeto que contém os atributos do Modelo de dados de experiência (XDM) do campo. As três propriedades a seguir são obrigatórias:<ul><li>id</code>: O valor URI $id</code> do schema associado ao campo.</li><li>contentType</code>: O tipo de conteúdo e o número da versão do schema. Isso deve assumir a forma de um dos cabeçalhos <a href="../../xdm/api/look-up-resource.md">Accept válidos</a> para uma solicitação de pesquisa XDM.</li><li>schemaPath</code>: O caminho para o campo dentro do schema do conjunto de dados.</li></ul>`labels`: Uma lista de rótulos de uso de dados que você deseja adicionar ao campo. |

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

## Excluir rótulos de um conjunto de dados

Você pode excluir os rótulos aplicados a um conjunto de dados, fazendo uma solicitação DELETE.

>[!NOTE] Você só deve usar essa operação ao preparar o conjunto de dados pai para exclusão.

**Formato da API**

```http
DELETE /dataSets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O `id` valor exclusivo do conjunto de dados cujos rótulos você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta com êxito HTTP status 200 (OK) indica que os rótulos foram excluídos. Você pode [procurar os rótulos](#lookup) existentes para o conjunto de dados em uma chamada separada para confirmar isso.

## Próximas etapas

Agora que você adicionou rótulos de uso de dados no nível do conjunto de dados e do campo, é possível começar a assimilar dados na Experience Platform. Para saber mais, leia a documentação [de ingestão de](../../ingestion/home.md)dados em start.

Agora você também pode definir políticas de uso de dados com base nos rótulos aplicados. Para obter mais informações, consulte a visão geral [das políticas de uso de](../policies/overview.md)dados.