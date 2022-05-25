---
title: Endpoint da API de ordem de trabalho
description: O endpoint /workorder na API da Higiene de Dados permite gerenciar programaticamente tarefas de exclusão para identidades de consumidores.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 5%

---

# Ponto de extremidade da ordem de trabalho

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Adobe Shield for Healthcare.

O `/workorder` O endpoint na API da Higiene de dados permite gerenciar programaticamente tarefas de exclusão para identidades de consumidores no Adobe Experience Platform.

## Introdução

O endpoint usado neste guia faz parte da API da Higiene de dados. Antes de continuar, reveja o [visão geral](./overview.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Excluir identidades {#delete-identities}

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
| `action` | A ação a ser executada. O valor deve ser definido como `delete_identity` ao excluir identidades. |
| `datasetId` | Se estiver excluindo de um único conjunto de dados, esse valor deve ser a ID do conjunto de dados em questão. Se estiver excluindo de todos os conjuntos de dados, defina o valor como `ALL`.<br><br>Se você estiver especificando um único conjunto de dados, o esquema do Experience Data Model (XDM) associado do conjunto de dados deverá ter uma identidade primária definida. |
| `identities` | Uma matriz contendo as identidades de pelo menos um usuário cujas informações você gostaria de excluir. Cada identidade é composta por um [namespace de identidade](../../identity-service/namespaces.md) e um valor:<ul><li>`namespace`: Contém uma única propriedade de string, `code`, que representa o namespace de identidade. </li><li>`id`: O valor de identidade.</ul>If `datasetId` especifica um único conjunto de dados, cada entidade em `identities` deve usar o mesmo namespace de identidade que a identidade primária do esquema.<br><br>If `datasetId` está definida como `ALL`, o `identities` A matriz não está restrita a nenhum namespace único, pois cada conjunto de dados pode ser diferente. No entanto, suas solicitações ainda estão restritas aos namespaces disponíveis para sua organização, conforme relatado por [Serviço de identidade](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da exclusão de identidade.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para procurar o status da exclusão posteriormente. |
| `orgId` | A ID da sua organização. |
| `batchId` | A ID do lote ao qual essa ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas em um lote para serem processadas pelos serviços de downstream. |
| `bundleOrdinal` | A ordem em que essa ordem de exclusão foi recebida quando foi empacotada em um lote para processamento de downstream. Usado para fins de depuração. |
| `payloadByteSize` | O tamanho, em bytes, da lista de identidades fornecidas na carga da solicitação que criou esta ordem de exclusão. |
| `operationCount` | O número de identidades às quais essa ordem de exclusão se aplica. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `responseMessage` | A resposta mais recente retornada pelo sistema. Se ocorrer um erro durante o processamento, esse valor será uma string JSON contendo informações detalhadas sobre o erro para ajudá-lo a entender o que pode ter dado errado. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |

{style=&quot;table-layout:auto&quot;}

## Listar os status de todas as exclusões de identidade {#list}

Você pode listar os status de todas as exclusões de identidade fazendo uma solicitação GET.

**Formato da API**

```http
GET /workorder?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUERY_PARAMS}` | Uma lista de parâmetros de consulta opcionais para a chamada de listagem, com vários parâmetros separados por `&` caracteres. Os parâmetros de consulta aceitos são os seguintes:<ul><li>`data` - Um valor booleano que, quando definido como `true`, inclui todas as solicitações e dados de resposta adicionais recebidos para a ordem de exclusão. O padrão é `false`.</li><li>`start` - Um carimbo de data e hora para o início do período de pesquisa das ordens de exclusão.</li><li>`end` - Um carimbo de data e hora para o fim do período de pesquisa das ordens de exclusão.</li><li>`page` - A página de resposta específica a ser retornada.</li><li>`limit` - O número de registros a serem exibidos por página.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes de todas as operações de exclusão, incluindo seu status atual. O exemplo de resposta a seguir foi truncado por questões de espaço.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `results` | Contém a lista de ordens de exclusão e seus detalhes. Para obter mais informações sobre as propriedades de uma ordem de exclusão, consulte o exemplo de resposta na seção sobre [como pesquisar uma ordem de exclusão](#lookup). |
| `total` | O número total de ordens de exclusão encontradas com base nos filtros atuais. |
| `count` | O número total de pedidos de exclusão encontrados em cada página da resposta. |
| `_links` | Contém informações de paginação para ajudá-lo a explorar o restante da resposta:<ul><li>`next`: Contém um URL para a próxima página na resposta.</li><li>`page`: Contém um modelo de URL para acessar outra página na resposta ou ajustar o número de itens retornados em cada página.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Recuperar o status de uma exclusão de identidade (#lookup)

Depois de enviar uma solicitação para o [excluir uma identidade](#delete-identities), é possível verificar seu status usando uma solicitação do GET.

**Formato da API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{WORK_ORDER_ID}` | O `workorderId` da exclusão de identidade que você está procurando. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da operação de exclusão, incluindo seu status atual.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Propriedade | Descrição |
| --- | --- |
| `workorderId` | A ID da ordem de exclusão. Isso pode ser usado para procurar o status da exclusão posteriormente. |
| `orgId` | A ID da sua organização. |
| `batchId` | A ID do lote ao qual essa ordem de exclusão está associada, usada para fins de depuração. Várias ordens de exclusão são agrupadas em um lote para serem processadas pelos serviços de downstream. |
| `bundleOrdinal` | A ordem em que essa ordem de exclusão foi recebida quando foi empacotada em um lote para processamento de downstream. Usado para fins de depuração. |
| `payloadByteSize` | O tamanho, em bytes, da lista de identidades fornecidas na carga da solicitação que criou esta ordem de exclusão. |
| `operationCount` | O número de identidades às quais essa ordem de exclusão se aplica. |
| `createdAt` | Um carimbo de data e hora de quando a ordem de exclusão foi criada. |
| `responseMessage` | A resposta mais recente retornada pelo sistema. Se ocorrer um erro durante o processamento, esse valor será uma string JSON contendo informações detalhadas sobre o erro para ajudá-lo a entender o que pode ter dado errado. |
| `status` | O status atual da ordem de exclusão. |
| `createdBy` | O usuário que criou a ordem de exclusão. |
