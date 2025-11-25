---
title: Registrar Ordens de Serviço de Exclusão
description: Saiba como usar o ponto de extremidade /workorder na API de higiene de dados para gerenciar ordens de trabalho de exclusão de registro no Adobe Experience Platform. Este guia aborda cotas, linhas do tempo de processamento e uso da API.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: f1f37439bd4d77faf1015741e604eee7188c58d7
workflow-type: tm+mt
source-wordcount: '2440'
ht-degree: 2%

---

# Registrar ordens de serviço de exclusão {#work-order-endpoint}

Use o ponto de extremidade `/workorder` na API de higiene de dados para criar, exibir e gerenciar ordens de trabalho de exclusão de registro no Adobe Experience Platform. As ordens de trabalho permitem controlar, monitorar e rastrear a remoção de dados entre conjuntos de dados para ajudar você a manter a qualidade dos dados e dar suporte aos padrões de governança de dados de sua organização.

>[!IMPORTANT]
>
>As ordens de serviço de exclusão de registro são para limpeza de dados, remoção de dados anônimos ou minimização de dados. **Não use ordens de trabalho de exclusão de registro para solicitações de direitos do titular dos dados sob regulamentos de privacidade como o GDPR.** Para casos de uso de conformidade, use o [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Introdução

Antes de começar, consulte a [visão geral](./overview.md) para saber mais sobre os cabeçalhos necessários, como ler exemplos de chamadas de API e onde encontrar a documentação relacionada.

## Cotas e cronogramas de processamento {#quotas}

As ordens de serviço de exclusão de registro estão sujeitas a limites diários e mensais de envio de identificador, determinados pelo direito de licença da organização. Esses limites se aplicam às solicitações de exclusão de registros com base na interface do usuário e na API.

>[!NOTE]
>
>Você pode enviar até **1.000.000 identificadores por dia**, mas somente se sua cota mensal restante permitir. Se o limite mensal for inferior a 1 milhão, os envios diários não poderão exceder esse limite.

### Direito de envio mensal por produto {#quota-limits}

A tabela a seguir mostra os limites de envio de identificador por produto e nível de direito. Para cada produto, o limite mensal é o menor de dois valores: um limite de identificador fixo ou um limite baseado em porcentagem vinculado ao volume de dados licenciado.

| Produto | Descrição do Direito | Limite mensal (o que for menor) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP ou Adobe Journey Optimizer | Sem o Privacy and Security Shield ou o complemento Healthcare Shield | 2.000.000 identificadores ou 5% do público endereçável |
| Real-Time CDP ou Adobe Journey Optimizer | Com o Privacy and Security Shield ou o complemento Healthcare Shield | 15.000.000 identificadores ou 10% do público endereçável |
| Customer Journey Analytics | Sem o Privacy and Security Shield ou o complemento Healthcare Shield | 2.000.000 identificadores ou 100 identificadores por milhão de linhas de direito do CJA |
| Customer Journey Analytics | Com o Privacy and Security Shield ou o complemento Healthcare Shield | 15.000.000 identificadores ou 200 identificadores por milhão de linhas de direito do CJA |

>[!NOTE]
>
>A maioria das organizações terá limites mensais mais baixos com base no público-alvo endereçável real ou nos direitos de linha do CJA.

>[!NOTE]
>
>As cotas são redefinidas no primeiro dia de cada mês. Cota não utilizada **não** é transferida.

>[!NOTE]
>
>O uso da cota é baseado no direito mensal licenciado de sua organização para **identificadores enviados**. As cotas não são aplicadas por medidas de proteção do sistema, mas podem ser monitoradas e revisadas.\
>A capacidade da ordem de trabalho de exclusão do registro é um **serviço compartilhado**. Seu limite mensal reflete os direitos mais altos no Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics e em qualquer complemento do Shield aplicável.

### Processamento de cronogramas para envios de identificadores {#sla-processing-timelines}

Após a submissão, as ordens de serviço de deleção de registro são enfileiradas e processadas com base no seu nível de direito.

| Descrição do produto e dos direitos | Duração da Fila | Tempo máximo de processamento (SLA) |
|------------------------------------|---------------------|-------------------------------|
| Sem o Privacy and Security Shield ou o complemento Healthcare Shield | Até 15 dias | 30 dias |
| Com o Privacy and Security Shield ou o complemento Healthcare Shield | Normalmente, 24 horas | 15 dias |

Se sua organização exigir limites mais altos, entre em contato com o representante da Adobe para obter uma revisão de direito.

>[!TIP]
>
>Para verificar seu nível atual de uso de cota ou direito, consulte o [Guia de referência de cota](../api/quota.md).

## Listar ordens de trabalho de exclusão de registro {#list}

Recupere uma lista paginada de ordens de serviço de exclusão de registro para operações de higiene de dados em sua organização. Filtrar resultados usando parâmetros de consulta. Cada registro de ordem de trabalho inclui o tipo de ação (como `identity-delete`), o status, o conjunto de dados relacionado, os detalhes do usuário e os metadados de auditoria.

**Formato da API**

```http
GET /workorder
```

A tabela a seguir descreve os parâmetros de consulta disponíveis para listar ordens de serviço de deleção de registro.

| Parâmetro da consulta | Descrição |
| --------------- | ------------|
| `search` | Correspondência parcial que não diferencia maiúsculas de minúsculas (pesquisa curinga) entre campos: author, displayName, description ou datasetName. Também corresponde à ID de expiração exata. |
| `type` | Filtrar resultados por tipo de ordem de trabalho (por exemplo, `identity-delete`). |
| `status` | Lista separada por vírgulas de status de ordens de serviço. Os valores de status diferenciam maiúsculas de minúsculas.<br>Enumeração: `received`, `validated`, `submitted`, `ingested`, `completed`, `failed` |
| `author` | Localize a pessoa que atualizou a ordem de serviço (ou o criador original) mais recentemente. Aceita literal ou padrão SQL. |
| `displayName` | Correspondência que não diferencia maiúsculas de minúsculas para o nome de exibição da ordem de serviço. |
| `description` | Correspondência que não diferencia maiúsculas de minúsculas para descrição de ordem de serviço. |
| `workorderId` | Correspondência exata da ID da ordem de serviço. |
| `sandboxName` | Correspondência exata do nome da sandbox usado na solicitação, ou use `*` para incluir todas as sandboxes. |
| `fromDate` | Filtrar por ordens de trabalho criadas nessa data ou depois dela. Exige que `toDate` seja definido. |
| `toDate` | Filtrar por ordens de trabalho criadas nessa data ou antes dela. Exige que `fromDate` seja definido. |
| `filterDate` | Retorna apenas as ordens de serviço criadas, atualizadas ou com status alterado nessa data. |
| `page` | Índice de página a ser retornado (começa em 0). |
| `limit` | Máximo de resultados por página (1-100, padrão: 25). |
| `orderBy` | Ordem de classificação dos resultados. Use o prefixo `+` ou `-` para crescente/decrescente. Exemplo: `orderBy=-datasetName`. |
| `properties` | Lista separada por vírgulas de campos adicionais a serem incluídos por resultado. Opcional. |


**Solicitação**

A solicitação a seguir recupera todas as ordens de serviço de deleção de registro concluídas, limitadas a duas por página:

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista paginada de ordens de serviço de deleção de registro.

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

A tabela a seguir descreve as propriedades na resposta.

| Propriedade | Descrição |
| --- | --- |
| `results` | Matriz de objetos de ordem de trabalho de exclusão de registro. Cada objeto contém os campos abaixo. |
| `workorderId` | O identificador exclusivo da ordem de serviço de exclusão do registro. |
| `orgId` | O identificador exclusivo da organização. |
| `bundleId` | O identificador exclusivo do conjunto que contém esta ordem de serviço de exclusão de registro. O agrupamento permite que várias ordens de exclusão sejam agrupadas e processadas juntas pelos serviços downstream. |
| `action` | O tipo de ação solicitado na ordem de serviço. |
| `createdAt` | O carimbo de data e hora quando a ordem de trabalho foi criada. |
| `updatedAt` | O carimbo de data e hora quando a ordem de trabalho foi atualizada pela última vez. |
| `operationCount` | O número de operações incluídas na ordem de serviço. |
| `targetServices` | Lista de serviços de destino da ordem de serviço. |
| `status` | Status atual da ordem de serviço. Os valores possíveis são: `received`,`validated`, `submitted`, `ingested`, `completed` e `failed`. |
| `createdBy` | O email e o identificador do usuário que criou a ordem de trabalho. |
| `datasetId` | O identificador exclusivo do conjunto de dados associado à ordem de serviço. Se a solicitação se aplicar a todos os conjuntos de dados, esse campo será definido como TODOS. |
| `datasetName` | O nome do conjunto de dados associado à ordem de serviço. |
| `displayName` | Um rótulo legível para a ordem de serviço. |
| `description` | Uma descrição da finalidade da ordem de serviço. |
| `total` | Número total de ordens de trabalho de exclusão de registro correspondentes à consulta. |
| `count` | Número de ordens de trabalho de exclusão de registro na página atual. |
| `_links` | Links de paginação e navegação. |
| `next` | Objeto com `href` (cadeia de caracteres) e `templated` (booleano) para a próxima página. |
| `page` | Objeto com `href` (cadeia de caracteres) e `templated` (booleano) para navegação de página. |

{style="table-layout:auto"}

## Criar uma ordem de serviço de exclusão de registro {#create}

Para excluir registros associados a uma ou mais identidades de um único conjunto de dados ou de todos os conjuntos de dados, faça uma solicitação POST para o ponto de extremidade `/workorder`.

As ordens de serviço são processadas de forma assíncrona e são exibidas na lista de ordens de serviço após o envio.

>[!TIP]
>
>Cada ordem de serviço de exclusão de registro enviada por meio da API pode incluir até **100.000 identidades**. Envie o máximo de identidades por solicitação possível para maximizar a eficiência. Evite envios de baixo volume, como ordens de trabalho de ID única.

**Formato da API**

```http
POST /workorder
```

>[!NOTE]
>
>Você só pode excluir registros de conjuntos de dados cujo esquema XDM associado defina uma identidade principal ou mapa de identidade.

>[!NOTE]
>
>Se você tentar criar uma ordem de serviço de exclusão de registro para um conjunto de dados que já tem uma expiração ativa, a solicitação retornará HTTP 400 (Solicitação inválida). Uma expiração ativa é qualquer exclusão programada que ainda não foi concluída.

**Solicitação**

A solicitação a seguir exclui todos os registros associados a endereços de email especificados de um conjunto de dados específico.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

A tabela a seguir descreve as propriedades para criar uma ordem de serviço de deleção de registro.

| Propriedade | Descrição |
| --- | --- |
| `displayName` | Um rótulo legível por humanos para esta ordem de serviço de exclusão de registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |
| `action` | A ação solicitada para a ordem de trabalho de exclusão do registro. Para excluir registros associados a uma determinada identidade, use `delete_identity`. |
| `datasetId` | O identificador exclusivo do conjunto de dados. Use a ID do conjunto de dados para um conjunto de dados específico, ou `ALL` para direcionar todos os conjuntos de dados. Os conjuntos de dados devem ter uma identidade primária ou mapa de identidade. Se existir um mapa de identidade, ele estará presente como um campo de nível superior chamado `identityMap`.<br>Observe que uma linha de conjunto de dados pode ter muitas identidades em seu mapa de identidade, mas apenas uma pode ser marcada como primária. `"primary": true` deve ser incluído para forçar `id` a corresponder a uma identidade principal. |
| `namespacesIdentities` | Uma matriz de objetos, cada um contendo:<br><ul><li> `namespace`: um objeto com uma propriedade `code` especificando o namespace de identidade (por exemplo, &quot;email&quot;).</li><li> `IDs`: Uma matriz de valores de identidade a serem excluídos para este namespace.</li></ul>Os namespaces de identidade fornecem contexto para dados de identidade. Você pode usar os namespaces padrão fornecidos pelo Experience Platform ou criar os seus próprios. Para saber mais, consulte a [documentação de namespace de identidade](../../identity-service/features/namespaces.md) e a [especificação da API do Serviço de Identidade](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da nova ordem de serviço de exclusão de registro.

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

A tabela a seguir descreve as propriedades na resposta.

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | O identificador exclusivo da ordem de serviço de exclusão do registro. Use esse valor para pesquisar o status ou os detalhes da exclusão. |
| `orgId` | O identificador exclusivo da organização. |
| `bundleId` | O identificador exclusivo do conjunto que contém esta ordem de serviço de exclusão de registro. O agrupamento permite que várias ordens de exclusão sejam agrupadas e processadas juntas pelos serviços downstream. |
| `action` | O tipo de ação solicitado na ordem de trabalho de exclusão do registro. |
| `createdAt` | O carimbo de data e hora quando a ordem de trabalho foi criada. |
| `updatedAt` | O carimbo de data e hora quando a ordem de trabalho foi atualizada pela última vez. |
| `operationCount` | O número de operações incluídas na ordem de serviço. |
| `targetServices` | Uma lista de serviços de destino para a ordem de serviço de exclusão de registro. |
| `status` | Status atual da ordem de serviço de exclusão do registro. |
| `createdBy` | O email e o identificador do usuário que criou a ordem de trabalho de exclusão de registro. |
| `datasetId` | O identificador exclusivo do conjunto de dados. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |
| `datasetName` | O nome do conjunto de dados para esta ordem de serviço de exclusão de registro. |
| `displayName` | Um rótulo legível para a ordem de serviço de exclusão do registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |

{style="table-layout:auto"}

>[!NOTE]
>
>A propriedade de ação para ordens de trabalho de exclusão de registro está atualmente `identity-delete` nas respostas da API. Se a API mudar para usar um valor diferente (como `delete_identity`), esta documentação será atualizada adequadamente.

## Converter listas de ID em JSON para solicitações de exclusão de registro

Para criar uma ordem de trabalho de exclusão de registro a partir de arquivos CSV, TSV ou TXT contendo identificadores, você pode usar scripts de conversão para produzir as cargas JSON necessárias para o ponto de extremidade `/workorder`. Essa abordagem é especialmente útil ao trabalhar com arquivos de dados existentes. Para scripts prontos para uso e instruções abrangentes, visite o [repositório GitHub de csv para higiene de dados](https://github.com/perlmonger42/csv-to-data-hygiene).

### Gerar cargas JSON

Os exemplos de script bash a seguir demonstram como executar os scripts de conversão no Python ou Ruby:

>[!BEGINTABS]

>[!TAB Exemplo para executar o script Python]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.py sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!TAB Exemplo para executar o script Ruby]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.rb sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!ENDTABS]

A tabela abaixo descreve os parâmetros nos scripts bash.

| Parâmetro | Descrição |
| ---           | ---     |
| `verbose` | Ativar saída detalhada. |
| `column` | O índice (com base em 1) ou o nome do cabeçalho da coluna que contém os valores de identidade a serem excluídos. O padrão é a primeira coluna, se não especificada. |
| `namespace` | Um objeto com uma propriedade `code` especificando o namespace de identidade (por exemplo, &quot;email&quot;). |
| `dataset-id` | O identificador exclusivo do conjunto de dados associado à ordem de serviço. Se a solicitação se aplicar a todos os conjuntos de dados, este campo será definido como `ALL`. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |
| `output-dir` | O diretório no qual gravar a carga JSON de saída. |

{style="table-layout:auto"}

O exemplo abaixo mostra uma carga JSON bem-sucedida convertida de um arquivo CSV, TSV ou TXT. Ele contém registros associados ao namespace especificado e é usado para excluir registros identificados por endereços de email.

```json
{
  "action": "delete_identity",
  "datasetId": "66f4161cc19b0f2aef3edf10",
  "displayName": "output/sample-big-001.json",
  "description": "a simple sample",
  "identities": [
    {
      "namespace": {
        "code": "email"
      },
      "id": "1"
    },
    {
      "namespace": {
        "code": "email"
      },
      "id": "2"
    }
  ]
}
```

A tabela a seguir descreve as propriedades na carga JSON.

| Propriedade | Descrição |
| ---          | ---     |
| `action` | A ação solicitada para a ordem de trabalho de exclusão do registro. Automaticamente definido como `delete_identity` pelo script de conversão. |
| `datasetId` | O identificador exclusivo do conjunto de dados. |
| `displayName` | Um rótulo legível por humanos para esta ordem de serviço de exclusão de registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |
| `identities` | Uma matriz de objetos, cada um contendo:<br><ul><li> `namespace`: um objeto com uma propriedade `code` especificando o namespace de identidade (por exemplo, &quot;email&quot;).</li><li> `id`: O valor de identidade a ser excluído para este namespace.</li></ul> |

{style="table-layout:auto"}

### Enviar os dados JSON gerados para o ponto de extremidade `/workorder`

Para enviar uma solicitação, siga as instruções na seção [criar uma ordem de serviço de exclusão de registro](#create). Use a carga JSON convertida como o corpo da solicitação (`-d`) ao enviar sua solicitação POST `curl` para o ponto de extremidade de API `/workorder`.

## Recuperar detalhes de uma ordem de trabalho de exclusão de registro específica {#lookup}

Recupere informações para uma ordem de trabalho de exclusão de registro específica fazendo uma solicitação GET para `/workorder/{WORKORDER_ID}`. A resposta inclui tipo de ação, status, conjunto de dados associado, informações do usuário e metadados de auditoria.

**Formato da API**

```http
GET /workorder/{WORKORDER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | O identificador exclusivo da ordem de serviço de exclusão de registro que você está pesquisando. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da ordem de serviço de exclusão de registro especificada.

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

A tabela a seguir descreve as propriedades na resposta.

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | O identificador exclusivo da ordem de serviço de exclusão do registro. |
| `orgId` | O identificador exclusivo da sua organização. |
| `bundleId` | O identificador exclusivo do conjunto que contém esta ordem de serviço de exclusão de registro. O agrupamento permite que várias ordens de exclusão sejam agrupadas e processadas juntas pelos serviços downstream. |
| `action` | O tipo de ação solicitado na ordem de trabalho de exclusão do registro. |
| `createdAt` | O carimbo de data e hora quando a ordem de trabalho foi criada. |
| `updatedAt` | O carimbo de data e hora quando a ordem de trabalho foi atualizada pela última vez. |
| `operationCount` | O número de operações incluídas na ordem de serviço. |
| `targetServices` | Uma lista de serviços de destino afetados por essa ordem de serviço de exclusão de registro. |
| `status` | O status atual da ordem de serviço de exclusão do registro. |
| `createdBy` | O email e o identificador do usuário que criou a ordem de trabalho de exclusão de registro. |
| `datasetId` | O identificador exclusivo do conjunto de dados associado à ordem de serviço. |
| `datasetName` | O nome do conjunto de dados associado à ordem de serviço. |
| `displayName` | Um rótulo legível para a ordem de serviço de exclusão do registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |

## Atualizar uma ordem de serviço de exclusão de registro

Atualize o `name` e o `description` de uma ordem de serviço de exclusão de registro fazendo uma solicitação PUT para o ponto de extremidade `/workorder/{WORKORDER_ID}`.

**Formato da API**

```http
PUT /workorder/{WORKORDER_ID}
```

A tabela a seguir descreve o parâmetro para essa solicitação.

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | O identificador exclusivo da ordem de serviço de deleção do registro que você deseja atualizar. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

A tabela a seguir descreve as propriedades que você pode atualizar.

| Propriedade | Descrição |
| --- | --- |
| `name` | O rótulo em formato legível por humanos atualizado para a ordem de serviço de exclusão de registro. |
| `description` | A descrição atualizada da ordem de trabalho de exclusão de registro. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna a solicitação de ordem de serviço atualizada.

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
  "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Propriedade | Descrição |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | O identificador exclusivo da ordem de serviço de exclusão do registro. |
| `orgId` | O identificador exclusivo da sua organização. |
| `bundleId` | O identificador exclusivo do conjunto que contém esta ordem de serviço de exclusão de registro. O agrupamento permite que várias ordens de exclusão sejam agrupadas e processadas juntas pelos serviços downstream. |
| `action` | O tipo de ação solicitado na ordem de trabalho de exclusão do registro. |
| `createdAt` | O carimbo de data e hora quando a ordem de trabalho foi criada. |
| `updatedAt` | O carimbo de data e hora quando a ordem de trabalho foi atualizada pela última vez. |
| `operationCount` | O número de operações incluídas na ordem de serviço. |
| `targetServices` | Uma lista de serviços de destino afetados por essa ordem de serviço de exclusão de registro. |
| `status` | O status atual da ordem de serviço de exclusão do registro. Os valores possíveis são: `received`,`validated`, `submitted`, `ingested`, `completed` e `failed`. |
| `createdBy` | O email e o identificador do usuário que criou a ordem de trabalho de exclusão de registro. |
| `datasetId` | O identificador exclusivo do conjunto de dados associado à ordem de serviço de exclusão do registro. |
| `datasetName` | O nome do conjunto de dados associado à ordem de serviço de exclusão do registro. |
| `displayName` | Um rótulo legível para a ordem de serviço de exclusão do registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |
| `productStatusDetails` | Uma matriz que lista o status atual dos processos downstream para a solicitação. Cada objeto contém:<ul><li>`productName`: O nome do serviço downstream.</li><li>`productStatus`: o status de processamento atual do serviço downstream.</li><li>`createdAt`: O carimbo de data/hora quando o status mais recente foi postado pelo serviço.</li></ul>Essa propriedade fica disponível depois que a ordem de serviço é enviada aos serviços downstream para iniciar o processamento. |

{style="table-layout:auto"}
