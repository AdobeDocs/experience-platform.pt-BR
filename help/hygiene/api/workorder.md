---
title: Endpoint da API de ordem de trabalho
description: O ponto de extremidade /workorder na API de higiene de dados permite gerenciar de forma programática tarefas de exclusão para identidades.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: 54f92257d21f918b5d60c982670f96d30e879c60
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 4%

---

# Ponto de extremidade da ordem de trabalho

A variável `/workorder` O endpoint na API da higiene de dados permite gerenciar de forma programática as solicitações de exclusão de registros no Adobe Experience Platform.

>[!IMPORTANT]
>
>As solicitações de exclusão de registro só estão disponíveis para organizações que compraram **Adobe Healthcare Shield**.
>
>
>As exclusões de registros devem ser usadas para limpeza de dados, remoção de dados anônimos ou minimização de dados. Eles são **não** a ser usado para solicitações de direitos do titular dos dados (conformidade) como relacionadas a regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Para todos os casos de uso de conformidade, use [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) em vez disso.

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, reveja o [visão geral](./overview.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Criar uma solicitação de exclusão de registro {#create}

Você pode excluir uma ou mais identidades de um único conjunto de dados ou de todos os conjuntos de dados fazendo uma solicitação POST para o `/workorder` terminal.

**Formato da API**

```http
POST /workorder
```

**Solicitação**

Dependendo do valor da variável `datasetId` fornecido na carga da solicitação, a chamada à API excluirá identidades de todos os conjuntos de dados ou de um único conjunto de dados especificado. A solicitação a seguir exclui três identidades de um conjunto de dados específico.

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
| `datasetId` | Se você estiver excluindo de um único conjunto de dados, esse valor deverá ser a ID do conjunto de dados em questão. Se estiver excluindo de todos os conjuntos de dados, defina o valor como `ALL`.<br><br>Se você estiver especificando um único conjunto de dados, o esquema do Experience Data Model (XDM) associado ao conjunto de dados deve ter uma identidade primária definida. |
| `displayName` | O nome de exibição da solicitação de exclusão de registro. |
| `description` | Uma descrição para a solicitação de exclusão de registro. |
| `identities` | Uma matriz que contém as identidades de pelo menos um usuário cujas informações você deseja excluir. Cada identidade é composta de um [namespace de identidade](../../identity-service/namespaces.md) e um valor:<ul><li>`namespace`: contém uma única propriedade de sequência de caracteres, `code`, que representa o namespace de identidade. </li><li>`id`: o valor da identidade.</ul>Se `datasetId` especifica um único conjunto de dados, cada entidade em `identities` deve usar o mesmo namespace de identidade que a identidade primária do esquema.<br><br>Se `datasetId` está definida como `ALL`, o `identities` a matriz não está restrita a um único namespace, pois cada conjunto de dados pode ser diferente. No entanto, suas solicitações ainda restringem os namespaces disponíveis para sua organização, conforme relatado por [Serviço de identidade](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

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
| `orgId` | Sua ID de organização. |
| `bundleId` | A ID do pacote ao qual esta ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de serviço. Para exclusões de registro, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |

{style="table-layout:auto"}

## Recuperar o status de uma exclusão de registro (#lookup)

Depois [criando uma solicitação de exclusão de registro](#create), é possível verificar o status usando uma solicitação do GET.

**Formato da API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | A variável `workorderId` da exclusão de registro que você está pesquisando. |

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
| `orgId` | Sua ID de organização. |
| `bundleId` | A ID do pacote ao qual esta ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de serviço. Para exclusões de registro, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |
| `productStatusDetails` | Uma matriz que lista o status atual dos processos downstream relacionados à solicitação. Cada objeto de matriz contém as seguintes propriedades:<ul><li>`productName`: o nome do serviço downstream.</li><li>`productStatus`: o status de processamento atual da solicitação do serviço downstream.</li><li>`createdAt`: um carimbo de data e hora de quando o status mais recente foi postado pelo serviço.</li></ul> |

## Atualizar uma solicitação de exclusão de registro

Você pode atualizar o `displayName` e `description` para uma exclusão de registro fazendo uma solicitação PUT.

**Formato da API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | A variável `workorderId` da exclusão de registro que você está pesquisando. |

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
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para consultar o status da exclusão posteriormente. |
| `orgId` | Sua ID de organização. |
| `bundleId` | A ID do pacote ao qual esta ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas para serem processadas pelos serviços downstream. |
| `action` | A ação que está sendo executada pela ordem de serviço. Para exclusões de registro, o valor é `identity-delete`. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `updatedAt` | Um carimbo de data e hora de quando a ordem de exclusão foi atualizada pela última vez. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
| `datasetId` | A ID do conjunto de dados sujeito à solicitação. Se a solicitação for para todos os conjuntos de dados, o valor será definido como `ALL`. |
| `productStatusDetails` | Uma matriz que lista o status atual dos processos downstream relacionados à solicitação. Cada objeto de matriz contém as seguintes propriedades:<ul><li>`productName`: o nome do serviço downstream.</li><li>`productStatus`: o status de processamento atual da solicitação do serviço downstream.</li><li>`createdAt`: um carimbo de data e hora de quando o status mais recente foi postado pelo serviço.</li></ul> |

{style="table-layout:auto"}
