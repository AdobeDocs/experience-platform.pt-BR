---
title: Endpoint da API de expiração do conjunto de dados
description: O endpoint /ttl na API da Higiene de Dados permite agendar programaticamente as expirações do conjunto de dados no Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 83149c4e6e8ea483133da4766c37886b8ebd7316
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 5%

---

# Ponto final de expiração do conjunto de dados

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Adobe Healthcare Shield.

O `/ttl` O endpoint na API da Higiene de dados permite agendar datas de expiração para os conjuntos de dados no Adobe Experience Platform.

A expiração de um conjunto de dados é apenas uma operação de exclusão com atraso de tempo. O conjunto de dados não está protegido durante o período transitório, pelo que pode ser eliminado por outros meios antes de expirar.

>[!NOTE]
>
>Embora a expiração seja especificada como um instante específico no tempo, pode haver um atraso máximo de 24 horas após a expiração antes do início da eliminação. Depois que a exclusão é iniciada, pode demorar até sete dias até que todos os rastreamentos do conjunto de dados tenham sido removidos dos sistemas da plataforma.

A qualquer momento antes de a exclusão do conjunto de dados ser realmente iniciada, você pode cancelar a expiração ou modificar o tempo de disparo. Após cancelar uma expiração de conjunto de dados, é possível reabri-la definindo uma nova expiração.

Depois que a exclusão do conjunto de dados for iniciada, seu trabalho de expiração será marcado como `executing`e não pode ser alterada. O próprio conjunto de dados pode ser recuperável por até sete dias, mas somente por meio de um processo manual iniciado por meio de uma solicitação de serviço da Adobe. Conforme a solicitação é executada, o lago de dados, o Serviço de identidade e o Perfil do cliente em tempo real começam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Depois que os dados forem excluídos de todos os três serviços, a expiração será marcada como `executed`.

>[!WARNING]
>
>Se um conjunto de dados estiver definido para expirar, você deverá alterar manualmente todos os fluxos de dados que possam estar assimilando dados nesse conjunto de dados para que seus fluxos de trabalho de downstream não sejam afetados negativamente.

## Introdução

O endpoint usado neste guia faz parte da API da Higiene de dados. Antes de continuar, reveja o [visão geral](./overview.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Listar expirações do conjunto de dados {#list}

Você pode listar todas as expirações do conjunto de dados para sua organização, fazendo uma solicitação do GET.

**Formato da API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMETERS}` | Uma lista de parâmetros de consulta opcionais, com vários parâmetros separados por `&` caracteres. Os parâmetros comuns incluem `size` e `page` para fins de paginação. Para obter uma lista completa dos parâmetros de consulta compatíveis, consulte [seção apêndice](#query-params). |

{style=&quot;table-layout:auto&quot;}

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

Uma resposta bem-sucedida lista as expirações do conjunto de dados resultantes. O exemplo a seguir foi truncado para espaço.

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
| `ttlDetails` | Contém os detalhes das expirações do conjunto de dados retornadas. Para obter mais detalhes sobre as propriedades de uma expiração de conjunto de dados, consulte a seção de resposta para fazer uma [chamada de pesquisa](#lookup). |

{style=&quot;table-layout:auto&quot;}

## Pesquisar uma expiração de conjunto de dados {#lookup}

Você pode pesquisar uma expiração de conjunto de dados por meio de uma solicitação do GET.

**Formato da API**

```http
GET /ttl/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados cuja expiração você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir consulta os detalhes de expiração do conjunto de dados `62759f2ede9e601b63a2ee14`:

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
| `expiry` | A data e a hora programadas em que o conjunto de dados será excluído. |
| `updatedAt` | Um carimbo de data e hora de quando a expiração foi atualizada pela última vez. |
| `updatedBy` | O usuário que atualizou a expiração pela última vez. |
| `displayName` | O nome de exibição da solicitação de expiração. |
| `description` | Uma descrição para a solicitação de expiração. |

{style=&quot;table-layout:auto&quot;}

### Tags de expiração do catálogo

Ao usar a variável [API do catálogo](../../catalog/api/getting-started.md) para pesquisar detalhes do conjunto de dados, se o conjunto de dados tiver uma expiração ativa, ele será listado em `tags.adobe/hygiene/ttl`.

O JSON a seguir representa uma resposta truncada para os detalhes de um conjunto de dados do Catálogo, que é um valor de expiração de `32503680000000`. O valor da tag codifica a expiração como um número inteiro de milissegundos desde o início da época Unix.

```json
{
  "63212313c308d51b997858ba": {
    "name": "TTL Test Dataset",
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

Você pode criar ou atualizar uma data de expiração para um conjunto de dados por meio de uma solicitação de PUT.

**Formato da API**

```http
PUT /ttl/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados para o qual você deseja agendar uma expiração. |

**Solicitação**

A solicitação a seguir agende um conjunto de dados `5b020a27e7040801dedbf46e` para eliminação no final de 2022 (Horário de Greenwich). Se nenhuma expiração existente for encontrada para o conjunto de dados, uma nova expiração será criada. Se o conjunto de dados já tiver uma expiração pendente, essa expiração será atualizada com o novo `expiry` valor.

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

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da expiração do conjunto de dados, com o status HTTP 200 (OK) se uma expiração pré-existente foi atualizada, ou 201 (Criado) se não houve expiração pré-existente.

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
| `expiry` | A data e a hora programadas em que o conjunto de dados será excluído. |
| `updatedAt` | Um carimbo de data e hora de quando a expiração foi atualizada pela última vez. |
| `updatedBy` | O usuário que atualizou a expiração pela última vez. |

{style=&quot;table-layout:auto&quot;}

## Cancelar uma expiração de conjunto de dados {#delete}

Você pode cancelar uma expiração de conjunto de dados fazendo uma solicitação de DELETE.

>[!NOTE]
>
>Somente as expirações do conjunto de dados que têm um status de `pending` pode ser cancelado. Tentar cancelar uma expiração que foi executada ou que já foi cancelada retorna um erro HTTP 404.

**Formato da API**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPIRATION_ID}` | O `workorderId` da expiração do conjunto de dados que você deseja cancelar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir cancela uma expiração de conjunto de dados com ID `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e o da expiração `status` está definido como `cancelled`.

## Recuperar o histórico de status de expiração de um conjunto de dados

Você pode consultar o histórico de status de expiração de um conjunto de dados específico usando o parâmetro de consulta `include=history` em uma solicitação de pesquisa. O resultado inclui informações sobre a criação da expiração do conjunto de dados, quaisquer atualizações que foram aplicadas e seu cancelamento ou execução (se aplicável).

**Formato da API**

```http
GET /ttl/{DATASET_ID}?include=history
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados cujo histórico de expiração você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

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

Uma resposta bem-sucedida retorna os detalhes da expiração do conjunto de dados, com um `history` matriz que fornece os detalhes da `status`, `expiry`, `updatedAt`e `updatedBy` atributos para cada uma das atualizações registradas.

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
| `datasetName` | O nome de exibição do conjunto de dados ao qual essa expiração se aplica. |
| `sandboxName` | O nome da sandbox em que o conjunto de dados de destino está localizado. |
| `displayName` | O nome de exibição da solicitação de expiração. |
| `description` | Uma descrição para a solicitação de expiração. |
| `imsOrg` | A ID da sua organização. |
| `history` | Lista o histórico de atualizações para a expiração como uma matriz de objetos, com cada objeto contendo a variável `status`, `expiry`, `updatedAt`e `updatedBy` para a expiração no momento da atualização. |

{style=&quot;table-layout:auto&quot;}

## Apêndice

### Parâmetros de consulta aceitos {#query-params}

A tabela a seguir descreve os parâmetros de consulta disponíveis quando [listando expirações do conjunto de dados](#list):

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `size` | Um número inteiro entre 1 e 100 que indica o número máximo de expirações a serem retornadas. O padrão é 25. | `size=50` |
| `page` | Um número inteiro que indica qual página de expirações retornar. | `page=3` |
| `orgId` | Corresponde as expirações dos conjuntos de dados cuja ID da organização corresponde à do parâmetro . Esse valor assume como padrão o da variável `x-gw-ims-org-id` cabeçalhos e são ignorados, a menos que a solicitação forneça um token de serviço. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | Uma lista de status separada por vírgulas. Quando incluída, a resposta corresponde às expirações do conjunto de dados cujo status atual está entre as listadas. | `status=pending,cancelled` |
| `author` | Corresponde a expirações cujas `created_by` é uma correspondência para a cadeia de caracteres de pesquisa. Se a string de pesquisa começar com `LIKE` ou `NOT LIKE`, o restante é tratado como um padrão de pesquisa SQL. Caso contrário, toda a cadeia de caracteres de pesquisa será tratada como uma sequência de caracteres literal que deve corresponder exatamente ao conteúdo inteiro de uma `created_by` campo. | `author=LIKE %john%` |
| `sandboxName` | Corresponde as expirações do conjunto de dados cujo nome da sandbox corresponde exatamente ao argumento . O padrão é o nome da sandbox no `x-sandbox-name` cabeçalho. Use `sandboxName=*` para incluir as expirações do conjunto de dados de todas as sandboxes. | `sandboxName=dev1` |
| `datasetId` | Corresponde as expirações que se aplicam a um conjunto de dados específico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | Corresponde as expirações que foram criadas na janela de 24 horas, começando no horário declarado.<br><br>Observe que as datas sem uma hora (como `2021-12-07`) representa a data e hora no início desse dia. Assim, `createdDate=2021-12-07` refere-se a qualquer expiração criada em 7 de dezembro de 2021, a partir de `00:00:00` through `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Corresponde as expirações que foram criadas em ou após o horário indicado. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Corresponde às expirações que foram criadas em ou antes do horário indicado. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Like `createdDate` / `createdFromDate` / `createdToDate`, mas corresponde ao tempo de atualização da expiração de um conjunto de dados em vez do tempo de criação.<br><br>Uma expiração é considerada atualizada em cada edição, incluindo quando é criada, cancelada ou executada. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Corresponde as expirações que foram canceladas a qualquer momento no intervalo indicado. Isso se aplica mesmo se a expiração tiver sido reaberta posteriormente (definindo uma nova expiração para o mesmo conjunto de dados). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Corresponde as expirações que foram concluídas durante o intervalo especificado. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Corresponde as expirações que devem ser executadas ou que já foram executadas durante o intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
