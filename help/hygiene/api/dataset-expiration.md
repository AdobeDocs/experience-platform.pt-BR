---
title: Ponto de extremidade da API de expiração do conjunto de dados
description: O ponto de extremidade /ttl na API da higiene de dados permite agendar programaticamente as expirações do conjunto de dados no Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 2%

---

# Ponto de extremidade de expiração do conjunto de dados

Use o ponto de extremidade `/ttl` na API de higiene de dados para agendar quando os conjuntos de dados na Adobe Experience Platform devem ser excluídos.

A expiração de um conjunto de dados é uma operação de exclusão atrasada. O conjunto de dados não é protegido enquanto isso e pode ser excluído por outros meios antes da expiração programada.

>[!NOTE]
>
>Embora a expiração seja especificada como um instante de tempo específico, pode haver até 24 horas de atraso após a expiração antes do início da exclusão real. Depois que a exclusão é iniciada, pode levar até sete dias para que todos os rastreamentos do conjunto de dados sejam removidos dos sistemas do Experience Platform.

Antes de começar a exclusão, você pode cancelar a expiração ou alterar o horário agendado. Para reabrir uma expiração cancelada, defina uma nova expiração.

Depois que a exclusão começar, o trabalho de expiração será marcado como `executing` e não poderá mais ser modificado. O conjunto de dados pode ser recuperado por até sete dias, mas somente por meio de uma solicitação de serviço manual da Adobe. Durante a exclusão, o data lake, o Serviço de identidade e o Perfil do cliente em tempo real removem separadamente o conteúdo do conjunto de dados. Quando a exclusão for concluída, a expiração será marcada como `completed`.

>[!WARNING]
>
>Se um conjunto de dados estiver definido para expirar, você deverá alterar manualmente todos os fluxos de dados que possam estar assimilando dados nesse conjunto de dados para que seus fluxos de trabalho downstream não sejam afetados negativamente.

O Gerenciamento avançado do ciclo de vida dos dados suporta exclusões de conjuntos de dados por meio do ponto de extremidade de expiração do conjunto de dados e exclusões de ID (dados em nível de linha) usando identidades primárias por meio do [ponto de extremidade da ordem de trabalho](./workorder.md). Também é possível gerenciar [expirações do conjunto de dados](../ui/dataset-expiration.md) e [exclusões de registros](../ui/record-delete.md) por meio da interface do usuário do Experience Platform. Consulte a documentação vinculada para obter mais informações.

>[!NOTE]
>
>O ciclo de vida dos dados não oferece suporte à exclusão em lote.

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, consulte o [Guia de API](./overview.md) para obter informações sobre cabeçalhos necessários para operações CRUD, mensagens de erro, coleções do Postman e como ler chamadas de API de exemplo.

>[!IMPORTANT]
>
>Ao fazer chamadas para a API de higiene de dados, você deve usar o cabeçalho -H `x-sandbox-name: {SANDBOX_NAME}`.

## Listar expirações do conjunto de dados {#list}

Você pode listar todas as expirações de conjunto de dados configuradas para sua organização fazendo uma solicitação GET para o ponto de extremidade `/ttl`.

Filtrar resultados usando parâmetros de consulta para retornar somente as expirações que atendem aos seus critérios. Cada resultado inclui detalhes de status e configuração para cada expiração do conjunto de dados.

**Formato da API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMETERS}` | Uma lista de parâmetros de consulta opcionais, com vários parâmetros separados por `&` caracteres. Parâmetros comuns incluem `limit` e `page` para fins de paginação. Para obter uma lista completa de parâmetros de consulta com suporte, consulte a [seção do apêndice](#query-params) uma lista completa de parâmetros de consulta com suporte. Os parâmetros mais usados estão incluídos abaixo e no apêndice. |
| `author` | Filtre pelo usuário que atualizou ou criou a expiração do conjunto de dados mais recentemente. Suporta padrões semelhantes a SQL (por exemplo, `LIKE %john%`). |
| `datasetId` | Filtrar expirações por uma ID de conjunto de dados específica. |
| `datasetName` | Um filtro que não diferencia maiúsculas de minúsculas para nomes de conjuntos de dados corresponde a. |
| `status` | Filtre por uma lista separada por vírgulas com os status: `pending`, `executing`, `cancelled`, `completed`. |
| `expiryDate` | Filtre por expirações com uma data de expiração específica. |
| `limit` | Estipule o número máximo de resultados a serem retornados (1-100, padrão: 25). |
| `page` | Paginar resultados com um índice baseado em zero (tamanho de página padrão: 50, máx.: 100). |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera todas as expirações do conjunto de dados atualizadas antes de 1º de agosto de 2021 e atualizadas pela última vez por um usuário cujo nome corresponda a &quot;Jane Doe&quot;.

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
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Propriedade | Descrição |
| --- | --- |
| `results` | Uma matriz de configurações de expiração do conjunto de dados. |
| `ttlId` | O identificador exclusivo da configuração de expiração do conjunto de dados. |
| `datasetId` | O identificador exclusivo do conjunto de dados associado a essa configuração. |
| `datasetName` | O nome do conjunto de dados. |
| `sandboxName` | A sandbox em que essa expiração do conjunto de dados é configurada. |
| `displayName` | Um nome legível para a configuração de expiração. |
| `description` | Uma descrição da configuração de expiração. |
| `imsOrg` | O identificador exclusivo da organização. |
| `status` | O status atual da expiração. Um de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | A data e a hora de expiração programadas (formato ISO 8601). |
| `updatedAt` | O carimbo de data e hora da última atualização dessa configuração. |
| `updatedBy` | O identificador e o email do usuário ou serviço que atualizou a configuração pela última vez. |
| `current_page` | O índice da página de resultados atual (baseado em zero). |
| `total_pages` | O número total de páginas de resultados disponíveis. |
| `total_count` | O número total de registros de configuração de expiração do conjunto de dados retornados. |

{style="table-layout:auto"}

## Pesquisar uma expiração de conjunto de dados {#lookup}

Recupere os detalhes de uma configuração específica de expiração do conjunto de dados fazendo uma solicitação do GET com a ID de expiração do conjunto de dados ou a ID do conjunto de dados como o parâmetro de caminho.

>[!IMPORTANT]
>
>Você pode fornecer uma ID de expiração do conjunto de dados (por exemplo, `SD-xxxxxx-xxxx`) ou uma ID de conjunto de dados no caminho. O `ttlId` na resposta é o identificador exclusivo para a expiração do conjunto de dados.

**Formato da API**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| Parâmetro | Descrição |
| --- | --- |
| `{ID}` | O identificador exclusivo da configuração de expiração do conjunto de dados. Você pode fornecer uma ID de expiração do conjunto de dados ou uma ID do conjunto de dados. |
| `include` | (Opcional) Se definido como `history`, a resposta inclui uma matriz `history` com eventos de alteração para a configuração. |

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
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| Propriedade | Descrição |
| --- | --- |
| `ttlId` | O identificador exclusivo da configuração de expiração do conjunto de dados. |
| `datasetId` | O identificador exclusivo do conjunto de dados. |
| `datasetName` | O nome do conjunto de dados. |
| `sandboxName` | A sandbox na qual a expiração do conjunto de dados é configurada. |
| `displayName` | Um nome legível para a configuração de expiração do conjunto de dados. |
| `description` | Uma descrição da configuração de expiração do conjunto de dados. |
| `imsOrg` | O identificador exclusivo da organização associado a essa configuração. |
| `status` | O status atual da configuração de expiração do conjunto de dados.<br>Um de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | O carimbo de data e hora de expiração agendado para o conjunto de dados (formato ISO 8601). |
| `updatedAt` | Carimbo de data e hora da atualização mais recente. |
| `updatedBy` | O identificador e o email do usuário ou serviço que atualizou a expiração do conjunto de dados pela última vez. |

{style="table-layout:auto"}

### Tags de expiração de catálogo

Ao usar a [API do catálogo](../../catalog/api/getting-started.md) para pesquisar detalhes do conjunto de dados, se o conjunto de dados tiver uma expiração ativa, ele será listado em `tags.adobe/hygiene/ttl`.

O JSON a seguir mostra uma resposta de API de catálogo truncada para um conjunto de dados com um valor de expiração de `32503680000000`. A tag codifica a expiração como o número de milissegundos desde a época do Unix.

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

Crie uma nova configuração de expiração do conjunto de dados para definir quando um conjunto de dados expirará e estará qualificado para exclusão.\
Forneça a ID do conjunto de dados, a data de expiração ou a data-hora (no formato ISO 8601), um nome de exibição e (opcionalmente) uma descrição.

>[!NOTE]
>
>O valor de expiração pode ser uma data (AAAA-MM-DD) ou uma data e hora (AAAA-MM-DDTHH:MM:SSZ). Se você fornecer apenas uma data, o sistema usará a meia-noite UTC (00:00:00Z) nesse dia. A expiração deve ser de pelo menos 24 horas no futuro.

Para criar uma expiração do conjunto de dados, envie uma solicitação POST, como mostrado abaixo.

>[!TIP]
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
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `datasetId` | **Obrigatório.** O identificador exclusivo do conjunto de dados para aplicar a expiração. |
| `expiry` | **Obrigatório.** A data e hora de expiração no formato ISO 8601. Isso define a duração dos dados no sistema. Se apenas uma data for fornecida, o padrão será meia-noite UTC (00:00:00Z). A expiração **deve ser de pelo menos 24 horas no futuro**. <br>**NOTA**:<ul><li>A solicitação falhará se uma expiração de conjunto de dados já existir para o conjunto de dados.</li></ul> |
| `displayName` | **Obrigatório.** Um nome legível para a configuração de expiração do conjunto de dados. |
| `description` | Uma descrição opcional para a configuração de expiração do conjunto de dados. |

**Resposta**

Uma resposta bem-sucedida retorna um status HTTP 201 (Criado) e a nova configuração de expiração do conjunto de dados.

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Propriedade | Descrição |
| --- | --- |
| `ttlId` | O identificador exclusivo da configuração de expiração do conjunto de dados criado. |
| `datasetId` | O identificador exclusivo do conjunto de dados. |
| `datasetName` | O nome do conjunto de dados. |
| `sandboxName` | A sandbox em que essa expiração do conjunto de dados é configurada. |
| `displayName` | O nome de exibição da configuração de expiração do conjunto de dados. |
| `description` | Uma descrição da configuração de expiração do conjunto de dados. |
| `imsOrg` | O identificador exclusivo da organização associado a essa configuração. |
| `status` | O status atual da configuração de expiração do conjunto de dados.<br>Um de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | O carimbo de data e hora de expiração agendado para o conjunto de dados. |
| `updatedAt` | O carimbo de data/hora da atualização mais recente. |
| `updatedBy` | O identificador e o email do usuário ou serviço que atualizou a configuração de expiração do conjunto de dados pela última vez. |

Um status HTTP 400 (Solicitação inválida) ocorre se a expiração de um conjunto de dados já existir para o conjunto de dados. Um status HTTP 404 (Não encontrado) ocorre se esse conjunto de dados não existir ou se você não tiver acesso ao conjunto de dados.

## Atualizar uma configuração de expiração do conjunto de dados {#update}

Para atualizar uma configuração de expiração de conjunto de dados existente, faça uma solicitação PUT para `/ttl/DATASET_EXPIRATION_ID`. Você só pode atualizar os campos `displayName`, `description` e `expiry` da configuração. Atualizações só são permitidas quando o status de expiração é `pending`.

>[!NOTE]
>
>O campo `expiry` aceita uma data (AAAA-MM-DD) ou data e hora (AAAA-MM-DDTHH:MM:SSZ). Se apenas uma data for fornecida, o sistema usará a meia-noite UTC (00:00:00Z) nesse dia. A expiração **deve ser de pelo menos 24 horas no futuro**.

**Formato da API**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | O identificador exclusivo da configuração de expiração do conjunto de dados. **OBSERVAÇÃO**: isso é chamado de `ttlId` na resposta. |

**Solicitação**

A solicitação a seguir atualiza a expiração, o nome de exibição e a descrição da expiração do conjunto de dados `SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45`:

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `displayName` | (Opcional) Um novo nome legível para a configuração de expiração do conjunto de dados. |
| `description` | (Opcional) Uma nova descrição para a configuração de expiração do conjunto de dados. |
| `expiry` | (Opcional) Uma nova data de expiração ou data e hora no formato ISO 8601. Se apenas uma data for fornecida, o padrão será meia-noite UTC. A expiração deve ser **pelo menos 24 horas no futuro**. |

>[!NOTE]
>
>Pelo menos um desses campos deve ser fornecido na solicitação.

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e a configuração de expiração do conjunto de dados atualizada.

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Propriedade | Descrição |
| --- | --- |
| `ttlId` | O identificador exclusivo da configuração de expiração atualizada do conjunto de dados. |
| `datasetId` | O identificador exclusivo do conjunto de dados. |
| `datasetName` | O nome do conjunto de dados. |
| `sandboxName` | A sandbox em que essa expiração do conjunto de dados é configurada. |
| `displayName` | O nome de exibição da configuração de expiração do conjunto de dados. |
| `description` | Uma descrição da configuração de expiração do conjunto de dados. |
| `imsOrg` | A ID da organização associada a essa configuração. |
| `status` | O status atual da configuração de expiração do conjunto de dados.<br>Um de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | O carimbo de data e hora de expiração agendado para o conjunto de dados. |
| `updatedAt` | O carimbo de data/hora da atualização mais recente. |
| `updatedBy` | O identificador e o email do usuário ou serviço que atualizou a configuração de expiração do conjunto de dados pela última vez. |

{style="table-layout:auto"}

Uma resposta sem sucesso retornará um status HTTP 404 (Não encontrado) se essa expiração de conjunto de dados não existir.

## Cancelar a expiração de um conjunto de dados {#delete}

Cancele uma configuração de expiração pendente do conjunto de dados fazendo uma solicitação DELETE para `/ttl/{ID}`.

>[!NOTE]
>
>Somente as expirações do conjunto de dados no status `pending` podem ser canceladas. A tentativa de cancelar uma expiração que já é `executing`, `completed` ou `cancelled` retorna HTTP 400 (Solicitação inválida).

**Formato da API**

```http
DELETE /ttl/{ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ID}` | O identificador exclusivo da configuração de expiração do conjunto de dados. Você pode fornecer uma ID de expiração do conjunto de dados ou uma ID do conjunto de dados. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir cancela uma expiração do conjunto de dados com a ID `SD-d4a7d918-283b-41fd-bfe1-4e730a613d21`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) e a configuração de expiração do conjunto de dados cancelado. Observe que o atributo `status` da expiração está definido como `cancelled`.

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| Propriedade | Descrição |
|---|---|
| `ttlId` | O identificador exclusivo da configuração de expiração do conjunto de dados excluído. |
| `datasetId` | O identificador exclusivo do conjunto de dados. |
| `datasetName` | O nome do conjunto de dados. |
| `sandboxName` | A sandbox em que essa expiração do conjunto de dados é configurada. |
| `displayName` | O nome de exibição da configuração de expiração do conjunto de dados. |
| `description` | Uma descrição da configuração de expiração do conjunto de dados. |
| `imsOrg` | O identificador exclusivo da organização associado a essa configuração. |
| `status` | O status atual da configuração de expiração do conjunto de dados.<br>Um de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | O carimbo de data e hora de expiração agendado para o conjunto de dados. |
| `updatedAt` | O carimbo de data/hora da atualização mais recente. |
| `updatedBy` | O identificador e o email do usuário ou serviço que atualizou a configuração de expiração do conjunto de dados pela última vez. |

**Exemplo de resposta 400 (Solicitação inválida)**

Erro 400 ao tentar cancelar um conjunto de dados com uma configuração de expiração de `executing`, `completed` ou `cancelled`.

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>Erro 404 ao tentar cancelar uma expiração de conjunto de dados que já é `completed` ou `cancelled`.

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

