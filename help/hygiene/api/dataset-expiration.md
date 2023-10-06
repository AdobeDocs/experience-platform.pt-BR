---
title: Ponto de extremidade da API de expiração do conjunto de dados
description: O ponto de extremidade /ttl na API da higiene de dados permite agendar programaticamente as expirações do conjunto de dados no Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 3%

---

# Ponto de extremidade de expiração do conjunto de dados

A variável `/ttl` O endpoint na API da higiene de dados permite agendar datas de expiração para conjuntos de dados na Adobe Experience Platform.

A expiração de um conjunto de dados é apenas uma operação de exclusão com tempo atrasado. O conjunto de dados não está protegido enquanto isso, portanto, ele pode ser excluído por outros meios antes de atingir sua expiração.

>[!NOTE]
>
>Embora a expiração seja especificada como um instante de tempo específico, pode haver até 24 horas de atraso após a expiração antes do início da exclusão real. Depois que a exclusão é iniciada, pode levar até sete dias até que todos os rastreamentos do conjunto de dados tenham sido removidos dos sistemas da plataforma.

A qualquer momento antes da exclusão do conjunto de dados ser iniciada, você pode cancelar a expiração ou modificar a hora do acionador. Depois de cancelar uma expiração de conjunto de dados, você pode reabri-la definindo uma nova expiração.

Depois que a exclusão do conjunto de dados for iniciada, seu trabalho de expiração será marcado como `executing`e não poderá ser alterada. O conjunto de dados em si pode ser recuperável por até sete dias, mas somente por meio de um processo manual iniciado por meio de uma solicitação de serviço da Adobe. À medida que a solicitação é executada, o data lake, o Serviço de identidade e o Perfil do cliente em tempo real iniciam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Depois que os dados forem excluídos dos três serviços, a expiração será marcada como `executed`.

>[!WARNING]
>
>Se um conjunto de dados estiver definido para expirar, você deverá alterar manualmente todos os fluxos de dados que possam estar assimilando dados nesse conjunto de dados para que seus fluxos de trabalho downstream não sejam afetados negativamente.

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, reveja o [visão geral](./overview.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Listar expirações do conjunto de dados {#list}

Você pode listar todas as expirações de conjunto de dados para sua organização fazendo uma solicitação GET.

**Formato da API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMETERS}` | Uma lista de parâmetros de consulta opcionais, com vários parâmetros separados por `&` caracteres. Parâmetros comuns incluem `size` e `page` para paginação. Para obter uma lista completa de parâmetros de consulta suportados, consulte a [seção apêndice](#query-params). |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida lista as expirações do conjunto de dados resultantes. O exemplo a seguir foi truncado por questões de espaço.

```json
{
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `totalRecords` | A contagem de expirações do conjunto de dados que corresponderam aos parâmetros da chamada de listagem. |
| `ttlDetails` | Contém os detalhes das expirações do conjunto de dados retornadas. Para obter mais detalhes sobre as propriedades de uma expiração de conjunto de dados, consulte a seção resposta para fazer uma [chamada de pesquisa](#lookup). |

{style="table-layout:auto"}

## Pesquisar uma expiração de conjunto de dados {#lookup}

Você pode pesquisar uma expiração de conjunto de dados por meio de uma solicitação GET.

**Formato da API**

```http
GET /ttl/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados cuja expiração você deseja pesquisar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir pesquisa os detalhes de expiração do conjunto de dados `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da expiração do conjunto de dados.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | A ID da expiração do conjunto de dados. |
| `datasetId` | A ID do conjunto de dados ao qual essa expiração se aplica. |
| `imsOrg` | A ID da sua organização. |
| `status` | O status atual da expiração do conjunto de dados. |
| `expiry` | A data e a hora agendadas em que o conjunto de dados será excluído. |
| `updatedAt` | Um carimbo de data e hora de quando a expiração foi atualizada pela última vez. |
| `updatedBy` | O usuário que atualizou a expiração pela última vez. |
| `displayName` | O nome de exibição da solicitação de expiração. |
| `description` | Uma descrição para a solicitação de expiração. |

{style="table-layout:auto"}

### Tags de expiração de catálogo

Ao usar o [API do catálogo](../../catalog/api/getting-started.md) para pesquisar detalhes do conjunto de dados, se o conjunto de dados tiver uma expiração ativa, ele será listado em `tags.adobe/hygiene/ttl`.

O JSON a seguir representa uma resposta truncada para os detalhes de um conjunto de dados do catálogo, que apresenta um valor de expiração de `32503680000000`. O valor da tag codifica a expiração como um número inteiro de milissegundos desde o início da época do Unix.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## Criar ou atualizar uma expiração de conjunto de dados {#create-or-update}

Você pode criar ou atualizar uma data de expiração para um conjunto de dados por meio de uma solicitação PUT.

**Formato da API**

```http
PUT /ttl/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados para o qual você deseja agendar uma expiração. |

**Solicitação**

A solicitação a seguir agenda um conjunto de dados `5b020a27e7040801dedbf46e` para exclusão no final de 2022 (Hora Média de Greenwich). Se nenhuma expiração existente for encontrada para o conjunto de dados, uma nova expiração será criada. Se o conjunto de dados já tiver uma expiração pendente, essa expiração será atualizada com o novo `expiry` valor.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `expiry` | Um carimbo de data e hora ISO 8601 para quando o conjunto de dados será excluído. |
| `displayName` | Um nome de exibição para a solicitação de expiração. |
| `description` | Uma descrição opcional para a solicitação de expiração. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da expiração do conjunto de dados, com o status HTTP 200 (OK) se uma expiração pré-existente foi atualizada ou 201 (Criado) se não houver uma expiração pré-existente.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | A ID da expiração do conjunto de dados. |
| `datasetId` | A ID do conjunto de dados ao qual essa expiração se aplica. |
| `imsOrg` | A ID da sua organização. |
| `status` | O status atual da expiração do conjunto de dados. |
| `expiry` | A data e a hora agendadas em que o conjunto de dados será excluído. |
| `updatedAt` | Um carimbo de data e hora de quando a expiração foi atualizada pela última vez. |
| `updatedBy` | O usuário que atualizou a expiração pela última vez. |

{style="table-layout:auto"}

## Cancelar a expiração de um conjunto de dados {#delete}

Você pode cancelar a expiração de um conjunto de dados fazendo uma solicitação DELETE.

>[!NOTE]
>
>Somente as expirações de conjunto de dados com status de `pending` pode ser cancelado. A tentativa de cancelar uma expiração que foi executada ou já foi cancelada retorna um erro HTTP 404.

**Formato da API**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPIRATION_ID}` | A variável `workorderId` da expiração do conjunto de dados que você deseja cancelar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir cancela a expiração de um conjunto de dados com a ID `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo), e a expiração de `status` atributo está definido como `cancelled`.

## Recuperar o histórico do status de expiração de um conjunto de dados

Você pode consultar o histórico do status de expiração de um conjunto de dados específico usando o parâmetro de consulta `include=history` em uma solicitação de pesquisa. O resultado inclui informações sobre a criação da expiração do conjunto de dados, quaisquer atualizações que tenham sido aplicadas e seu cancelamento ou execução (se aplicável).

**Formato da API**

```http
GET /ttl/{DATASET_ID}?include=history
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados cujo histórico de expiração você deseja pesquisar. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da expiração do conjunto de dados, com uma `history` que fornece os detalhes de sua `status`, `expiry`, `updatedAt`, e `updatedBy` para cada uma de suas atualizações registradas.

```json
{
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | A ID da expiração do conjunto de dados. |
| `datasetId` | A ID do conjunto de dados ao qual essa expiração se aplica. |
| `datasetName` | O nome de exibição do conjunto de dados ao qual esta expiração se aplica. |
| `sandboxName` | O nome da sandbox em que o conjunto de dados de destino está localizado. |
| `displayName` | O nome de exibição da solicitação de expiração. |
| `description` | Uma descrição para a solicitação de expiração. |
| `imsOrg` | A ID da sua organização. |
| `history` | Lista o histórico de atualizações para a expiração como uma matriz de objetos, com cada objeto contendo a variável `status`, `expiry`, `updatedAt`, e `updatedBy` atributos para a expiração no momento da atualização. |

{style="table-layout:auto"}

## Apêndice

### Parâmetros de consulta aceitos {#query-params}

A tabela a seguir descreve os parâmetros de consulta disponíveis quando [listar expirações do conjunto de dados](#list):

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `size` | Um número inteiro entre 1 e 100 que indica o número máximo de expirações a serem retornadas. O padrão é 25. | `size=50` |
| `page` | Um número inteiro que indica qual página de expirações deve retornar. | `page=3` |
| `orgId` | Corresponde às expirações de conjuntos de dados cuja ID da organização corresponde à do parâmetro. Esse valor é padronizado como do `x-gw-ims-org-id` e é ignorada, a menos que a solicitação forneça um token de serviço. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | Uma lista de status separados por vírgulas. Quando incluída, a resposta corresponde às expirações do conjunto de dados cujo status atual está entre os listados. | `status=pending,cancelled` |
| `author` | Corresponde a expirações cujas `created_by` é uma correspondência para a string de pesquisa. Se a string de pesquisa começar com `LIKE` ou `NOT LIKE`, o restante é tratado como um padrão de pesquisa SQL. Caso contrário, a cadeia de caracteres de pesquisa inteira será tratada como uma cadeia literal que deve corresponder exatamente ao conteúdo inteiro de um `created_by` campo. | `author=LIKE %john%` |
| `sandboxName` | Corresponde às expirações de conjunto de dados cujo nome da sandbox corresponde exatamente ao argumento. O padrão é o nome da sandbox no da solicitação `x-sandbox-name` cabeçalho. Uso `sandboxName=*` para incluir expirações de conjunto de dados de todas as sandboxes. | `sandboxName=dev1` |
| `datasetId` | Corresponde às expirações que se aplicam a um conjunto de dados específico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | Corresponde às expirações que foram criadas na janela de 24 horas, começando no horário declarado.<br><br>Observe que as datas sem um horário (como `2021-12-07`) representam a data e hora no início desse dia. Assim, `createdDate=2021-12-07` refere-se a qualquer expiração criada em 7 de dezembro de 2021, `00:00:00` até `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Corresponde às expirações criadas no horário indicado ou depois dele. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Corresponde às expirações criadas no horário indicado ou antes dele. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Curtir `createdDate` / `createdFromDate` / `createdToDate`, mas corresponde a uma hora de atualização de expiração de conjunto de dados, em vez da hora de criação.<br><br>Uma expiração é considerada atualizada em cada edição, incluindo quando é criada, cancelada ou executada. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Corresponde às expirações que foram canceladas a qualquer momento no intervalo indicado. Isso se aplica mesmo que a expiração tenha sido reaberta posteriormente (definindo uma nova expiração para o mesmo conjunto de dados). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Corresponde às expirações concluídas durante o intervalo especificado. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Corresponde às expirações que devem ser executadas, ou já foram executadas, durante o intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style="table-layout:auto"}
