---
keywords: Experience Platform;página inicial;tópicos populares;conjunto de dados;conjunto de dados;criar um conjunto de dados;criar conjunto de dados
solution: Experience Platform
title: Criar um conjunto de dados usando APIs
description: Este documento fornece etapas gerais para criar um conjunto de dados usando APIs do Adobe Experience Platform e preencher o conjunto de dados usando um arquivo.
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: e2f16f532b98e6948ffd7f331e630137b3972f0f
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 2%

---

# Criar um conjunto de dados usando APIs

Este documento fornece etapas gerais para criar um conjunto de dados usando APIs do Adobe Experience Platform e preencher o conjunto de dados usando um arquivo.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Assimilação em lote](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] O permite assimilar dados como arquivos em lote.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para o [!DNL Platform] APIs.

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem uma `Content-Type: application/json` cabeçalho. Para solicitações JSON+PATCH, a variável `Content-Type` deve ser `application/json-patch+json`.

## Tutorial

Para criar um conjunto de dados, um esquema deve ser definido primeiro. Um esquema é um conjunto de regras para ajudar a representar dados. Além de descrever a estrutura dos dados, os esquemas fornecem restrições e expectativas que podem ser aplicadas e usadas para validar os dados à medida que são movidos entre sistemas.

Essas definições padrão permitem que os dados sejam interpretados de forma consistente, independentemente da origem, e eliminam a necessidade de tradução entre aplicativos. Para obter mais informações sobre a composição de schemas, consulte o guia na [noções básicas da composição do esquema](../../xdm/schema/composition.md)

## Pesquisar um esquema de conjunto de dados

Este tutorial começa onde a variável [Tutorial da API do registro de esquema](../../xdm/tutorials/create-schema-api.md) termina, utilizando o schema de Membros de fidelidade criado durante esse tutorial.

Se você não tiver concluído o [!DNL Schema Registry] tutorial, inicie e continue com este tutorial de conjunto de dados somente depois de ter composto o esquema necessário.

A chamada a seguir pode ser usada para exibir o esquema Membros de Fidelidade criado durante a [!DNL Schema Registry] Tutorial da API:

**Formato da API**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O formato do objeto de resposta depende do cabeçalho Aceitar enviado na solicitação. As propriedades individuais nesta resposta foram minimizadas por espaço.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Criar um conjunto de dados

Com o esquema Membros de fidelidade em vigor, agora é possível criar um conjunto de dados que faça referência ao esquema.

**Formato da API**

```HTTP
POST /dataSets
```

**Solicitação**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `schemaRef.id` | O URI `$id` para o esquema XDM no qual o conjunto de dados será baseado. |
| `schemaRef.contentType` | Indica o formato e a versão do esquema. Consulte a seção sobre [controle de versão do esquema](../../xdm/api/getting-started.md#versioning) no guia API XDM para obter mais informações. |

>[!NOTE]
>
>Este tutorial usa o [Apache Parquet](https://parquet.apache.org/docs/) formato de arquivo para todos os seus exemplos. Um exemplo que usa o formato de arquivo JSON pode ser encontrado no [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md)

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta que consiste em uma matriz que contém a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma cadeia de caracteres gerada pelo sistema e somente leitura usada para fazer referência ao conjunto de dados em chamadas de API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Criar um lote

Antes de adicionar dados a um conjunto de dados, é necessário criar um lote vinculado ao conjunto de dados. O lote será usado para upload.

**Formato da API**

```HTTP
POST /batches
```

**Solicitação**

O corpo da solicitação inclui um campo &quot;datasetId&quot;, cujo valor é o `{DATASET_ID}` gerado na etapa anterior.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta. O objeto de resposta consiste em uma matriz contendo a ID do lote recém-criado no formato `"@/batches/{BATCH_ID}"`. A ID do lote é uma string somente leitura gerada pelo sistema usada para fazer referência ao lote em chamadas de API.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## Fazer upload de arquivos em um lote

Depois de criar um novo lote para upload com sucesso, agora é possível fazer upload de arquivos para o conjunto de dados específico. É importante lembrar que, ao definir o conjunto de dados, você especificou o formato de arquivo como Parquet. Portanto, os arquivos carregados devem estar nesse formato.

>[!NOTE]
>
>O maior arquivo de upload de dados aceito é de 512 MB. Se o arquivo de dados for maior que esse, ele precisará ser dividido em blocos com até 512 MB, para ser carregado um de cada vez. Você pode fazer upload de cada arquivo no mesmo lote repetindo essa etapa para cada arquivo, usando a mesma ID de lote. Não há limite para o número de arquivos que você pode carregar como parte de um lote.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BATCH_ID}` | A variável `id` do lote para o qual você está fazendo upload. |
| `{DATASET_ID}` | A variável `id` do conjunto de dados em que o lote será mantido. |
| `{FILE_NAME}` | O nome do arquivo que você está fazendo upload. |

**Solicitação**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Resposta**

Um arquivo carregado com êxito retorna um corpo de resposta em branco e o Status HTTP 200 (OK).

## Sinal de conclusão de lote

Depois de fazer upload de todos os arquivos de dados para o lote, você pode sinalizar o lote para conclusão. A conclusão da sinalização faz com que o serviço crie [!DNL Catalog] `DataSetFile` entradas para os arquivos carregados e associá-los ao lote gerado anteriormente. A variável [!DNL Catalog] O lote é marcado como bem-sucedido, o que aciona todos os fluxos downstream que podem funcionar nos dados agora disponíveis.

**Formato da API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parâmetro | Descrição |
| --- | --- |
| `{BATCH_ID}` | A variável `id` do lote que você está marcando como concluído. |

**Solicitação**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Resposta**

Um lote concluído com êxito retorna um corpo de resposta em branco e um Status HTTP 200 (OK).

## Monitorar assimilação

Dependendo do tamanho dos dados, os lotes levam vários períodos de tempo para serem assimilados. Você pode monitorar o status de um lote anexando a ID de um lote a um `GET /batches` solicitação.

**Formato da API**

```HTTP
GET /batches/{BATCH_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BATCH_ID}` | A variável `id` do lote que você deseja monitorar. |

**Solicitação**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Resposta**

Uma resposta positiva retorna um objeto com sua `status` atributo que contém o valor de `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

Uma resposta negativa retorna um objeto com o valor de `"failed"` no seu `"status"` e inclui todas as mensagens de erro relevantes:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{ORG_ID}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>Um intervalo de pesquisa recomendado é de dois minutos.

## Ler dados do conjunto de dados

Com a ID em lote, é possível usar a API de acesso a dados para ler e verificar todos os arquivos carregados no lote. A resposta retorna uma matriz contendo uma lista de IDs de arquivo, cada uma fazendo referência a um arquivo no lote.

Você também pode usar a API de acesso a dados para retornar o nome, o tamanho em bytes e um link para baixar o arquivo ou a pasta.

Etapas detalhadas para trabalhar com a API de acesso a dados podem ser encontradas no [Guia do desenvolvedor do Data Access](../../data-access/home.md).

## Atualizar o esquema do conjunto de dados

É possível adicionar campos e assimilar dados adicionais em conjuntos de dados criados. Para fazer isso, primeiro é necessário atualizar o schema adicionando propriedades adicionais que definem os novos dados. Isso pode ser feito usando operações PATCH e/ou PUT para atualizar o schema existente.

Para obter mais informações sobre a atualização de schemas, consulte [Guia do desenvolvedor da API do registro de esquema](../../xdm/api/getting-started.md).

Depois de atualizar o esquema, você pode seguir novamente as etapas deste tutorial para assimilar novos dados que estejam em conformidade com o esquema revisado.

É importante lembrar que a evolução do esquema é meramente aditiva, o que significa que você não pode introduzir uma alteração de quebra em um esquema depois que ele for salvo no registro e usado para assimilação de dados. Para saber mais sobre as práticas recomendadas de composição de esquema para uso com o Adobe Experience Platform, consulte o manual na [noções básicas da composição do esquema](../../xdm/schema/composition.md).
