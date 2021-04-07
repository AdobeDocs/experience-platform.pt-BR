---
keywords: Experience Platform, home, tópicos populares, conjunto de dados, conjunto de dados, criar um conjunto de dados, criar um conjunto de dados
solution: Experience Platform
title: Criar um conjunto de dados usando APIs
topic: conjuntos de dados
description: Este documento fornece etapas gerais para criar um conjunto de dados usando APIs do Adobe Experience Platform e preencher o conjunto de dados usando um arquivo.
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 1%

---

# Criar um conjunto de dados usando APIs

Este documento fornece etapas gerais para criar um conjunto de dados usando APIs do Adobe Experience Platform e preencher o conjunto de dados usando um arquivo.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Ingestão](../../ingestion/batch-ingestion/overview.md) em lote:  [!DNL Experience Platform] O permite assimilar dados como arquivos em lote.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs [!DNL Platform].

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Tutorial

Para criar um conjunto de dados, um schema deve ser definido primeiro. Um schema é um conjunto de regras para ajudar a representar dados. Além de descrever a estrutura dos dados, os esquemas fornecem restrições e expectativas que podem ser aplicadas e usadas para validar dados conforme são movidos entre sistemas.

Essas definições padrão permitem que os dados sejam interpretados de forma consistente, independentemente da origem, e removem a necessidade de tradução entre aplicativos. Para obter mais informações sobre a composição de schemas, consulte o guia sobre as [noções básicas da composição do schema](../../xdm/schema/composition.md)

## Pesquisar um esquema de conjunto de dados

Este tutorial começa onde o [Tutorial da API do Registro de Esquema](../../xdm/tutorials/create-schema-api.md) termina, utilizando o esquema Membros da Fidelidade criado durante esse tutorial.

Se você não concluiu o tutorial [!DNL Schema Registry], comece por lá e continue com este tutorial de conjunto de dados somente depois de ter composto o schema necessário.

A chamada a seguir pode ser usada para exibir o esquema Membros de Fidelidade criado durante o tutorial da API [!DNL Schema Registry]:

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O formato do objeto de resposta depende do cabeçalho Accept enviado na solicitação. As propriedades individuais nessa resposta foram minimizadas para espaço.

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
    "imsOrg": "{IMS_ORG}",
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

Com o esquema Membros do programa de fidelidade em vigor, agora é possível criar um conjunto de dados que faça referência ao esquema.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `schemaRef.id` | O valor de URI `$id` para o esquema XDM no qual o conjunto de dados será baseado. |
| `schemaRef.contentType` | Indica o formato e a versão do esquema. Consulte a seção sobre [controle de versão do schema](../../xdm/api/getting-started.md#versioning) no guia da API XDM para obter mais informações. |

>[!NOTE]
>
>Este tutorial usa o formato de arquivo [Apache Parquet](https://parquet.apache.org/documentation/latest/) para todos os seus exemplos. Um exemplo que usa o formato de arquivo JSON pode ser encontrado no [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md)

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta que consiste em uma matriz que contém a ID do conjunto de dados recém-criado no formato `"@/datasets/{DATASET_ID}"`. A ID do conjunto de dados é uma string gerada pelo sistema e somente leitura, usada para fazer referência ao conjunto de dados nas chamadas de API.

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

O corpo da solicitação inclui um campo &quot;datasetId&quot;, cujo valor é `{DATASET_ID}` gerado na etapa anterior.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna o Status HTTP 201 (Criado) e um objeto de resposta contendo detalhes do lote recém-criado, incluindo seu `id`, uma sequência de caracteres gerada pelo sistema somente leitura.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
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

## Upload de arquivos em um lote

Depois de criar com êxito um novo lote para upload, agora é possível fazer upload de arquivos para o conjunto de dados específico. É importante lembrar que, ao definir o conjunto de dados, você especificou o formato de arquivo como Parquet. Portanto, os arquivos carregados devem estar nesse formato.

>[!NOTE]
>
>O maior arquivo de upload de dados compatível é de 512 MB. Se o arquivo de dados for maior que esse, ele precisará ser dividido em partes que não excedam 512 MB, para ser carregado uma de cada vez. Você pode fazer upload de cada arquivo no mesmo lote repetindo essa etapa para cada arquivo, usando a mesma ID de lote. Não há limite para o número se os arquivos forem carregados como parte de um lote.

**Formato da API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BATCH_ID}` | O `id` do lote para o qual você está fazendo upload. |
| `{DATASET_ID}` | O `id` do conjunto de dados no qual o lote será mantido. |
| `{FILE_NAME}` | O nome do arquivo que você está fazendo upload. |

**Solicitação**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Resposta**

Um arquivo carregado com êxito retorna um corpo de resposta em branco e o Status HTTP 200 (OK).

## Conclusão do lote de sinais

Após fazer upload de todos os arquivos de dados para o lote, é possível sinalizar o lote para conclusão. A conclusão da sinalização faz com que o serviço crie entradas [!DNL Catalog] `DataSetFile` para os arquivos carregados e as associe ao lote gerado anteriormente. O lote [!DNL Catalog] é marcado como bem-sucedido, o que aciona todos os fluxos de downstream que podem então funcionar nos dados agora disponíveis.

**Formato da API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parâmetro | Descrição |
| --- | --- |
| `{BATCH_ID}` | O `id` do lote que você está marcando como concluído. |

**Solicitação**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Resposta**

Um lote concluído com êxito retorna um corpo de resposta em branco e o Status HTTP 200 (OK).

## Assimilação do monitor

Dependendo do tamanho dos dados, os lotes levam longos períodos de tempo variáveis para serem assimilados. Você pode monitorar o status de um lote ao anexar um parâmetro de solicitação `batch` contendo a ID do lote a uma solicitação `GET /batches`. A API pesquisa o conjunto de dados para o status do lote a partir da assimilação até que `status` na resposta indique conclusão (&quot;sucesso&quot; ou &quot;falha&quot;).

**Formato da API**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BATCH_ID}` | O `id` do lote que você deseja monitorar. |

**Solicitação**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Resposta**

Uma resposta positiva retorna um objeto com seu atributo `status` contendo o valor de `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
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

Uma resposta negativa retorna um objeto com o valor `"failed"` em seu atributo `"status"` e inclui quaisquer mensagens de erro relevantes:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
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
>Um intervalo de sondagem recomendado é de dois minutos.

## Ler dados do conjunto de dados

Com a ID de lote, é possível usar a API de acesso a dados para ler novamente e verificar todos os arquivos carregados no lote. A resposta retorna uma matriz contendo uma lista de IDs de arquivo, cada uma fazendo referência a um arquivo no lote.

Você também pode usar a API de acesso a dados para retornar o nome, o tamanho em bytes e um link para baixar o arquivo ou a pasta.

As etapas detalhadas para trabalhar com a API de acesso a dados podem ser encontradas no [Guia do desenvolvedor de acesso a dados](../../data-access/home.md).

## Atualizar o esquema do conjunto de dados

Você pode adicionar campos e assimilar dados adicionais em conjuntos de dados criados. Para fazer isso, primeiro é necessário atualizar o schema adicionando propriedades adicionais que definem os novos dados. Isso pode ser feito usando operações PATCH e/ou PUT para atualizar o schema existente.

Para obter mais informações sobre a atualização de schemas, consulte o [Guia do desenvolvedor da API do Registro de Schema](../../xdm/api/getting-started.md).

Depois de atualizar o schema, você pode seguir novamente as etapas deste tutorial para assimilar novos dados que estejam em conformidade com o schema revisado.

É importante lembrar que a evolução do schema é meramente aditiva, o que significa que não é possível introduzir uma alteração de quebra em um schema depois de ele ter sido salvo no registro e usado para assimilação de dados. Para saber mais sobre as práticas recomendadas para compor o schema a ser usado com o Adobe Experience Platform, consulte o guia sobre as [noções básicas da composição do schema](../../xdm/schema/composition.md).
