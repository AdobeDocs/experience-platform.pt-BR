---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Ponto de extremidade da API de trabalhos do sistema de perfil
type: Documentation
description: O Adobe Experience Platform permite excluir um conjunto de dados ou lote do Armazenamento de perfis para remover os dados do Perfil do cliente em tempo real que não são mais necessários ou que foram adicionados por engano. Isso requer o uso da API de perfil para criar um trabalho de sistema de perfil ou excluir solicitação.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 3%

---

# Endpoint de trabalhos do sistema de perfil (solicitações de exclusão)

O Adobe Experience Platform permite assimilar dados de várias fontes e criar perfis robustos para clientes individuais. Os dados assimilados em [!DNL Platform] são armazenados em [!DNL Data Lake] e, se os conjuntos de dados tiverem sido habilitados para Perfil, esses dados também serão armazenados no armazenamento de dados [!DNL Real-Time Customer Profile]. Ocasionalmente, pode ser necessário excluir dados de perfil associados a um conjunto de dados do armazenamento de Perfil para remover dados que não são mais necessários ou foram adicionados por engano. Isso requer o uso da API [!DNL Real-Time Customer Profile] para criar um trabalho do sistema [!DNL Profile], ou `delete request`, que também pode ser modificado, monitorado ou removido, se necessário.

>[!NOTE]
>
>Se você estiver tentando excluir conjuntos de dados ou lotes de [!DNL Data Lake], visite a [Visão geral do Serviço de Catálogo](../../catalog/home.md) para obter mais informações.

## Introdução

O ponto de extremidade de API usado neste guia faz parte de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas para qualquer API Experience Platform com êxito.

## Exibir solicitações de exclusão

Uma solicitação de exclusão é um processo assíncrono de longa duração, o que significa que sua organização pode estar executando várias solicitações de exclusão de uma só vez. Para exibir todas as solicitações de exclusão executadas atualmente pela sua organização, é possível executar uma solicitação GET para o ponto de extremidade `/system/jobs`.

Você também pode usar parâmetros de consulta opcionais para filtrar a lista de solicitações de exclusão retornadas na resposta. Para usar vários parâmetros, separe cada parâmetro usando um E comercial (`&`).

**Formato da API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `start` | Deslocar a página de resultados retornados de acordo com o tempo de criação da solicitação. Exemplo: `start=4` |
| `limit` | Limitar o número de resultados retornados. Exemplo: `limit=10` |
| `page` | Retornar uma página específica de resultados, de acordo com o horário de criação da solicitação. Exemplo: `page=2` |
| `sort` | Classificar os resultados por um campo específico em ordem crescente (`asc`) ou decrescente (`desc`). O parâmetro de classificação não funciona ao retornar várias páginas de resultados. Exemplo: `sort=batchId:asc` |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
|---|---|
| `_page.count` | O número total de solicitações. Esta resposta foi truncada por questões de espaço. |
| `_page.next` | Se houver uma página adicional de resultados, exiba a próxima página de resultados substituindo o valor da ID em uma [solicitação de pesquisa](#view-a-specific-delete-request) pelo valor `"next"` fornecido. |
| `jobType` | O tipo de trabalho sendo criado. Nesse caso, ele sempre retornará `"DELETE"`. |
| `status` | O status da solicitação de exclusão. Os valores possíveis são `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Um objeto que inclui o número de registros que foram processados (`"recordsProcessed"`) e o tempo em segundos que a solicitação foi processada ou quanto tempo a solicitação levou para ser concluída (`"timeTakenInSec"`). |

## Criar uma solicitação de exclusão {#create-a-delete-request}

A inicialização de uma nova solicitação de exclusão é feita por meio de uma solicitação POST para o ponto de extremidade `/systems/jobs`, em que a ID do conjunto de dados ou lote a ser excluído é fornecida no corpo da solicitação.

### Excluir um conjunto de dados e dados de perfil associados

Para excluir um conjunto de dados e todos os dados de perfil associados ao conjunto de dados do armazenamento de Perfil, a ID do conjunto de dados deve ser incluída no corpo da solicitação POST. Esta ação excluirá TODOS os dados de um determinado conjunto de dados. [!DNL Experience Platform] permite excluir conjuntos de dados com base em esquemas de série de tempo e registro.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Propriedade | Descrição |
|---|---|
| `dataSetId` | **(Obrigatório)** A ID do conjunto de dados que você deseja excluir. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da solicitação de exclusão recém-criada, incluindo uma ID exclusiva gerada pelo sistema e somente leitura para a solicitação. Isso pode ser usado para pesquisar a solicitação e verificar seu status. O `status` para a solicitação no momento da criação é `"NEW"` até que comece a ser processado. O `dataSetId` na resposta deve corresponder ao `dataSetId` enviado na solicitação.

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
|---|---|
| `id` | A ID exclusiva, gerada pelo sistema, somente leitura da solicitação de exclusão. |
| `dataSetId` | A ID do conjunto de dados, conforme especificado na solicitação POST. |

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

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Propriedade | Descrição |
|---|---|
| `batchId` | **(Obrigatório)** A ID do lote que você deseja excluir. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da solicitação de exclusão recém-criada, incluindo uma ID exclusiva gerada pelo sistema e somente leitura para a solicitação. Isso pode ser usado para pesquisar a solicitação e verificar seu status. O `"status"` para a solicitação no momento da criação é `"NEW"` até que comece a ser processado. O valor `"batchId"` na resposta deve corresponder ao valor `"batchId"` enviado na solicitação.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Propriedade | Descrição |
|---|---|
| `id` | A ID exclusiva, gerada pelo sistema, somente leitura da solicitação de exclusão. |
| `batchId` | A ID do lote, conforme especificado na solicitação POST. |

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
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obrigatório)** A ID da solicitação de exclusão que você deseja exibir. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta fornece os detalhes da solicitação de exclusão, incluindo o status atualizado. A ID da solicitação de exclusão na resposta (o valor `"id"`) deve corresponder à ID enviada no caminho da solicitação.

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
|---|---|
| `jobType` | O tipo de trabalho que está sendo criado, nesse caso, ele sempre retornará `"DELETE"`. |
| `status` | O status da solicitação de exclusão. Valores possíveis: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Uma matriz que inclui o número de registros que foram processados (`"recordsProcessed"`) e o tempo em segundos que a solicitação foi processada ou quanto tempo a solicitação levou para ser concluída (`"timeTakenInSec"`). |

Quando o status da solicitação de exclusão for `"COMPLETED"`, você poderá confirmar que os dados foram excluídos tentando acessá-los usando a API de acesso a dados. Para obter instruções sobre como usar a API de acesso a dados para acessar conjuntos de dados e lotes, consulte a [documentação sobre acesso a dados](../../data-access/home.md).

## Remover uma solicitação de exclusão

[!DNL Experience Platform] permite que você exclua uma solicitação anterior, o que pode ser útil por vários motivos, incluindo se o trabalho de exclusão não foi concluído ou ficou preso no estágio de processamento. Para remover uma solicitação de exclusão, você pode executar uma solicitação DELETE para o ponto de extremidade `/system/jobs` e incluir a ID da solicitação de exclusão que você deseja remover no caminho da solicitação.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. É possível confirmar se a solicitação foi excluída executando uma solicitação do GET para visualizar a solicitação de exclusão por sua ID. Isso deve retornar um Status HTTP 404 (Não encontrado), indicando que a solicitação de exclusão foi removida.

## Próximas etapas

Agora que você sabe as etapas envolvidas na exclusão de conjuntos de dados e lotes do [!DNL Profile store] no [!DNL Experience Platform], é possível excluir com segurança dados que foram adicionados incorretamente ou que sua organização não precisa mais. Lembre-se de que uma solicitação de exclusão não pode ser desfeita, portanto, você só deve excluir dados de que está confiante de que não são necessários agora e não serão necessários no futuro.
