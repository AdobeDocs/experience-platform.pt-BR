---
title: Registrar Solicitações de Exclusão (Ponto Final da Ordem de Trabalho)
description: O ponto de extremidade /workorder na API de higiene de dados permite gerenciar de forma programática tarefas de exclusão para identidades.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---

# Registrar solicitações de exclusão (ponto de extremidade da ordem de trabalho) {#work-order-endpoint}

O ponto de extremidade `/workorder` na API da higiene de dados permite gerenciar programaticamente solicitações de exclusão de registros no Adobe Experience Platform.

>[!IMPORTANT]
> 
>As exclusões de registros devem ser usadas para limpeza de dados, remoção de dados anônimos ou minimização de dados. Eles **não** devem ser usados para solicitações de direitos do titular dos dados (conformidade) relacionadas a regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Para todos os casos de uso de conformidade, use o [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, revise a [visão geral](./overview.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Cotas e cronogramas de processamento {#quotas}

As solicitações de exclusão de registros estão sujeitas a limites diários e mensais de envio de identificadores, determinados pelo direito de licença da organização. Esses limites se aplicam às solicitações de exclusão baseadas em interface e API.

>[!NOTE]
>
>Você pode enviar até **1.000.000 identificadores por dia**, mas somente se sua cota mensal restante permitir. Se o limite mensal for inferior a 1 milhão, os envios diários não poderão exceder esse limite.

### Direito de envio mensal por produto {#quota-limits}

A tabela abaixo descreve os limites de envio de identificadores por produto e nível de direito. Para cada produto, o limite mensal é o menor de dois valores: um limite de identificador fixo ou um limite baseado em porcentagem vinculado ao volume de dados licenciado.

| Produto | Descrição do Direito | Limite mensal (o que for menor) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP ou Adobe Journey Optimizer | Sem o Privacy and Security Shield ou o complemento Healthcare Shield | 2.000.000 identificadores ou 5% do público endereçável |
| Real-Time CDP ou Adobe Journey Optimizer | Com o Privacy and Security Shield ou o complemento Healthcare Shield | 15.000.000 identificadores ou 10% do público endereçável |
| Customer Journey Analytics | Sem o Privacy and Security Shield ou o complemento Healthcare Shield | 2.000.000 identificadores ou 100 identificadores por milhão de linhas de direito do CJA |
| Customer Journey Analytics | Com o Privacy and Security Shield ou o complemento Healthcare Shield | 15.000.000 identificadores ou 200 identificadores por milhão de linhas de direito do CJA |

>[!NOTE]
>
> A maioria das organizações terá limites mensais mais baixos com base no público-alvo endereçável real ou nos direitos de linha do CJA.

As cotas são redefinidas no primeiro dia de cada mês. Cota não utilizada **não** é transferida.

>[!NOTE]
>
>As cotas são baseadas no direito mensal licenciado de sua organização para **identificadores enviados**. Esses procedimentos não são aplicados pelas medidas de proteção do sistema, mas podem ser monitorados e revisados.
>
>A Exclusão de Registro é um **serviço compartilhado**. Seu limite mensal reflete os direitos mais altos no Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics e em qualquer complemento do Shield aplicável.

### Processamento de cronogramas para envios de identificadores {#sla-processing-timelines}

Após o envio, as solicitações de exclusão de registro são enfileiradas e processadas com base no seu nível de direito.

| Descrição do produto e dos direitos | Duração da Fila | Tempo máximo de processamento (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Sem o Privacy and Security Shield ou o complemento Healthcare Shield | Até 15 dias | 30 dias |
| Com o Privacy and Security Shield ou o complemento Healthcare Shield | Normalmente, 24 horas | 15 dias |

Se sua organização exigir limites mais altos, entre em contato com o representante da Adobe para obter uma revisão de direito.

>[!TIP]
>
>Para verificar seu nível atual de uso de cota ou direito, consulte o [Guia de referência de cota](../api/quota.md).

## Criar uma solicitação de exclusão de registro {#create}

Você pode excluir uma ou mais identidades de um único conjunto de dados ou de todos os conjuntos de dados fazendo uma solicitação POST para o ponto de extremidade `/workorder`.

>[!TIP]
>
>Cada solicitação de exclusão de registro enviada pela API pode incluir até **100.000 identidades**. Para maximizar a eficiência, envie o máximo possível de identidades por solicitação e evite envios de baixo volume, como ordens de trabalho de ID única.

**Formato da API**

```http
POST /workorder
```

>[!NOTE]
>
>As solicitações de ciclo de vida dos dados só podem modificar conjuntos de dados com base nas identidades principais ou em um mapa de identidade. Uma solicitação deve especificar a identidade primária ou fornecer um mapa de identidade.

**Solicitação**

Dependendo do valor de `datasetId` fornecido na carga da solicitação, a chamada de API excluirá identidades de todos os conjuntos de dados ou de um único conjunto de dados especificado. A solicitação a seguir exclui três identidades de um conjunto de dados específico.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `action` | A ação a ser executada. O valor deve ser definido como `delete_identity` para exclusões de registro. |
| `datasetId` | Se você estiver excluindo de um único conjunto de dados, esse valor deverá ser a ID do conjunto de dados em questão. Se você estiver excluindo de todos os conjuntos de dados, defina o valor como `ALL`.<br><br>Se você estiver especificando um único conjunto de dados, o esquema do Experience Data Model (XDM) associado ao conjunto de dados deve ter uma identidade primária definida. Se o conjunto de dados não tiver uma identidade primária, ele deverá ter um mapa de identidade para ser modificado por uma solicitação do ciclo de vida dos dados.<br>Se existir um mapa de identidade, ele estará presente como um campo de nível superior chamado `identityMap`.<br>Observe que uma linha de conjunto de dados pode ter muitas identidades em seu mapa de identidade, mas apenas uma pode ser marcada como primária. `"primary": true` deve ser incluído para forçar `id` a corresponder a uma identidade principal. |
| `displayName` | O nome de exibição da solicitação de exclusão de registro. |
| `description` | Uma descrição para a solicitação de exclusão de registro. |
| `identities` | Uma matriz que contém as identidades de pelo menos um usuário cujas informações você deseja excluir. Cada identidade é composta de um [namespace de identidade](../../identity-service/features/namespaces.md) e um valor:<ul><li>`namespace`: Contém uma única propriedade de cadeia de caracteres, `code`, que representa o namespace de identidade. </li><li>`id`: o valor de identidade.</ul>Se `datasetId` especificar um único conjunto de dados, cada entidade em `identities` deverá usar o mesmo namespace de identidade que a identidade principal do esquema.<br><br>Se `datasetId` estiver definido como `ALL`, a matriz `identities` não estará restrita a nenhum namespace único, pois cada conjunto de dados pode ser diferente. No entanto, suas solicitações ainda restringem os namespaces disponíveis para sua organização, conforme relatado pelo [Serviço de Identidade](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da exclusão do registro.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para consultar o status da exclusão posteriormente. |
| `orgId` | Sua ID da organização. |
| `bundleId` | A ID do pacote ao qual esta ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de serviço. Para exclusões de registro, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |

{style="table-layout:auto"}

## Recuperar o status de uma exclusão de registro {#lookup}

Depois de [criar uma solicitação de exclusão de registro](#create), você poderá verificar seu status usando uma solicitação GET.

**Formato da API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | O `workorderId` da exclusão de registro que você está procurando. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da operação de exclusão, incluindo seu status atual.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para consultar o status da exclusão posteriormente. |
| `orgId` | Sua ID da organização. |
| `bundleId` | A ID do pacote ao qual esta ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de serviço. Para exclusões de registro, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |
| `productStatusDetails` | Uma matriz que lista o status atual dos processos downstream relacionados à solicitação. Cada objeto de matriz contém as seguintes propriedades:<ul><li>`productName`: O nome do serviço downstream.</li><li>`productStatus`: o status de processamento atual da solicitação do serviço downstream.</li><li>`createdAt`: Um carimbo de data e hora de quando o status mais recente foi postado pelo serviço.</li></ul> |

## Atualizar uma solicitação de exclusão de registro

Você pode atualizar o `displayName` e o `description` para uma exclusão de registro fazendo uma solicitação PUT.

**Formato da API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | O `workorderId` da exclusão de registro que você está procurando. |

{style="table-layout:auto"}

**Solicitação**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `displayName` | Um nome de exibição atualizado para a solicitação de exclusão de registro. |
| `description` | Uma descrição atualizada da solicitação de exclusão de registro. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da exclusão do registro.

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
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
| --- | --- |
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para consultar o status da exclusão posteriormente. |
| `orgId` | Sua ID da organização. |
| `bundleId` | A ID do pacote ao qual esta ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de serviço. Para exclusões de registro, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |
| `productStatusDetails` | Uma matriz que lista o status atual dos processos downstream relacionados à solicitação. Cada objeto de matriz contém as seguintes propriedades:<ul><li>`productName`: O nome do serviço downstream.</li><li>`productStatus`: o status de processamento atual da solicitação do serviço downstream.</li><li>`createdAt`: Um carimbo de data e hora de quando o status mais recente foi postado pelo serviço.</li></ul> |

{style="table-layout:auto"}
