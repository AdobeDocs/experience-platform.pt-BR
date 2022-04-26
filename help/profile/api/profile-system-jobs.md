---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Endpoint da API de tarefas do sistema de perfis
topic-legacy: guide
type: Documentation
description: O Adobe Experience Platform permite que você exclua um conjunto de dados ou lote do armazenamento de Perfil para remover os dados do Perfil do cliente em tempo real que não são mais necessários ou foram adicionados com erro. Isso requer o uso da API de perfil para criar um trabalho do sistema de perfil ou excluir uma solicitação.
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: ba8b62c67cdd6fa011166cc851ffc1c970108835
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 3%

---

# Ponto de extremidade de tarefas do sistema de perfil (solicitações de exclusão)

O Adobe Experience Platform permite assimilar dados de várias fontes e criar perfis robustos para clientes individuais. Dados assimilados em [!DNL Platform] é armazenado no [!DNL Data Lake]e se os conjuntos de dados tiverem sido habilitados para o Perfil, esses dados serão armazenados no [!DNL Real-time Customer Profile] armazenamento de dados também. Ocasionalmente, pode ser necessário excluir um conjunto de dados ou lote do armazenamento do Perfil para remover dados que não são mais necessários ou que foram adicionados com erro. Isso requer o uso da variável [!DNL Real-time Customer Profile] API para criar um [!DNL Profile] trabalho do sistema, ou `delete request`, que também podem ser modificadas, monitoradas ou removidas, se necessário.

>[!NOTE]
>
>Se você estiver tentando excluir conjuntos de dados ou lotes da variável [!DNL Data Lake], visite o [Visão geral do serviço de catálogo](../../catalog/home.md) para obter mais informações.

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, reveja o [guia de introdução](getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Exibir solicitações de exclusão

Uma solicitação de exclusão é um processo assíncrono de longa duração, o que significa que sua organização pode estar executando várias solicitações de exclusão ao mesmo tempo. Para exibir todas as solicitações de exclusão que sua organização está executando no momento, é possível executar uma solicitação de GET para a `/system/jobs` endpoint .

Você também pode usar parâmetros de consulta opcionais para filtrar a lista de solicitações de exclusão retornadas na resposta. Para usar vários parâmetros, separe cada parâmetro usando um E comercial (`&`).

**Formato da API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `start` | Deslocar a página de resultados retornados, de acordo com a hora de criação da solicitação. Exemplo: `start=4` |
| `limit` | Limite o número de resultados retornados. Exemplo: `limit=10` |
| `page` | Retorne uma página específica de resultados, de acordo com o horário de criação da solicitação. Exemplo: `page=2` |
| `sort` | Classifique os resultados por um campo específico em ordem crescente (`asc`) ou decrescente (`desc`). O parâmetro de classificação não funciona ao retornar várias páginas de resultados. Exemplo: `sort=batchId:asc` |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui uma matriz &quot;filho&quot; com um objeto para cada solicitação de exclusão contendo os detalhes dessa solicitação.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
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
|---|---|
| `_page.count` | O número total de solicitações. Essa resposta foi truncada para espaço. |
| `_page.next` | Se existir uma página adicional de resultados, visualize a próxima página de resultados substituindo o valor de ID em uma [solicitação de pesquisa](#view-a-specific-delete-request) com o `"next"` valor fornecido. |
| `jobType` | O tipo de trabalho que está sendo criado. Nesse caso, ele sempre retornará `"DELETE"`. |
| `status` | O status da solicitação de exclusão. Os valores possíveis são `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Um objeto que inclui o número de registros que foram processados (`"recordsProcessed"`) e o tempo em segundos que a solicitação está sendo processada ou o tempo que ela levou para ser concluída (`"timeTakenInSec"`). |

## Criar uma solicitação de exclusão {#create-a-delete-request}

A inicialização de uma nova solicitação de exclusão é feita por meio de uma solicitação POST para a variável `/systems/jobs` endpoint , onde a ID do conjunto de dados ou lote a ser excluído é fornecida no corpo da solicitação.

### Excluir um conjunto de dados

Para excluir um conjunto de dados do armazenamento do Perfil, a ID do conjunto de dados deve ser incluída no corpo da solicitação do POST. Esta ação excluirá TODOS os dados de um determinado conjunto de dados. [!DNL Experience Platform] permite excluir conjuntos de dados com base em esquemas de registro e de série de tempo.

**Formato da API**

```http
POST /system/jobs
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Propriedade | Descrição |
|---|---|
| `dataSetId` | **(Obrigatório)** A ID do conjunto de dados que você deseja excluir. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da solicitação de exclusão recém-criada, incluindo uma ID exclusiva, gerada pelo sistema e somente leitura para a solicitação. Isso pode ser usado para buscar a solicitação e verificar seu status. O `status` para a solicitação no momento da criação é `"NEW"` até que o processamento seja iniciado. O `dataSetId` na resposta deve corresponder ao `dataSetId` enviado na solicitação.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Propriedade | Descrição |
|---|---|
| `id` | A ID exclusiva, gerada pelo sistema e somente leitura da solicitação de exclusão. |
| `dataSetId` | A ID do conjunto de dados, conforme especificado na solicitação do POST. |

### Excluir um lote

Para excluir um lote, a ID do lote deve ser incluída no corpo da solicitação do POST. Lembre-se de que não é possível excluir lotes para conjuntos de dados com base em esquemas de registro. Somente lotes para conjuntos de dados com base em esquemas de séries de tempo podem ser excluídos.

>[!NOTE]
>
> O motivo pelo qual você não pode excluir lotes para conjuntos de dados com base em esquemas de registro é porque os lotes de conjuntos de dados de tipo de registro substituem registros anteriores e, portanto, não podem ser &quot;desfeitos&quot; ou excluídos. A única maneira de remover o impacto de lotes incorretos para conjuntos de dados com base em esquemas de registro é assimilar novamente o lote com os dados corretos para substituir os registros incorretos.

Para obter mais informações sobre o comportamento do registro e da série de tempo, consulte [seção sobre comportamentos de dados XDM](../../xdm/home.md#data-behaviors) no [!DNL XDM System] visão geral.

**Formato da API**

```http
POST /system/jobs
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Propriedade | Descrição |
|---|---|
| `batchId` | **(Obrigatório)** A ID do lote que você deseja excluir. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da solicitação de exclusão recém-criada, incluindo uma ID exclusiva, gerada pelo sistema e somente leitura para a solicitação. Isso pode ser usado para buscar a solicitação e verificar seu status. O `"status"` para a solicitação no momento da criação é `"NEW"` até que o processamento seja iniciado. O `"batchId"` na resposta deve corresponder ao valor `"batchId"` valor enviado na solicitação.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Propriedade | Descrição |
|---|---|
| `id` | A ID exclusiva, gerada pelo sistema e somente leitura da solicitação de exclusão. |
| `batchId` | A ID do lote, conforme especificado na solicitação de POST. |

Se tentar iniciar uma solicitação de exclusão para um lote de conjuntos de dados de Registro, você encontrará um erro de nível 400, semelhante ao seguinte:

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

Para visualizar uma solicitação de exclusão específica, incluindo detalhes como seu status, você pode executar uma solicitação de pesquisa (GET) para a `/system/jobs` e incluir a ID da solicitação de exclusão no caminho.

**Formato da API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obrigatório)** A ID da solicitação de exclusão que você deseja visualizar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta fornece os detalhes da solicitação de exclusão, incluindo seu status atualizado. A ID da solicitação de exclusão na resposta (a variável `"id"` deve corresponder à ID enviada no caminho da solicitação.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Propriedades | Descrição |
|---|---|
| `jobType` | O tipo de trabalho que está sendo criado, nesse caso, ele sempre retornará `"DELETE"`. |
| `status` | O status da solicitação de exclusão. Valores possíveis: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Uma matriz que inclui o número de registros que foram processados (`"recordsProcessed"`) e o tempo em segundos que a solicitação está sendo processada ou o tempo que ela levou para ser concluída (`"timeTakenInSec"`). |

Quando o status da solicitação de exclusão for `"COMPLETED"` é possível confirmar que os dados foram excluídos tentando acessar os dados excluídos usando a API de acesso a dados. Para obter instruções sobre como usar a API de acesso a dados para acessar conjuntos de dados e lotes, consulte o [Documentação de acesso a dados](../../data-access/home.md).

## Remover uma solicitação de exclusão

[!DNL Experience Platform] permite excluir uma solicitação anterior, o que pode ser útil por vários motivos, incluindo se o trabalho de exclusão não tiver sido concluído ou se tiver ficado preso no estágio de processamento. Para remover uma solicitação de exclusão, você pode executar uma solicitação de DELETE para a variável `/system/jobs` endpoint e inclua a ID da solicitação de exclusão que deseja remover para o caminho da solicitação.

**Formato da API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parâmetro | Descrição |
|---|---|
| {DELETE_REQUEST_ID} | A ID da solicitação de exclusão que você deseja remover. |

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. Você pode confirmar que a solicitação foi excluída executando uma solicitação do GET para visualizar a solicitação de exclusão por sua ID. Isso deve retornar um Status HTTP 404 (Não encontrado), indicando que a solicitação de exclusão foi removida.

## Próximas etapas

Agora que você sabe as etapas envolvidas na exclusão de conjuntos de dados e lotes da variável [!DNL Profile Store] within [!DNL Experience Platform], você pode excluir com segurança os dados que foram adicionados incorretamente ou que sua organização não precisa mais. Lembre-se de que uma solicitação de exclusão não pode ser desfeita, portanto, você deve excluir apenas os dados de que está confiante que não é necessário agora e que não serão necessários no futuro.
