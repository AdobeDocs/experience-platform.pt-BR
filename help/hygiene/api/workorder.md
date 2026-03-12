---
title: Registrar Ordens de Serviço de Exclusão
description: Saiba como usar o ponto de extremidade /workorder na API de higiene de dados para gerenciar ordens de trabalho de exclusão de registro no Adobe Experience Platform. Este guia aborda cotas, linhas do tempo de processamento e uso da API.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 5ca3e4feae3096e41689610ac3afac7e93047149
workflow-type: tm+mt
source-wordcount: '3316'
ht-degree: 1%

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

A tabela a seguir mostra os limites de envio de identificador por produto e nível de direito. Para cada produto, o limite mensal é o menor de dois valores: um limite de identificador fixo ou um limite baseado em porcentagem vinculado ao volume de dados licenciado. Na prática, a maioria das organizações tem limites mensais mais baixos com base em seu público-alvo endereçável real ou direitos de linha do Adobe Customer Journey Analytics.

| Produto | Descrição do Direito | Limite mensal (o que for menor) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP ou Adobe Journey Optimizer | Sem o Privacy and Security Shield ou o complemento Healthcare Shield | 2.000.000 identificadores ou 5% do público endereçável |
| Real-Time CDP ou Adobe Journey Optimizer | Com o Privacy and Security Shield ou o complemento Healthcare Shield | 15.000.000 identificadores ou 10% do público endereçável |
| Customer Journey Analytics | Sem o Privacy and Security Shield ou o complemento Healthcare Shield | 2.000.000 identificadores ou 100 identificadores por milhão de linhas de direito do Customer Journey Analytics |
| Customer Journey Analytics | Com o Privacy and Security Shield ou o complemento Healthcare Shield | 15.000.000 identificadores ou 200 identificadores por milhão de linhas de direito do Customer Journey Analytics |

>[!NOTE]
>
>- As cotas são redefinidas no primeiro dia de cada mês. Cota não utilizada **não** é transferida.
>- O uso da cota é baseado no direito mensal licenciado de sua organização para **identificadores enviados**. As cotas não são aplicadas por medidas de proteção do sistema, mas podem ser monitoradas e revisadas.
>- A capacidade da ordem de trabalho de exclusão do registro é um **serviço compartilhado**. Seu limite mensal reflete os direitos mais altos no Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics e em qualquer complemento do Shield aplicável.

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
        "identity",
        "ajo"
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
| `targetServices` | O conjunto de serviços de público alvo que processaram a exclusão. O valor padrão depende dos direitos da organização. Para organizações com Real-Time CDP ou Adobe Journey Optimizer, o padrão é o conjunto completo de serviços com suporte (`["datalake", "identity", "profile", "ajo"]`). Para organizações exclusivas da Customer Journey Analytics (sem um direito ao Perfil de Cliente em Tempo Real), o único valor válido é [&quot;datalake&quot;]. |
| `status` | Status atual da ordem de serviço. Os valores possíveis são: `received`,`validated`, `submitted`, `ingested`, `completed` e `failed`. |
| `createdBy` | O email e o identificador do usuário que criou a ordem de trabalho. |
| `datasetId` | Os conjuntos de dados direcionados pela ordem de trabalho: uma única ID de conjunto de dados, uma lista separada por vírgulas de IDs de conjunto de dados (conjunto de dados múltiplo) ou o literal `ALL`. Quando a solicitação usou o modo somente de perfil, esse valor é `ALL`. |
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

Para excluir registros associados a uma ou mais identidades de um único conjunto de dados, vários conjuntos de dados ou todos os conjuntos de dados, faça uma solicitação POST para o ponto de extremidade `/workorder`.

As ordens de serviço são processadas de forma assíncrona e são exibidas na lista de ordens de serviço após o envio. As opções de vários conjuntos de dados e somente de perfil (serviços direcionados) estão disponíveis para todos os clientes a partir da versão de março de 2026 do Experience Platform.

>[!TIP]
>
>Cada ordem de serviço de exclusão de registro enviada por meio da API pode incluir até **100.000 identidades**. Envie o máximo de identidades por solicitação possível para maximizar a eficiência. Evite envios de baixo volume, como ordens de trabalho de ID única.

**Formato da API**

```http
POST /workorder
```

>[!IMPORTANT]
>
>As ordens de trabalho de exclusão de registro atuam exclusivamente no campo **identidade principal**. As seguintes limitações se aplicam:
>
>- **O esquema do conjunto de dados deve definir uma identidade primária ou um mapa de identidade.** Só é possível excluir registros de conjuntos de dados cujo esquema XDM associado define uma identidade primária ou mapa de identidade.
>- **As identidades secundárias não foram verificadas.** Se um conjunto de dados contiver vários campos de identidade, somente a identidade principal será usada para correspondência. Os registros não podem ser direcionados ou excluídos com base em identidades não primárias.
>- **Os registros sem uma identidade principal preenchida são ignorados.** Se um registro não tiver metadados de identidade primários preenchidos, ele não estará qualificado para exclusão.
>- **Dados assimilados antes da configuração de identidade não são qualificados.** Se o campo de identidade principal foi adicionado a um esquema após a assimilação de dados, os registros assimilados anteriormente não poderão ser excluídos por meio de ordens de trabalho de exclusão de registro.

>[!NOTE]
>
>Se você tentar criar uma ordem de serviço de exclusão de registro para um conjunto de dados que já tem uma expiração ativa, a solicitação retornará HTTP 400 (Solicitação inválida). Uma expiração ativa é qualquer exclusão agendada que ainda não foi concluída.

### Formatos de carga de identidade (`namespacesIdentities` ou `identities`)

O corpo da solicitação deve incluir **exatamente um** dos itens a seguir.

| Formato | Propriedade | Forma | Quando usar |
|--------|----------|-------|-------------|
| **Recomendado** | `namespacesIdentities` | Matriz de objetos com `namespace` (por exemplo, `{ "code": "email" }`) e `ids` (matriz de sequências de identidade). | Use para todas as cargas, sejam elas construídas manualmente ou geradas por código. Isso é especialmente eficiente para reduzir o tamanho da carga quando muitas identidades compartilham o mesmo namespace. |
| **Também aceito** | `identities` | Matriz de objetos com `namespace` (por exemplo, `{ "code": "email" }`) e um único `id` (string). | Aceito para compatibilidade com versões anteriores. Este é o formato produzido pelos [scripts de conversão de csv em higiene de dados](#convert-id-lists-to-json-for-record-delete-requests). O serviço normaliza esse formato internamente, de modo que o comportamento resultante é idêntico. |

Se você enviar **ambas as propriedades**, **nenhuma propriedade** ou fornecer **uma matriz vazia** para a propriedade incluída, a API retornará **HTTP 400 (Solicitação inválida)** com uma destas mensagens:

- **Ambas as propriedades fornecidas:** `"Identities and NamespacesIdentities are not allowed at the same time"`
- **Lista não fornecida ou vazia:** `"Identities are Empty for Delete Identity request."`

**Solicitação**

A solicitação a seguir exclui todos os registros associados a endereços de email especificados de um conjunto de dados específico. Ele usa o formato `namespacesIdentities` recomendado.

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
            "ids": [
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
| `datasetId` | O identificador exclusivo dos conjuntos de dados. O valor deve ser exatamente um destes: o literal `ALL`, uma única ID de conjunto de dados ou uma lista separada por vírgulas de duas ou mais IDs de conjunto de dados (por exemplo, `"id1,id2,id3"`). Você não pode combinar `ALL` com IDs específicas. As solicitações de um único conjunto de dados se comportam como antes, as solicitações de vários conjuntos de dados excluem as identidades de cada conjunto de dados listado e `ALL` direciona cada conjunto de dados. Os conjuntos de dados devem ter uma identidade primária ou mapa de identidade. Se existir um mapa de identidade, ele estará presente como um campo de nível superior chamado `identityMap`.<br>**Observação**: uma linha de conjunto de dados pode ter muitas identidades em seu mapa de identidades, mas apenas uma pode ser marcada como primária. `"primary": true` deve ser incluído para forçar `id` a corresponder a uma identidade principal.<br>Ao usar `targetServices` para exclusão somente de perfil, `datasetId` deve ser `ALL`. |
| `targetServices` | Opcional. Especifica quais serviços devem processar a exclusão. O valor padrão depende dos direitos da organização. Organizações com Real-Time CDP ou Adobe Journey Optimizer recebem o conjunto completo de serviços suportados (`["datalake", "identity", "profile", "ajo"]`) por padrão. Organizações com Customer Journey Analytics, mas sem um direito de Perfil de Cliente em Tempo Real, só podem usar [&quot;datalake&quot;]. Para limitar a exclusão somente a dados relacionados ao perfil e deixar o data lake intacto, defina como `["identity", "profile", "ajo"]` (em qualquer ordem). Este modo somente de perfil requer um direito de Real-Time CDP ou Adobe Journey Optimizer e `datasetId` deve ser `ALL`. |
| `identities` | **Use exatamente um de `identities` ou `namespacesIdentities`.** Matriz de objetos, cada uma com `namespace` (objeto com `code`, por exemplo, `"email"`) e `id` (cadeia de caracteres de identidade única). Aceito para compatibilidade com versões anteriores e produzido pelos scripts de conversão. O serviço normaliza esse formato internamente; o comportamento é idêntico. Consulte [Formato de carga da identidade](#identity-payload-format-identities-or-namespacesidentities) acima. |
| `namespacesIdentities` | **Use exatamente um de `identities` ou `namespacesIdentities`.** Matriz de objetos, cada uma com `namespace` (objeto com `code`, por exemplo, `"email"`) e `ids` (matriz de cadeias de caracteres de identidade). Recomendado para todas as cargas. A propriedade `namespacesIdentities` é mais compacta quando muitas identidades compartilham um namespace. Consulte [Formato de carga da identidade](#identity-payload-format-identities-or-namespacesidentities) acima. Namespaces de identidade: [documentação de namespace de identidade](../../identity-service/features/namespaces.md), [API do Serviço de Identidade](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

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
    "identity",
    "ajo"
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
| `datasetId` | O identificador exclusivo dos conjuntos de dados. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. Para solicitações de vários conjuntos de dados, o valor reflete a lista separada por vírgulas ou a ID única enviada. |
| `datasetName` | O nome do conjunto de dados para esta ordem de serviço de exclusão de registro. |
| `displayName` | Um rótulo legível para a ordem de serviço de exclusão do registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |

{style="table-layout:auto"}

O valor de resposta `targetServices` ecoa sua solicitação ou mostra o conjunto padrão completo quando omitido (consulte a tabela de resposta acima).

### Conjunto de dados múltiplos e somente perfil (API) {#multi-dataset-profile-only}

As seguintes opções estão disponíveis somente por meio da API e não são compatíveis com a interface da higiene de dados. Eles controlam quais conjuntos de dados e quais serviços processam a exclusão, permitindo envios de vários conjuntos de dados e solicitações de serviço direcionadas somente por perfil.

A tabela a seguir resume como o corpo da solicitação e o comportamento mudam para cada opção.

| Opção | Solicitar alteração de corpo | Comportamento |
|--------|---------------------|----------|
| **Conjunto de dados múltiplos** | Use uma lista separada por vírgulas em `datasetId` (ex.: `"id1,id2,id3"`). ID única ou `ALL` inalterada. | As identidades são excluídas dos conjuntos de dados listados (ou de um conjunto de dados, ou de todos os conjuntos de dados quando `ALL`). |
| **Somente perfil (serviços direcionados)** | Adicionar `targetServices` com exatamente `["identity", "profile", "ajo"]` (qualquer pedido). Exige `datasetId`: `"ALL"`. | Somente Identidade, Perfil e Adobe Journey Optimizer processam a exclusão; o data lake não é modificado. |

#### Solicitações de vários conjuntos de dados

O campo `datasetId` é dividido em vírgulas: use uma única ID (o mesmo comportamento de antes), uma lista de IDs separada por vírgulas ou o literal `ALL`. Para excluir identidades de vários conjuntos de dados específicos em uma ordem de trabalho, forneça uma lista separada por vírgulas:

```json
"datasetId": "6707eb36eef4d42ab86d9fbe,6643f00c16ddf51767fcf780"
```

As identidades são excluídas de cada um dos conjuntos de dados listados. As solicitações de um único conjunto de dados funcionam como sempre funcionam; use `ALL` para direcionar cada conjunto de dados. O valor deve ser exatamente um de: `ALL`, uma única ID de conjunto de dados ou duas ou mais IDs de conjunto de dados separadas por vírgulas (sem combinar `ALL` com IDs específicas).

#### Somente perfil (serviços direcionados)

Para remover apenas dados de identidade e relacionados ao perfil sem alterar o data lake, inclua `targetServices` com exatamente estes três valores em qualquer ordem: `identity`, `profile` e `ajo`. Identidade, Perfil e AJO são explicitamente incluídos; o data lake é excluído. Neste modo, `datasetId` deve ser `ALL` (o caso de uso é a exclusão completa do perfil, não fragmentos por conjunto de dados).

O exemplo a seguir cria uma ordem de serviço de deleção de registro somente de perfil:

```shell
curl -X POST \
  "https://platform.adobe.io/data/core/hygiene/workorder" \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
    "action": "delete_identity",
    "datasetId": "ALL",
    "displayName": "Profile-only delete for specified identity",
    "description": "Delete identity, profile, and AJO data only; datalake unchanged.",
    "targetServices": ["identity", "profile", "ajo"],
    "namespacesIdentities": [
      {
        "namespace": { "code": "email" },
        "ids": ["user@example.com"]
      }
    ]
  }'
```

As respostas bem-sucedidas para solicitações de vários conjuntos de dados ou somente de perfil seguem a mesma forma que outras respostas de ordem de trabalho. Os `datasetId` e `targetServices` retornados refletem os valores na solicitação (ou na lista padrão completa quando `targetServices` é omitido), para que você possa confirmar o que foi enviado.

>[!NOTE]
>
>A propriedade de ação para ordens de trabalho de exclusão de registro está atualmente `identity-delete` nas respostas da API. Se a API mudar para usar um valor diferente (como `delete_identity`), esta documentação será atualizada adequadamente.

## Converter listas de ID em JSON para solicitações de exclusão de registro (#convert-id-lists-to-json-for-record-delete-requests)

Use scripts de conversão para produzir as cargas JSON necessárias para o terminal `/workorder` quando seus identificadores estiverem em arquivos CSV, TSV ou TXT. Essa abordagem é especialmente útil ao trabalhar com arquivos de dados existentes. Para obter scripts e instruções prontos para uso, consulte o [repositório GitHub de csv para higiene de dados](https://github.com/perlmonger42/csv-to-data-hygiene).

Os scripts geram o formato **`identities`** — um `id` por objeto com um `namespace`. A API aceita esse formato como está; você pode enviar o JSON gerado diretamente no corpo da POSTAGEM para `/workorder` sem conversão. O formato recomendado é **`namespacesIdentities`**; consulte [Criar uma ordem de trabalho de exclusão de registro](#create) e [Formato de carga de identidade](#identity-payload-format-identities-or-namespacesidentities).

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
| `namespace` | O código do namespace de identidade passado para o script (por exemplo, `email`). O JSON gerado usa isso na propriedade `namespace.code` de cada objeto. |
| `dataset-id` | O identificador exclusivo do(s) conjunto(s) de dados: uma única ID, IDs separadas por vírgulas para vários conjuntos de dados ou `ALL` para todos os conjuntos de dados. |
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
| `datasetId` | O identificador exclusivo do(s) conjunto(s) de dados: uma única ID, IDs separadas por vírgula ou `ALL`. |
| `displayName` | Um rótulo legível por humanos para esta ordem de serviço de exclusão de registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |
| `identities` | Uma matriz de objetos, cada um contendo:<br><ul><li> `namespace`: um objeto com uma propriedade `code` especificando o namespace de identidade (por exemplo, &quot;email&quot;).</li><li> `id`: O valor de identidade a ser excluído para este namespace.</li></ul> |

{style="table-layout:auto"}

### Enviar os dados JSON gerados para o ponto de extremidade `/workorder`

A saída do script usa o formato `identities`, que a API aceita como está. Use a carga JSON convertida como o corpo da solicitação (`-d`) ao enviar sua solicitação POST `curl` para o ponto de extremidade `/workorder`. Para obter opções completas de solicitação e regras de validação, consulte [Criar uma ordem de trabalho de exclusão de registro](#create).

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
| `datasetId` | O identificador exclusivo do(s) conjunto(s) de dados associado(s) à ordem de trabalho (ID única, IDs separadas por vírgula ou `ALL`). |
| `datasetName` | O nome do conjunto de dados associado à ordem de serviço. |
| `displayName` | Um rótulo legível para a ordem de serviço de exclusão do registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |

## Atualizar uma ordem de serviço de exclusão de registro {#update}

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
| `datasetId` | O identificador exclusivo do(s) conjunto(s) de dados associado(s) à ordem de trabalho de exclusão de registro (ID única, IDs separadas por vírgula ou `ALL`). |
| `datasetName` | O nome do conjunto de dados associado à ordem de serviço de exclusão do registro. |
| `displayName` | Um rótulo legível para a ordem de serviço de exclusão do registro. |
| `description` | Uma descrição da ordem de serviço de exclusão do registro. |
| `productStatusDetails` | Uma matriz que lista o status atual dos processos downstream para a solicitação. Cada objeto contém:<ul><li>`productName`: O nome do serviço downstream.</li><li>`productStatus`: o status de processamento atual do serviço downstream.</li><li>`createdAt`: O carimbo de data/hora quando o status mais recente foi postado pelo serviço.</li></ul>Essa propriedade fica disponível depois que a ordem de serviço é enviada aos serviços downstream para iniciar o processamento. |

{style="table-layout:auto"}
