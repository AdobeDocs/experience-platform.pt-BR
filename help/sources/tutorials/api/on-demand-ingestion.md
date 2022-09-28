---
keywords: Experience Platform; home; tópicos populares; serviço de fluxo;
title: (Beta) Criar uma Execução de Fluxo para Assimilação sob Demanda Usando a API do Serviço de Fluxo
description: Este tutorial aborda as etapas para criar uma execução de fluxo para assimilação sob demanda usando a API do Serviço de Fluxo
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 61b3799a4d8c8b6682babd85b6f50a7e69778553
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 1%

---

# (Beta) Crie uma execução de fluxo para assimilação sob demanda usando o [!DNL Flow Service] API

>[!IMPORTANT]
>
>A assimilação por demanda está atualmente em beta e sua organização pode ainda não ter acesso a ela. A funcionalidade descrita nesta documentação está sujeita a alterações.

As execuções de fluxo representam uma instância de execução de fluxo. Por exemplo, se um fluxo for agendado para ser executado a cada hora às 9h, às 10h e às 11h, então você terá três instâncias de uma execução de fluxo. As execuções de fluxo são específicas de sua organização específica.

A assimilação sob demanda oferece a capacidade de criar uma execução de fluxo em relação a um fluxo de dados específico. Isso permite que os usuários criem uma execução de fluxo, com base em determinados parâmetros e criem um ciclo de assimilação, sem tokens de serviço. O suporte para assimilação sob demanda está disponível somente para fontes em lote.

Este tutorial aborda as etapas sobre como usar a assimilação sob demanda e criar uma execução de fluxo usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

>[!NOTE]
>
>Para criar uma execução de fluxo, primeiro você deve ter a ID de fluxo de um fluxo de dados agendado para assimilação única.

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).

## Criar uma execução de fluxo para uma origem baseada em tabela

Para criar um fluxo para uma fonte baseada em tabela, faça uma solicitação de POST para a variável [!DNL Flow Service] API ao fornecer a ID do fluxo no qual você deseja criar a execução, bem como valores para a hora de início, hora de término e coluna delta.

>[!TIP]
>
>As fontes baseadas em tabela incluem as seguintes categorias de origem: publicidade, análises, consentimento e preferências, CRMs, sucesso do cliente, banco de dados, automação de marketing, pagamentos e protocolos.

**Formato da API**

```http
POST /runs/
```

**Solicitação**

A solicitação a seguir cria uma execução de fluxo para ID de fluxo `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Você só precisa fornecer a variável `deltaColumn` ao criar sua primeira execução de fluxo. Depois disso, `deltaColumn` será corrigido como parte de `copy` transformação no fluxo e será tratada como a fonte da verdade. Qualquer tentativa de alterar o `deltaColumn` através dos parâmetros de execução de fluxo resultará em um erro.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `flowId` | A ID do fluxo no qual a execução do fluxo será criada. |
| `params.windowStartTime` | Um número inteiro que define a hora de início da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.windowEndTime` | Um número inteiro que define a hora de término da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.deltaColumn` | A coluna delta é necessária para particionar os dados e separar os dados ingeridos recentemente dos dados históricos. |
| `params.deltaColumn.name` | O nome da coluna delta. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da execução de fluxo recém-criada, incluindo sua execução exclusiva `id`.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID da execução do fluxo recém-criado. Consulte o guia sobre [recuperação de especificações de fluxo](../api/collect/database-nosql.md#specs) para obter mais informações sobre especificações de execução baseadas em tabela. |
| `createdAt` | O carimbo de data e hora unix que designa quando a execução do fluxo foi criada. |
| `updatedAt` | O carimbo de data e hora unix que designa quando a execução do fluxo foi atualizada pela última vez. |
| `createdBy` | A ID da organização do usuário que criou a execução do fluxo. |
| `updatedBy` | A ID da organização do usuário que atualizou a execução do fluxo pela última vez. |
| `createdClient` | O cliente do aplicativo que criou a execução de fluxo. |
| `updatedClient` | O cliente do aplicativo que atualizou a execução do fluxo pela última vez. |
| `sandboxId` | A ID da sandbox que contém a execução do fluxo. |
| `sandboxName` | O nome da sandbox que contém a execução do fluxo. |
| `imsOrgId` | A ID da organização. |
| `flowId` | A ID do fluxo no qual a execução do fluxo é criada. |
| `params.windowStartTime` | Um número inteiro que define a hora de início da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.windowEndTime` | Um número inteiro que define a hora de término da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.deltaColumn` | A coluna delta é necessária para particionar os dados e separar os dados ingeridos recentemente dos dados históricos. **Observação**: O `deltaColumn` só é necessário ao criar a primeira execução de fluxo. |
| `params.deltaColumn.name` | O nome da coluna delta. |
| `etag` | A versão do recurso da execução do fluxo. |
| `metrics` | Essa propriedade exibe um resumo do status da execução do fluxo. |

## Criar uma execução de fluxo para uma origem baseada em arquivo

Para criar um fluxo para uma fonte baseada em arquivo, faça uma solicitação de POST para a variável [!DNL Flow Service] Ao fornecer a ID do fluxo, você deseja criar os valores run-against e para o tempo inicial e final.

>[!TIP]
>
>As fontes baseadas em arquivo incluem todas as fontes de armazenamento em nuvem.

**Formato da API**

```http
POST /runs/
```

**Solicitação**

A solicitação a seguir cria uma execução de fluxo para ID de fluxo `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `flowId` | A ID do fluxo no qual a execução do fluxo será criada. |
| `params.windowStartTime` | Um número inteiro que define a hora de início da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.windowEndTime` | Um número inteiro que define a hora de término da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da execução de fluxo recém-criada, incluindo sua execução exclusiva `id`.


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID da execução do fluxo recém-criado. Consulte o guia sobre [recuperação de especificações de fluxo](../api/collect/cloud-storage.md#specs) para obter mais informações sobre especificações de execução baseadas em arquivo. |
| `createdAt` | O carimbo de data e hora unix que designa quando a execução do fluxo foi criada. |
| `updatedAt` | O carimbo de data e hora unix que designa quando a execução do fluxo foi atualizada pela última vez. |
| `createdBy` | A ID da organização do usuário que criou a execução do fluxo. |
| `updatedBy` | A ID da organização do usuário que atualizou a execução do fluxo pela última vez. |
| `createdClient` | O cliente do aplicativo que criou a execução de fluxo. |
| `updatedClient` | O cliente do aplicativo que atualizou a execução do fluxo pela última vez. |
| `sandboxId` | A ID da sandbox que contém a execução do fluxo. |
| `sandboxName` | O nome da sandbox que contém a execução do fluxo. |
| `imsOrgId` | A ID da organização. |
| `flowId` | A ID do fluxo no qual a execução do fluxo é criada. |
| `params.windowStartTime` | Um número inteiro que define a hora de início da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.windowEndTime` | Um número inteiro que define a hora de término da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `etag` | A versão do recurso da execução do fluxo. |
| `metrics` | Essa propriedade exibe um resumo do status da execução do fluxo. |


## Monitore suas execuções de fluxo

Depois que a execução do fluxo tiver sido criada, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções do fluxo, status de conclusão e erros. Para monitorar as execuções de fluxo usando a API, consulte o tutorial em [monitoramento de fluxos de dados na API ](./monitor.md). Para monitorar as execuções de fluxo usando a interface do usuário da plataforma, consulte o guia em [monitorar fluxos de dados de fontes usando o painel de monitoramento](../../../dataflows/ui/monitor-sources.md).
