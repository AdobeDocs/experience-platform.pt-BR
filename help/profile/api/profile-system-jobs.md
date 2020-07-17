---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Trabalhos do sistema do Perfil - API do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 2%

---


# Ponto final de trabalhos do sistema de Perfil (Excluir solicitações)

O Adobe Experience Platform permite que você ingira dados de várias fontes e crie perfis robustos para clientes individuais. Os dados ingeridos [!DNL Platform] são armazenados no armazenamento [!DNL Data Lake] e no [!DNL Real-time Customer Profile] armazenamento de dados. Ocasionalmente, pode ser necessário excluir um conjunto de dados ou lote do Perfil Store para remover dados que não são mais necessários ou que foram adicionados por erro. Isso requer o uso da [!DNL Real-time Customer Profile] API para criar um trabalho do [!DNL Profile] sistema, também conhecido como &quot;[!DNL delete request]&quot;, que também pode ser modificado, monitorado ou removido, se necessário.

>[!NOTE]
>Se você estiver tentando excluir conjuntos de dados ou lotes do [!DNL Data Lake], visite a visão geral [do Serviço de](../../catalog/home.md) catálogo para obter instruções.

## Introdução

O endpoint da API usado neste guia faz parte do [!DNL Real-time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Antes de continuar, reveja o guia [de](getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Visualização de solicitações de exclusão

Uma solicitação de exclusão é um processo assíncrono de longa duração, o que significa que sua organização pode estar executando várias solicitações de exclusão ao mesmo tempo. Para visualização de todas as solicitações de exclusão que sua organização está executando no momento, é possível executar uma solicitação GET para o `/system/jobs` endpoint.

Você também pode usar parâmetros de query opcionais para filtrar a lista de solicitações de exclusão retornadas na resposta. Para usar vários parâmetros, separe cada parâmetro usando um E comercial (&amp;).

**Formato da API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `start` | Deslocar a página de resultados retornados, de acordo com a hora de criação da solicitação. Exemplo: *`start=4`* |
| `limit` | Limite o número de resultados retornados. Exemplo: *`limit=10`* |
| `page` | Retorna uma página específica de resultados, de acordo com a hora de criação da solicitação. Exemplo: ***`page=2`*** |
| `sort` | Classifique os resultados por um campo específico em ordem crescente (*`asc`*) ou decrescente (**`desc`**). O parâmetro de classificação não funciona ao retornar várias páginas de resultados. Exemplo: `sort=batchId:asc` |

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui uma matriz &quot;filhos&quot; com um objeto para cada solicitação de exclusão que contém os detalhes dessa solicitação.

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
| `_page.next` | Se existir uma página adicional de resultados, visualização a próxima página de resultados substituindo o valor da ID em uma solicitação [de](#view-a-specific-delete-request) pesquisa pelo `"next"` valor fornecido. |
| `jobType` | O tipo de trabalho que está sendo criado. Nesse caso, ele sempre voltará `"DELETE"`. |
| `status` | O status da solicitação de exclusão. Os valores possíveis são `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Um objeto que inclui o número de registros que foram processados (`"recordsProcessed"`) e o tempo em segundos que a solicitação está sendo processada, ou o tempo que a solicitação levou para ser concluída (`"timeTakenInSec"`). |

## Criar uma solicitação de exclusão {#create-a-delete-request}

A inicialização de uma nova solicitação de exclusão é feita por meio de uma solicitação POST para o `/systems/jobs` ponto de extremidade, onde a ID do conjunto de dados ou lote a ser excluído é fornecida no corpo da solicitação.

### Excluir um conjunto de dados

Para excluir um conjunto de dados, a ID do conjunto de dados deve ser incluída no corpo da solicitação POST. Esta ação excluirá TODOS os dados de um dado conjunto de dados. [!DNL Experience Platform] permite que você exclua conjuntos de dados com base em schemas de registro e de série de tempo.

>[!CAUTION]
> Ao tentar excluir um conjunto de dados [!DNL Profile]habilitado usando a [!DNL Experience Platform] interface do usuário, o conjunto de dados é desabilitado para inclusão, mas não será excluído até que uma solicitação de exclusão seja criada usando a API. Para obter mais informações, consulte o [apêndice](#appendix) a este documento.

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

Uma resposta bem-sucedida retorna os detalhes da solicitação de exclusão recém-criada, incluindo uma ID exclusiva gerada pelo sistema e somente leitura para a solicitação. Isso pode ser usado para procurar a solicitação e verificar seu status. A solicitação **`status`** no momento da criação é feita *`"NEW"`* até que comece o processamento. A resposta **`dataSetId`** deve corresponder à ***`dataSetId`*** enviada na solicitação.

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
| `id` | A ID exclusiva gerada pelo sistema e somente leitura da solicitação de exclusão. |
| `dataSetId` | A ID do conjunto de dados, conforme especificado na solicitação POST. |

### Excluir um lote

Para excluir um lote, a ID do lote deve ser incluída no corpo da solicitação POST. Lembre-se de que não é possível excluir lotes para conjuntos de dados com base em schemas de registro. Somente lotes para conjuntos de dados com base em schemas de séries de tempo podem ser excluídos.

>[!NOTE]
> O motivo pelo qual você não pode excluir lotes de conjuntos de dados com base em schemas de registro é porque os lotes de conjuntos de dados de tipo de registro substituem registros anteriores e, portanto, não podem ser &quot;desfeitos&quot; ou excluídos. A única maneira de remover o impacto de lotes errados para conjuntos de dados baseados em schemas de registro é ingerir novamente o lote com os dados corretos para substituir os registros incorretos.

Para obter mais informações sobre o comportamento de registro e série de tempo, consulte a [seção sobre comportamentos](../../xdm/home.md#data-behaviors) de dados XDM na [!DNL XDM System] visão geral.

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

Uma resposta bem-sucedida retorna os detalhes da solicitação de exclusão recém-criada, incluindo uma ID exclusiva gerada pelo sistema e somente leitura para a solicitação. Isso pode ser usado para procurar a solicitação e verificar seu status. A solicitação `"status"` no momento da criação é feita `"NEW"` até que comece o processamento. A resposta `"batchId"` deve corresponder à `"batchId"` enviada na solicitação.

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
| `id` | A ID exclusiva gerada pelo sistema e somente leitura da solicitação de exclusão. |
| `batchId` | A ID do lote, conforme especificado na solicitação POST. |

Se você tentar iniciar uma solicitação de exclusão para um lote de conjuntos de dados de Registro, ocorrerá um erro de nível 400, semelhante ao seguinte:

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

## Visualização de uma solicitação de exclusão específica {#view-a-specific-delete-request}

Para visualização de uma solicitação de exclusão específica, incluindo detalhes como seu status, é possível executar uma solicitação de pesquisa (GET) para o `/system/jobs` ponto de extremidade e incluir a ID da solicitação de exclusão no caminho.

**Formato da API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obrigatório)** A ID da solicitação de exclusão que você deseja visualização. |

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

A resposta fornece os detalhes da solicitação de exclusão, incluindo seu status atualizado. A ID da solicitação de exclusão na resposta deve corresponder à ID enviada no caminho da solicitação.

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
| `status` | O status da solicitação de exclusão. Possible values: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Uma matriz que inclui o número de registros que foram processados (`"recordsProcessed"`) e o tempo em segundos que a solicitação está sendo processada, ou o tempo que a solicitação levou para ser concluída (`"timeTakenInSec"`). |

Quando o status da solicitação de exclusão for `"COMPLETED"` você poderá confirmar que os dados foram excluídos ao tentar acessar os dados excluídos usando a API de acesso a dados. Para obter instruções sobre como usar a API de acesso a dados para acessar conjuntos de dados e lotes, consulte a documentação [de acesso a](../../data-access/home.md)dados.

## Remover uma solicitação de exclusão

[!DNL Experience Platform] permite que você exclua uma solicitação anterior, que pode ser útil por vários motivos, incluindo se o trabalho de exclusão não foi concluído ou ficou preso no estágio de processamento. Para remover uma solicitação de exclusão, é possível executar uma solicitação DELETE ao ponto de extremidade `/system/jobs` e incluir a ID da solicitação de exclusão que você deseja remover ao caminho da solicitação.

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

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. Você pode confirmar que a solicitação foi excluída executando uma solicitação GET para visualização da solicitação de exclusão por sua ID. Isso deve retornar um Status HTTP 404 (Não encontrado), indicando que a solicitação de exclusão foi removida.

## Próximas etapas

Agora que você sabe as etapas envolvidas na exclusão de conjuntos de dados e lotes do [!DNL Profile Store] dentro [!DNL Experience Platform], é possível excluir com segurança os dados que foram adicionados erroneamente ou que sua organização não precisa mais. Lembre-se de que uma solicitação de exclusão não pode ser desfeita, portanto, você deve excluir apenas os dados de que está confiante que não precisa agora e que não serão necessários no futuro.

## Apêndice {#appendix}

As informações a seguir complementam o ato de excluir um conjunto de dados do [!DNL Profile Store].

### Excluir um conjunto de dados usando a [!DNL Experience Platform] interface do usuário

Ao usar a interface do [!DNL Experience Platform] usuário para excluir um conjunto de dados para o qual foi ativado [!DNL Profile], uma caixa de diálogo é aberta perguntando: &quot;Tem certeza de que deseja excluir esse conjunto de dados do [!DNL Experience Data Lake]? Use a API &#39;p[!DNL rofile systems jobs]&#39; para excluir esse conjunto de dados do [!DNL Profile Service].&quot;

Clicar em **[!UICONTROL Excluir]** na interface do usuário desativa o conjunto de dados para ingestão, mas NÃO exclui automaticamente o conjunto de dados no backend. Para excluir permanentemente o conjunto de dados, uma solicitação de exclusão deve ser criada manualmente usando as etapas neste guia para [criar uma solicitação](#create-a-delete-request)de exclusão.

A imagem a seguir mostra o aviso ao tentar excluir um conjunto de dados [!DNL Profile]habilitado usando a interface do usuário.

![](../images/delete-profile-dataset.png)

Para obter mais informações sobre como trabalhar com conjuntos de dados, comece lendo a visão geral [dos](../../catalog/datasets/overview.md)conjuntos de dados.