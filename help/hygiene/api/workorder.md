---
title: Endpoint da API de ordem de trabalho
description: O endpoint /workorder na API da Higiene de Dados permite gerenciar programaticamente tarefas de exclusão para identidades de consumidores.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: fb9d226a4ea2d23ccbf61416e275a0de5025554f
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 5%

---

# Ponto de extremidade da ordem de trabalho

>[!IMPORTANT]
>
>Atualmente, as solicitações de exclusão do consumidor estão disponíveis apenas para organizações que compraram o Adobe Healthcare Shield ou Privacy Shield.

O `/workorder` O endpoint na API da Higiene de Dados permite gerenciar programaticamente solicitações de exclusão de clientes no Adobe Experience Platform.

## Introdução

O endpoint usado neste guia faz parte da API da Higiene de dados. Antes de continuar, reveja o [visão geral](./overview.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Criar uma solicitação de exclusão do consumidor {#delete-consumers}

É possível excluir uma ou mais identidades de consumidores de um único conjunto de dados ou de todos os conjuntos de dados, fazendo uma solicitação de POST para a `/workorder` endpoint .

**Formato da API**

```http
POST /workorder
```

**Solicitação**

Dependendo do valor da variável `datasetId` fornecida na carga da solicitação, a chamada da API excluirá identidades do consumidor de todos os conjuntos de dados ou de um único conjunto de dados especificado. A solicitação a seguir exclui três identidades de consumidor de um conjunto de dados específico.

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
        "displayName": "Example Consumer Delete Request",
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
| `action` | A ação a ser executada. O valor deve ser definido como `delete_identity` para exclusões de consumidores. |
| `datasetId` | Se estiver excluindo de um único conjunto de dados, esse valor deve ser a ID do conjunto de dados em questão. Se estiver excluindo de todos os conjuntos de dados, defina o valor como `ALL`.<br><br>Se você estiver especificando um único conjunto de dados, o esquema do Experience Data Model (XDM) associado do conjunto de dados deverá ter uma identidade primária definida. |
| `displayName` | O nome de exibição da solicitação de exclusão do consumidor. |
| `description` | Uma descrição para a solicitação de exclusão do consumidor. |
| `identities` | Uma matriz contendo as identidades de pelo menos um usuário cujas informações você gostaria de excluir. Cada identidade é composta por um [namespace de identidade](../../identity-service/namespaces.md) e um valor:<ul><li>`namespace`: Contém uma única propriedade de string, `code`, que representa o namespace de identidade. </li><li>`id`: O valor de identidade.</ul>If `datasetId` especifica um único conjunto de dados, cada entidade em `identities` deve usar o mesmo namespace de identidade que a identidade primária do esquema.<br><br>If `datasetId` está definida como `ALL`, o `identities` A matriz não está restrita a nenhum namespace único, pois cada conjunto de dados pode ser diferente. No entanto, suas solicitações ainda estão restritas aos namespaces disponíveis para sua organização, conforme relatado por [Serviço de identidade](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da exclusão do consumidor.

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
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para procurar o status da exclusão posteriormente. |
| `orgId` | Sua ID da organização. |
| `bundleId` | A ID do pacote ao qual essa ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de trabalho. Para exclusões do consumidor, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados que está sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |

{style=&quot;table-layout:auto&quot;}

## Recuperar o status de uma exclusão do consumidor (#lookup)

Depois [criação de uma solicitação de exclusão do consumidor](#delete-consumers), é possível verificar seu status usando uma solicitação do GET.

**Formato da API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | O `workorderId` da exclusão do consumidor que você está procurando. |

{style=&quot;table-layout:auto&quot;}

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
  "displayName": "Example Consumer Delete Request",
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
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para procurar o status da exclusão posteriormente. |
| `orgId` | Sua ID da organização. |
| `bundleId` | A ID do pacote ao qual essa ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de trabalho. Para exclusões do consumidor, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados que está sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |
| `productStatusDetails` | Uma matriz que lista o status atual de processos downstream relacionados à solicitação. Cada objeto de matriz contém as seguintes propriedades:<ul><li>`productName`: O nome do serviço downstream.</li><li>`productStatus`: O status de processamento atual da solicitação do serviço downstream.</li><li>`createdAt`: Um carimbo de data e hora de quando o status mais recente foi publicado pelo serviço.</li></ul> |

## Atualizar uma solicitação de exclusão do consumidor

Você pode atualizar o `displayName` e `description` para um consumidor, exclua fazendo uma solicitação de PUT.

**Formato da API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | O `workorderId` da exclusão do consumidor que você está procurando. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
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
| `displayName` | Um nome de exibição atualizado para a solicitação de exclusão do consumidor. |
| `description` | Uma descrição atualizada para a solicitação de exclusão do consumidor. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da exclusão do consumidor.

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
  "displayName" : "Update - displayName",
  "description" : "Update - description",
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
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para procurar o status da exclusão posteriormente. |
| `orgId` | Sua ID da organização. |
| `bundleId` | A ID do pacote ao qual essa ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de trabalho. Para exclusões do consumidor, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados que está sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |
| `productStatusDetails` | Uma matriz que lista o status atual de processos downstream relacionados à solicitação. Cada objeto de matriz contém as seguintes propriedades:<ul><li>`productName`: O nome do serviço downstream.</li><li>`productStatus`: O status de processamento atual da solicitação do serviço downstream.</li><li>`createdAt`: Um carimbo de data e hora de quando o status mais recente foi publicado pelo serviço.</li></ul> |

{style=&quot;table-layout:auto&quot;}
