---
title: Ponto de extremidade da API de expiração do conjunto de dados
description: O ponto de extremidade /ttl na API da higiene de dados permite agendar programaticamente as expirações do conjunto de dados no Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 911089ec641d9fbb436807b04dd38e00fd47eecf
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 2%

---

# Ponto de extremidade de expiração do conjunto de dados

O ponto de extremidade `/ttl` na API da higiene de dados permite agendar datas de expiração para conjuntos de dados na Adobe Experience Platform.

A expiração de um conjunto de dados é apenas uma operação de exclusão com tempo atrasado. O conjunto de dados não está protegido enquanto isso, portanto, ele pode ser excluído por outros meios antes de atingir sua expiração.

>[!NOTE]
>
>Embora a expiração seja especificada como um instante de tempo específico, pode haver até 24 horas de atraso após a expiração antes do início da exclusão real. Depois que a exclusão é iniciada, pode levar até sete dias até que todos os rastreamentos do conjunto de dados tenham sido removidos dos sistemas da plataforma.

A qualquer momento antes da exclusão do conjunto de dados ser iniciada, você pode cancelar a expiração ou modificar a hora do acionador. Depois de cancelar uma expiração de conjunto de dados, você pode reabri-la definindo uma nova expiração.

Depois que a exclusão do conjunto de dados for iniciada, seu trabalho de expiração será marcado como `executing`, e talvez não seja alterado. O conjunto de dados em si pode ser recuperável por até sete dias, mas somente por meio de um processo manual iniciado por meio de uma solicitação de serviço da Adobe. À medida que a solicitação é executada, o data lake, o Serviço de identidade e o Perfil do cliente em tempo real iniciam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Depois que os dados forem excluídos dos três serviços, a expiração será marcada como `completed`.

>[!WARNING]
>
>Se um conjunto de dados estiver definido para expirar, você deverá alterar manualmente todos os fluxos de dados que possam estar assimilando dados nesse conjunto de dados para que seus fluxos de trabalho downstream não sejam afetados negativamente.

O Gerenciamento avançado do ciclo de vida dos dados suporta exclusões de conjuntos de dados por meio do ponto de extremidade de expiração do conjunto de dados e exclusões de ID (dados em nível de linha) usando identidades primárias por meio do [ponto de extremidade da ordem de trabalho](./workorder.md). Também é possível gerenciar [expirações do conjunto de dados](../ui/dataset-expiration.md) e [exclusões de registros](../ui/record-delete.md) por meio da interface do usuário da Platform. Consulte a documentação vinculada para obter mais informações.

>[!NOTE]
>
>O ciclo de vida dos dados não oferece suporte à exclusão em lote.

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, consulte o [Guia de API](./overview.md) para obter informações sobre cabeçalhos necessários para operações CRUD, mensagens de erro, coleções do Postman e como ler chamadas de API de exemplo.

>[!IMPORTANT]
>
>Ao fazer chamadas para a API de higiene de dados, você deve usar o cabeçalho -H `x-sandbox-name: {SANDBOX_NAME}`.

## Listar expirações do conjunto de dados {#list}

Você pode listar todas as expirações de conjunto de dados para sua organização fazendo uma solicitação GET. Parâmetros de consulta podem ser usados para filtrar a resposta para resultados apropriados.

**Formato da API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMETERS}` | Uma lista de parâmetros de consulta opcionais, com vários parâmetros separados por `&` caracteres. Parâmetros comuns incluem `limit` e `page` para fins de paginação. Para obter uma lista completa de parâmetros de consulta com suporte, consulte a [seção do apêndice](#query-params). |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida lista as expirações do conjunto de dados resultantes. O exemplo a seguir foi truncado por questões de espaço.

>[!IMPORTANT]
>
>O `ttlId` na resposta também é chamado de `{DATASET_EXPIRATION_ID}`. Ambos se referem ao identificador exclusivo para a expiração do conjunto de dados.

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Propriedade | Descrição |
| --- | --- |
| `total_count` | A contagem de expirações do conjunto de dados que corresponderam aos parâmetros da chamada de listagem. |
| `results` | Contém os detalhes das expirações do conjunto de dados retornadas. Para obter mais detalhes sobre as propriedades de uma expiração de conjunto de dados, consulte a seção de resposta para fazer uma [chamada de pesquisa](#lookup). |

{style="table-layout:auto"}

## Pesquisar uma expiração de conjunto de dados {#lookup}

Para pesquisar uma expiração de conjunto de dados, faça uma solicitação GET com `{DATASET_ID}` ou `{DATASET_EXPIRATION_ID}`.

>[!IMPORTANT]
>
>O `{DATASET_EXPIRATION_ID}` é mencionado como `ttlId` na resposta. Ambos se referem ao identificador exclusivo para a expiração do conjunto de dados.

**Formato da API**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados cuja expiração você deseja pesquisar. |
| `{DATASET_EXPIRATION_ID}` | A ID da expiração do conjunto de dados. |

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
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Propriedade | Descrição |
| --- | --- |
| `ttlId` | A ID da expiração do conjunto de dados. |
| `datasetId` | A ID do conjunto de dados ao qual essa expiração se aplica. |
| `datasetName` | O nome de exibição do conjunto de dados ao qual esta expiração se aplica. |
| `sandboxName` | O nome da sandbox em que o conjunto de dados de destino está localizado. |
| `imsOrg` | A ID da sua organização. |
| `status` | O status atual da expiração do conjunto de dados. |
| `expiry` | A data e a hora agendadas em que o conjunto de dados será excluído. |
| `updatedAt` | Um carimbo de data e hora de quando a expiração foi atualizada pela última vez. |
| `updatedBy` | O usuário que atualizou a expiração pela última vez. |
| `displayName` | O nome de exibição da solicitação de expiração. |
| `description` | Uma descrição para a solicitação de expiração. |

{style="table-layout:auto"}

### Tags de expiração de catálogo

Ao usar a [API do catálogo](../../catalog/api/getting-started.md) para pesquisar detalhes do conjunto de dados, se o conjunto de dados tiver uma expiração ativa, ele será listado em `tags.adobe/hygiene/ttl`.

O JSON a seguir representa uma resposta truncada para os detalhes de um conjunto de dados do catálogo, que tem um valor de expiração de `32503680000000`. O valor da tag codifica a expiração como um número inteiro de milissegundos desde o início da época do Unix.

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

## Criar uma expiração de conjunto de dados {#create}

Para garantir que os dados sejam removidos do sistema após um período especificado, programe uma expiração para um conjunto de dados específico fornecendo a ID do conjunto de dados e a data e hora de expiração no formato ISO 8601.

Para criar uma expiração do conjunto de dados, execute uma solicitação POST, como mostrado abaixo, e forneça os valores mencionados abaixo na carga.

>[!NOTE]
>
>Se você receber um erro 404, verifique se a solicitação não tem barras &quot;/&quot; adicionais. Uma barra à direita pode causar falha em uma solicitação POST.

**Formato da API**

```http
POST /ttl
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| Propriedade | Descrição |
| --- | --- |
| `datasetId` | **Obrigatório** A ID do conjunto de dados de destino para o qual você deseja agendar uma expiração. |
| `expiry` | **Obrigatório** Uma data e hora no formato ISO 8601. Se a cadeia de caracteres não tiver deslocamento de fuso horário explícito, o fuso horário será considerado UTC. O tempo de vida dos dados no sistema é definido de acordo com o valor de expiração fornecido.<br>Observação:<ul><li>A solicitação falhará se uma expiração de conjunto de dados já existir para o conjunto de dados.</li><li>Esta data e hora devem ser pelo menos **24 horas no futuro**.</li></ul> |
| `displayName` | Um nome de exibição opcional para a solicitação de expiração do conjunto de dados. |
| `description` | Uma descrição opcional para a solicitação de expiração. |

**Resposta**

Uma resposta bem-sucedida retorna um status HTTP 201 (Criado) e o novo estado da expiração do conjunto de dados.

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
}
```

| Propriedade | Descrição |
| --- | --- |
| `ttlId` | A ID da expiração do conjunto de dados. |
| `datasetId` | A ID do conjunto de dados ao qual essa expiração se aplica. |
| `datasetName` | O nome de exibição do conjunto de dados ao qual esta expiração se aplica. |
| `sandboxName` | O nome da sandbox em que o conjunto de dados de destino está localizado. |
| `imsOrg` | A ID da sua organização. |
| `status` | O status atual da expiração do conjunto de dados. |
| `expiry` | A data e a hora agendadas em que o conjunto de dados será excluído. |
| `updatedAt` | Um carimbo de data e hora de quando a expiração foi atualizada pela última vez. |
| `updatedBy` | O usuário que atualizou a expiração pela última vez. |
| `displayName` | Um nome de exibição para a solicitação de expiração. |
| `description` | Uma descrição para a solicitação de expiração. |

Um status HTTP 400 (Solicitação inválida) ocorre se a expiração de um conjunto de dados já existir para o conjunto de dados. Uma resposta sem sucesso retornará um status HTTP 404 (Não encontrado) se essa expiração de conjunto de dados não existir (ou se você não tiver acesso ao conjunto de dados).

## Atualizar uma expiração de conjunto de dados {#update}

Para atualizar uma data de expiração para um conjunto de dados, use uma solicitação PUT e o `ttlId`. Você pode atualizar as informações de `displayName`, `description` e/ou `expiry`.

>[!NOTE]
>
>Se você alterar a data e a hora de expiração, ela deverá ser de pelo menos 24 horas no futuro. Esse atraso imposto oferece uma oportunidade para cancelar ou reagendar a expiração e evitar qualquer perda acidental de dados.

**Formato da API**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | A ID da expiração do conjunto de dados que você deseja alterar. Observação: isso é chamado de `ttlId` na resposta. |

**Solicitação**

A solicitação a seguir reagenda a expiração de um conjunto de dados `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` para o final de 2024 (Horário de Greenwich). Se a expiração do conjunto de dados existente for encontrada, ela será atualizada com o novo valor `expiry`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `expiry` | **Obrigatório** Uma data e hora no formato ISO 8601. Se a cadeia de caracteres não tiver deslocamento de fuso horário explícito, o fuso horário será considerado UTC. O tempo de vida dos dados no sistema é definido de acordo com o valor de expiração fornecido. Qualquer carimbo de data e hora de expiração anterior do mesmo conjunto de dados deve ser substituído pelo novo valor de expiração fornecido. Esta data e hora devem ser pelo menos **24 horas no futuro**. |
| `displayName` | Um nome de exibição para a solicitação de expiração. |
| `description` | Uma descrição opcional para a solicitação de expiração. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o novo estado da expiração do conjunto de dados e um status HTTP 200 (OK) se uma expiração pré-existente tiver sido atualizada.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Propriedade | Descrição |
| --- | --- |
| `ttlId` | A ID da expiração do conjunto de dados. |
| `datasetId` | A ID do conjunto de dados ao qual essa expiração se aplica. |
| `imsOrg` | A ID da sua organização. |
| `status` | O status atual da expiração do conjunto de dados. |
| `expiry` | A data e a hora agendadas em que o conjunto de dados será excluído. |
| `updatedAt` | Um carimbo de data e hora de quando a expiração foi atualizada pela última vez. |
| `updatedBy` | O usuário que atualizou a expiração pela última vez. |

{style="table-layout:auto"}

Uma resposta sem sucesso retornará um status HTTP 404 (Não encontrado) se essa expiração de conjunto de dados não existir.

## Cancelar a expiração de um conjunto de dados {#delete}

Você pode cancelar a expiração de um conjunto de dados fazendo uma solicitação DELETE.

>[!NOTE]
>
>Somente as expirações de conjunto de dados com status `pending` podem ser canceladas. A tentativa de cancelar uma expiração que foi executada ou já foi cancelada retorna um erro HTTP 404.

**Formato da API**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{EXPIRATION_ID}` | O `ttlId` da expiração do conjunto de dados que você deseja cancelar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir cancela uma expiração do conjunto de dados com a ID `SD-b16c8b48-a15a-45c8-9215-587ea89369bf`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem Conteúdo), e o atributo `status` da expiração está definido como `cancelled`.

## Apêndice

### Parâmetros de consulta aceitos {#query-params}

A tabela a seguir descreve os parâmetros de consulta disponíveis ao [listar expirações do conjunto de dados](#list):

>[!NOTE]
>
>Os parâmetros `description`, `displayName` e `datasetName` contêm a capacidade de pesquisa por valores LIKE. Isso significa que você pode encontrar expirações agendadas do conjunto de dados chamadas: &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot; pesquisando a cadeia de caracteres &quot;Name1&quot;.

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `author` | Use o parâmetro de consulta `author` para localizar a pessoa que atualizou mais recentemente a expiração do conjunto de dados. Se nenhuma atualização tiver sido feita desde a criação, isso corresponderá ao criador original da expiração. Esse parâmetro corresponde a expirações nas quais o campo `created_by` corresponde à cadeia de caracteres de pesquisa.<br>Se a cadeia de caracteres de pesquisa começar com `LIKE` ou `NOT LIKE`, o restante será tratado como um padrão de pesquisa SQL. Caso contrário, a cadeia de caracteres de pesquisa inteira será tratada como uma cadeia literal que deve corresponder exatamente ao conteúdo inteiro de um campo `created_by`. | `author=LIKE %john%`, `author=John Q. Public` |
| `datasetId` | Corresponde às expirações que se aplicam a um conjunto de dados específico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Corresponde a expirações cujo nome do conjunto de dados contém a cadeia de caracteres de pesquisa fornecida. A correspondência não diferencia maiúsculas de minúsculas. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Corresponde a expirações cujo nome de exibição contém a cadeia de caracteres de pesquisa fornecida. A correspondência não diferencia maiúsculas de minúsculas. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtra resultados com base em uma data de execução exata, uma data de término para execução ou uma data de início para execução. Eles são usados para recuperar dados ou registros associados à execução de uma operação em uma data específica, antes de uma data específica ou depois de uma data específica. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | Corresponde às expirações que ocorreram na janela de 24 horas da data especificada. | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | Corresponde às expirações que devem ser executadas, ou já foram executadas, durante o intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Um número inteiro entre 1 e 100 que indica o número máximo de expirações a serem retornadas. O padrão é 25. | `limit=50` |
| `orderBy` | O parâmetro de consulta `orderBy` especifica a ordem de classificação dos resultados retornados pela API. Use-a para organizar os dados com base em um ou mais campos, em ordem crescente (ASC) ou decrescente (DESC). Use o prefixo + ou - para indicar ASC e DESC, respectivamente. Os seguintes valores são aceitos: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Corresponde às expirações de conjuntos de dados cuja ID da organização corresponde à do parâmetro. Esse valor é padronizado com o dos cabeçalhos `x-gw-ims-org-id` e é ignorado, a menos que a solicitação forneça um token de serviço. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Um número inteiro que indica qual página de expirações deve retornar. | `page=3` |
| `sandboxName` | Corresponde às expirações de conjunto de dados cujo nome da sandbox corresponde exatamente ao argumento. O padrão é o nome da sandbox no cabeçalho `x-sandbox-name` da solicitação. Use `sandboxName=*` para incluir expirações de conjunto de dados de todas as sandboxes. | `sandboxName=dev1` |
| `search` | Corresponde a expirações nas quais a cadeia de caracteres especificada é uma correspondência exata para a ID de expiração, ou está **contida** em qualquer um destes campos:<br><ul><li>autor</li><li>nome de exibição</li><li>descrição</li><li>nome de exibição</li><li>nome do conjunto de dados</li></ul> | `search=TESTING` |
| `status` | Uma lista de status separados por vírgulas. Quando incluída, a resposta corresponde às expirações do conjunto de dados cujo status atual está entre os listados. | `status=pending,cancelled` |
| `ttlId` | Corresponde à solicitação de expiração com a ID fornecida. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | Corresponde às expirações que foram atualizadas na janela de 24 horas da data especificada. | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | Corresponde às expirações que foram atualizadas na janela de 24 horas, a partir do horário declarado.<br><br>Uma expiração é considerada atualizada em cada edição, inclusive quando ela é criada, cancelada ou executada. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

