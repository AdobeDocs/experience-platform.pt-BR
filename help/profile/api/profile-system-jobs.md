---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Ponto de extremidade da API de trabalhos do sistema de perfil
type: Documentation
description: O Adobe Experience Platform permite excluir um conjunto de dados ou lote do Armazenamento de perfis para remover os dados do Perfil do cliente em tempo real que não são mais necessários ou que foram adicionados por engano. Isso requer o uso da API de perfil para criar um trabalho de sistema de perfil ou excluir solicitação.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 2%

---

# Endpoint de trabalhos do sistema de perfil (solicitações de exclusão)

>[!IMPORTANT]
>
>Os endpoints a seguir podem diferir entre as implementações do Adobe Experience Platform em execução no Microsoft Azure e no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

O Adobe Experience Platform permite assimilar dados de várias fontes e criar perfis robustos para clientes individuais. Os dados assimilados em [!DNL Experience Platform] são armazenados em [!DNL Data Lake] e, se os conjuntos de dados tiverem sido habilitados para Perfil, esses dados também serão armazenados no armazenamento de dados [!DNL Real-Time Customer Profile]. Ocasionalmente, pode ser necessário excluir dados de perfil associados a um conjunto de dados do armazenamento de Perfil para remover dados que não são mais necessários ou foram adicionados por engano. Isso requer o uso da API [!DNL Real-Time Customer Profile] para criar um trabalho do sistema [!DNL Profile], ou &quot;excluir solicitação&quot;.

>[!NOTE]
>
>Se você estiver tentando excluir conjuntos de dados ou lotes de [!DNL Data Lake], visite a [Visão geral do Serviço de Catálogo](../../catalog/home.md) para obter mais informações.

## Introdução

O ponto de extremidade de API usado neste guia faz parte de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Exibir solicitações de exclusão {#view}

Uma solicitação de exclusão é um processo assíncrono de longa duração, o que significa que sua organização pode estar executando várias solicitações de exclusão de uma só vez. Para exibir todas as solicitações de exclusão executadas atualmente pela sua organização, é possível executar uma solicitação GET para o ponto de extremidade `/system/jobs`.

Você também pode usar parâmetros de consulta opcionais para filtrar a lista de solicitações de exclusão retornadas na resposta. Para usar vários parâmetros, separe cada parâmetro usando um E comercial (`&`).

**Formato da API**

>[!AVAILABILITY]
>
>Os seguintes parâmetros de consulta estão **somente** disponíveis ao usar o Experience Platform no Microsoft Azure.
>
>Ao usar esse endpoint no AWS, as primeiras 100 tarefas do sistema são retornadas em ordem decrescente, com base na data de criação.

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `start` | Deslocar a página de resultados retornados de acordo com o tempo de criação da solicitação. | `start=4` |
| `limit` | Limitar o número de resultados retornados. | `limit=10` |
| `page` | Retornar uma página específica de resultados, de acordo com o horário de criação da solicitação. | `page=2` |
| `sort` | Classificar os resultados por um campo específico em ordem crescente (`asc`) ou decrescente (`desc`). O parâmetro de classificação não funciona ao retornar várias páginas de resultados. | `sort=batchId:asc` |

**Solicitação**

>[!IMPORTANT]
>
>A solicitação a seguir é diferente entre as instâncias do Azure e do AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Um exemplo de solicitação para visualizar seus trabalhos do sistema.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Você **deve** usar o cabeçalho de solicitação `x-sandbox-id` em vez do cabeçalho de solicitação `x-sandbox-name` ao usar este ponto de extremidade com o AWS.

+++ Um exemplo de solicitação para visualizar seus trabalhos do sistema.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
```

+++

>[!ENDTABS]

**Resposta**

>[!IMPORTANT]
>
>A resposta a seguir é diferente entre as instâncias do Azure e do AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Uma resposta bem-sucedida inclui uma matriz &quot;filho&quot; com um objeto para cada solicitação de exclusão contendo os detalhes dessa solicitação.

+++ Uma resposta bem-sucedida para exibir as solicitações de exclusão

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `_page.count` | O número total de solicitações. Esta resposta foi truncada por questões de espaço. |
| `_page.next` | Se houver uma página adicional de resultados, exiba a próxima página de resultados substituindo o valor da ID em uma [solicitação de pesquisa](#view-a-specific-delete-request) pelo valor `"next"` fornecido. |
| `jobType` | O tipo de trabalho sendo criado. Nesse caso, ele sempre retornará `"DELETE"`. |
| `status` | O status da solicitação de exclusão. Os valores possíveis incluem `"NEW"`, `"PROCESSING"`, `"COMPLETED"` e `"ERROR"`. |
| `metrics` | Um objeto que inclui o número de registros que foram processados (`"recordsProcessed"`) e o tempo em segundos que a solicitação foi processada ou quanto tempo a solicitação levou para ser concluída (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

Uma resposta bem-sucedida retorna uma matriz que contém um objeto para cada solicitação do sistema.

+++ Uma resposta bem-sucedida para exibir as solicitações do sistema

```json
{
    [
        {
            "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
            "requestType": "DELETE_EE_BATCH",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        },
        {
            "requestId": "38a835eb-b491-4864-902b-be07fa4d6a6d",
            "requestType": "TRUNCATE_DATASET",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        }        
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `requestId` | A ID do trabalho do sistema. |
| `requestType` | O tipo de trabalho do sistema. Os valores possíveis incluem `BACKFILL_TTL`, `DELETE_EE_BATCH` e `TRUNCATE_DATASET`. |
| `status` | O status do trabalho do sistema. Os valores possíveis incluem `NEW`, `SUCCESS`, `ERROR`, `FAILED` e `IN-PROGRESS`. |
| `properties` | Um objeto que contém IDs de lote e/ou conjunto de dados do trabalho do sistema. |

+++

>[!ENDTABS]

## Criar uma solicitação de exclusão {#create-a-delete-request}

O início de uma nova solicitação de exclusão é feito por meio de uma solicitação POST para o ponto de extremidade `/systems/jobs`, em que a ID do conjunto de dados ou lote a ser excluído é fornecida no corpo da solicitação.

### Excluir um conjunto de dados e dados de perfil associados

Para excluir um conjunto de dados e todos os dados de perfil associados ao conjunto de dados do armazenamento de Perfil, a ID do conjunto de dados deve ser incluída no corpo da solicitação POST. Esta ação excluirá TODOS os dados de um determinado conjunto de dados. [!DNL Experience Platform] permite excluir conjuntos de dados com base em esquemas de série de tempo e registro.

**Formato da API**

```http
POST /system/jobs
```

**Solicitação**

>[!IMPORTANT]
>
>A solicitação a seguir é diferente entre as instâncias do Azure e do AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Uma solicitação de amostra para excluir um conjunto de dados.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Propriedade | Descrição |
| -------- | ----------- |
| `dataSetId` | A ID do conjunto de dados que você deseja excluir. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Você **deve** usar o cabeçalho de solicitação `x-sandbox-id` em vez do cabeçalho de solicitação `x-sandbox-name` ao usar este ponto de extremidade com o AWS.

+++ Uma solicitação de amostra para excluir um conjunto de dados.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Propriedade | Descrição |
| -------- | ----------- |
| `dataSetId` | A ID do conjunto de dados que você deseja excluir. |

>[!ENDTABS]

**Resposta**

>[!IMPORTANT]
>
>A resposta a seguir é diferente entre as instâncias do Azure e do AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Uma resposta bem-sucedida retorna os detalhes da solicitação de exclusão recém-criada, incluindo uma ID exclusiva gerada pelo sistema e somente leitura para a solicitação. Isso pode ser usado para pesquisar a solicitação e verificar seu status. O `status` para a solicitação no momento da criação é `"NEW"` até que comece a ser processado. O `dataSetId` na resposta deve corresponder ao `dataSetId` enviado na solicitação.

+++ Uma resposta bem-sucedida para criar uma solicitação de exclusão.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | A ID exclusiva, gerada pelo sistema, somente leitura da solicitação de exclusão. |
| `dataSetId` | A ID do conjunto de dados, conforme especificado na solicitação POST. |

+++

>[!TAB Amazon Web Services (AWS)]

Uma resposta bem-sucedida retorna os detalhes da solicitação do sistema recém-criada.

+++ Uma resposta bem-sucedida para criar uma solicitação de exclusão.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `requestId` | A ID do trabalho do sistema. |
| `requestType` | O tipo de trabalho do sistema. Os valores possíveis incluem `BACKFILL_TTL`, `DELETE_EE_BATCH` e `TRUNCATE_DATASET`. |
| `status` | O status do trabalho do sistema. Os valores possíveis incluem `NEW`, `SUCCESS`, `ERROR`, `FAILED` e `IN-PROGRESS`. |
| `properties` | Um objeto que contém IDs de lote e/ou conjunto de dados do trabalho do sistema. |

+++

>[!ENDTABS]

### Excluir um lote

Para excluir um lote, a ID do lote deve ser incluída no corpo da solicitação POST. Observe que não é possível excluir lotes para conjuntos de dados com base em esquemas de registro. Somente lotes para conjuntos de dados com base em esquemas de série temporal podem ser excluídos.

>[!NOTE]
>
> O motivo pelo qual você não pode excluir lotes para conjuntos de dados com base em esquemas de registro é porque os lotes do conjunto de dados do tipo de registro substituem os registros anteriores e, portanto, não podem ser &quot;desfeitos&quot; ou excluídos. A única maneira de remover o impacto de lotes errados para conjuntos de dados com base em esquemas de registro é assimilar novamente o lote com os dados corretos para substituir os registros incorretos.

Para obter mais informações sobre comportamento de registro e série temporal, consulte a [seção sobre comportamentos de dados XDM](../../xdm/home.md#data-behaviors) na visão geral de [!DNL XDM System].

**Formato da API**

```http
POST /system/jobs
```

**Solicitação**

>[!IMPORTANT]
>
>A solicitação a seguir é diferente entre as instâncias do Azure e do AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Uma solicitação de amostra para excluir um lote.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Propriedade | Descrição |
| -------- | ----------- |
| `datasetId` | A ID do conjunto de dados do lote que você deseja excluir. |
| `batchId` | A ID do lote que você deseja excluir. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Você **deve** usar o cabeçalho de solicitação `x-sandbox-id` em vez do cabeçalho de solicitação `x-sandbox-name` ao usar este ponto de extremidade com o AWS.

+++ Uma solicitação de amostra para excluir um lote.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Propriedade | Descrição |
| -------- | ----------- |
| `datasetId` | A ID do conjunto de dados do lote que você deseja excluir. |
| `batchId` | A ID do lote que você deseja excluir. |

>[!ENDTABS]

**Resposta**

>[!IMPORTANT]
>
>A resposta a seguir é diferente entre as instâncias do Azure e do AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Uma resposta bem-sucedida retorna os detalhes da solicitação de exclusão recém-criada, incluindo uma ID exclusiva gerada pelo sistema e somente leitura para a solicitação. Isso pode ser usado para pesquisar a solicitação e verificar seu status. O `"status"` para a solicitação no momento da criação é `"NEW"` até que comece a ser processado. O valor `"batchId"` na resposta deve corresponder ao valor `"batchId"` enviado na solicitação.

+++ Uma resposta bem-sucedida para criar uma solicitação de exclusão.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "66a92c5910df2d1767de13f3",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | A ID exclusiva, gerada pelo sistema, somente leitura da solicitação de exclusão. |
| `datasetId` | A ID do conjunto de dados especificado. |
| `batchId` | A ID do lote, conforme especificado na solicitação POST. |

+++

>[!TAB Amazon Web Services (AWS)]

Uma resposta bem-sucedida retorna os detalhes da solicitação do sistema recém-criada.

+++ Uma resposta bem-sucedida para criar uma solicitação de exclusão.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `requestId` | A ID do trabalho do sistema. |
| `requestType` | O tipo de trabalho do sistema. Os valores possíveis incluem `BACKFILL_TTL`, `DELETE_EE_BATCH` e `TRUNCATE_DATASET`. |
| `status` | O status do trabalho do sistema. Os valores possíveis incluem `NEW`, `SUCCESS`, `ERROR`, `FAILED` e `IN-PROGRESS`. |
| `properties` | Um objeto que contém IDs de lote e/ou conjunto de dados do trabalho do sistema. |

+++

>[!ENDTABS]

>[!AVAILABILITY]
>
>O seguinte recurso está disponível **somente** ao usar o Experience Platform no Microsoft Azure.

Se você tentar iniciar uma solicitação de exclusão para um lote de conjunto de dados de Registro, encontrará um erro de nível 400, semelhante ao seguinte:

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Exibir uma solicitação de exclusão específica {#view-a-specific-delete-request}

Para exibir uma solicitação de exclusão específica, incluindo detalhes como seu status, você pode executar uma solicitação de pesquisa (GET) para o ponto de extremidade `/system/jobs` e incluir a ID da solicitação de exclusão no caminho.

**Formato da API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DELETE_REQUEST_ID}` | A ID da solicitação de exclusão que você deseja exibir. |

**Solicitação**

>[!IMPORTANT]
>
>A solicitação a seguir é diferente entre as instâncias do Azure e do AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Uma solicitação de amostra para exibir um trabalho de perfil.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Você **deve** usar o cabeçalho de solicitação `x-sandbox-id` em vez do cabeçalho de solicitação `x-sandbox-name` ao usar este ponto de extremidade com o AWS.

+++ Uma solicitação de amostra para exibir um trabalho de perfil.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

+++

>[!ENDTABS]


**Resposta**

>[!IMPORTANT]
>
>A resposta a seguir é diferente entre as instâncias do Azure e do AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

A resposta fornece os detalhes da solicitação de exclusão, incluindo o status atualizado. A ID da solicitação de exclusão na resposta (o valor `"id"`) deve corresponder à ID enviada no caminho da solicitação.

+++ Uma resposta bem-sucedida para exibir uma solicitação de exclusão.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Propriedades | Descrição |
| ---------- | ----------- |
| `jobType` | O tipo de trabalho que está sendo criado, nesse caso, ele sempre retornará `"DELETE"`. |
| `status` | O status da solicitação de exclusão. Os valores possíveis incluem `NEW`, `PROCESSING`, `COMPLETED` e `ERROR`. |
| `metrics` | Uma matriz que inclui o número de registros que foram processados (`"recordsProcessed"`) e o tempo em segundos que a solicitação foi processada ou quanto tempo a solicitação levou para ser concluída (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

Uma resposta bem-sucedida retorna os detalhes da solicitação do sistema especificada.

+++ Uma resposta bem-sucedida para exibir uma solicitação de exclusão.

```json
{
    "requestId": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `requestId` | A ID do trabalho do sistema. |
| `requestType` | O tipo de trabalho do sistema. Os valores possíveis incluem `BACKFILL_TTL`, `DELETE_EE_BATCH` e `TRUNCATE_DATASET`. |
| `status` | O status do trabalho do sistema. Os valores possíveis incluem `NEW`, `SUCCESS`, `ERROR`, `FAILED` e `IN-PROGRESS`. |
| `properties` | Um objeto que contém IDs de lote e/ou conjunto de dados do trabalho do sistema. |

+++

>[!ENDTABS]

Quando o status da solicitação de exclusão for `"COMPLETED"`, você poderá confirmar que os dados foram excluídos tentando acessá-los usando a API de acesso a dados. Para obter instruções sobre como usar a API de acesso a dados para acessar conjuntos de dados e lotes, consulte a [documentação sobre acesso a dados](../../data-access/home.md).

## Remover uma solicitação de exclusão

>[!AVAILABILITY]
>
>Este ponto de extremidade **só** tem suporte na instância do Azure do Adobe Experience Platform e **não** tem suporte na instância do AWS.

[!DNL Experience Platform] permite que você exclua uma solicitação anterior, o que pode ser útil por vários motivos, incluindo se o trabalho de exclusão não foi concluído ou ficou preso no estágio de processamento. Para remover uma solicitação de exclusão, você pode executar uma solicitação DELETE para o ponto de extremidade `/system/jobs` e incluir a ID da solicitação de exclusão que você deseja remover no caminho da solicitação.

**Formato da API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| {DELETE_REQUEST_ID} | A ID da solicitação de exclusão que você deseja remover. |

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. É possível confirmar se a solicitação foi excluída executando uma solicitação do GET para visualizar a solicitação de exclusão por sua ID. Isso deve retornar um Status HTTP 404 (Não encontrado), indicando que a solicitação de exclusão foi removida.

## Próximas etapas

Agora que você sabe as etapas envolvidas na exclusão de conjuntos de dados e lotes do [!DNL Profile store] no [!DNL Experience Platform], é possível excluir com segurança dados que foram adicionados incorretamente ou que sua organização não precisa mais. Lembre-se de que uma solicitação de exclusão não pode ser desfeita, portanto, você só deve excluir dados de que está confiante de que não são necessários agora e não serão necessários no futuro.
