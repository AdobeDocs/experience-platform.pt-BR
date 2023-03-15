---
keywords: Experience Platform;página inicial;tópicos populares;api do conjunto de dados;gerenciar uso de dados;api de uso de dados
solution: Experience Platform
title: Gerenciar rótulos de uso de dados para conjuntos de dados usando APIs
description: A API de serviço do conjunto de dados permite aplicar e editar rótulos de uso para conjuntos de dados. Ela faz parte dos recursos de catálogo de dados da Adobe Experience Platform, mas é separada da API de serviço de catálogo que gerencia metadados do conjunto de dados.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 2%

---

# Gerenciar rótulos de uso de dados para conjuntos de dados usando APIs

A variável [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) O permite aplicar e editar rótulos de uso para conjuntos de dados. Isso faz parte dos recursos do catálogo de dados da Adobe Experience Platform, mas é separado da variável [!DNL Catalog Service] API que gerencia metadados do conjunto de dados.

>[!IMPORTANT]
>
>A aplicação de rótulos no nível do conjunto de dados só é compatível com casos de uso de governança de dados. Se estiver tentando criar políticas de acesso para os dados, você deverá [aplicar rótulos ao esquema](../../xdm/tutorials/labels.md) em que o conjunto de dados se baseia. Consulte a visão geral em [controle de acesso baseado em atributos](../../access-control/abac/overview.md) para obter mais informações.

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

Você pode criar um conjunto de rótulos para um conjunto de dados fornecendo-os na carga de uma solicitação POST ou PUT para o [!DNL Dataset Service] API. O uso de qualquer um desses métodos substitui quaisquer rótulos existentes e os substitui pelos fornecidos na carga.

**Formato da API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O único `id` valor do conjunto de dados para o qual você está criando rótulos. |

**Solicitação**

O exemplo de solicitação PUT abaixo atualiza os rótulos existentes para um conjunto de dados, bem como um campo específico nesse conjunto de dados. Os campos fornecidos na carga são os mesmos que seriam necessários para uma solicitação POST.

Ao fazer chamadas de API que atualizam os rótulos existentes de um conjunto de dados (PUT), um `If-Match` cabeçalho que indica que a versão atual da entidade do rótulo do conjunto de dados no Serviço de conjunto de dados deve ser incluída. Para evitar colisões de dados, o serviço atualizará a entidade do conjunto de dados somente se o `If-Match` A sequência de caracteres corresponde à tag da versão mais recente gerada pelo sistema para esse conjunto de dados.

>[!NOTE]
>
>Se não existirem rótulos para o conjunto de dados em questão, novos rótulos só poderão ser adicionados por meio de uma solicitação POST, o que não requer um `If-Match` cabeçalho. Depois que os rótulos forem adicionados a um conjunto de dados, uma variável `etag` é atribuído um valor que pode ser usado para atualizar ou remover os rótulos posteriormente.

Para recuperar a versão mais recente da entidade de rótulo do conjunto de dados, faça uma [solicitação GET](#look-up) para o `/datasets/{DATASET_ID}/labels` terminal. O valor atual é retornado na resposta sob um `etag` cabeçalho. Ao atualizar rótulos de conjuntos de dados existentes, a prática recomendada é executar primeiro uma solicitação de pesquisa para o conjunto de dados para buscar o mais recente `etag` antes de usar esse valor na variável `If-Match` cabeçalho da solicitação PUT subsequente.

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
| `optionalLabels` | Uma lista de campos individuais no conjunto de dados ao qual você deseja adicionar rótulos. Cada item nesta matriz deve ter as seguintes propriedades: <br/><br/>`option`: um objeto que contém a variável [!DNL Experience Data Model] Atributos de (XDM) do campo. As três propriedades a seguir são obrigatórias:<ul><li>id</code>: a $id de URI</code> valor do schema associado ao campo.</li><li>contentType</code>: O tipo de conteúdo e o número da versão do esquema. Esta deve assumir a forma de um dos <a href="../../xdm/api/getting-started.md#accept">Aceitar cabeçalhos</a> para uma solicitação de pesquisa XDM.</li><li>schemaPath</code>: O caminho para o campo no esquema do conjunto de dados.</li></ul>`labels`: uma lista de rótulos de uso de dados que você deseja adicionar ao campo. |

**Resposta**

Uma resposta bem-sucedida retorna o conjunto atualizado de rótulos para o conjunto de dados.

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

## Próximas etapas

Ao ler este documento, você aprendeu a gerenciar rótulos de uso de dados para conjuntos de dados e campos usando o [!DNL Dataset Service] API. Agora você pode definir [políticas de uso de dados](../policies/overview.md) e [políticas de controle de acesso](../../access-control/abac/ui/policies.md) com base nos rótulos aplicados.

Para obter mais informações sobre o gerenciamento de conjuntos de dados no [!DNL Experience Platform], consulte o [visão geral dos conjuntos de dados](../../catalog/datasets/overview.md).
