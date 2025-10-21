---
keywords: Experience Platform;página inicial;tópicos populares;serviço de fluxo;
title: Criar uma execução de fluxo para assimilação sob demanda usando a API do serviço de fluxo
description: Saiba como criar uma execução de fluxo para assimilação sob demanda usando a API do serviço de fluxo
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: b2b835faf9cf52ea0461d43b29076eaf7b0688f1
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 2%

---

# Crie uma execução de fluxo para assimilação sob demanda usando a API [!DNL Flow Service]

As execuções de fluxo representam uma instância da execução de fluxo. Por exemplo, se um fluxo estiver agendado para ser executado por hora às 9h00, 10h10 e 11h20, você terá três instâncias de um fluxo em execução. :00:00:00 As execuções de fluxo são específicas para sua organização específica.

A assimilação sob demanda oferece a capacidade de criar uma execução de fluxo em relação a um determinado fluxo de dados. Isso permite que seus usuários criem uma execução de fluxo, com base em determinados parâmetros, e criem um ciclo de assimilação, sem tokens de serviço. O suporte para assimilação sob demanda está disponível somente para origens em lote.

Este tutorial aborda as etapas sobre como usar a assimilação sob demanda e criar uma execução de fluxo usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!TIP]
>
>A repetição de uma execução de fluxo processará somente arquivos com carimbos de data e hora que se enquadrem na faixa da execução original.

## Introdução

>[!NOTE]
>
>Para criar uma execução de fluxo, primeiro você deve ter a ID de fluxo de um fluxo de dados programado para assimilação única.

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../landing/api-guide.md).

## Criar uma execução de fluxo para uma origem baseada em tabela

Para criar um fluxo para uma origem baseada em tabela, faça uma solicitação POST para a API [!DNL Flow Service] enquanto fornece a ID do fluxo para o qual você deseja criar a execução, bem como valores para a coluna de hora de início, hora de término e delta.

>[!TIP]
>
>As fontes baseadas em tabela incluem as seguintes categorias de fonte: publicidade, análises, consentimento e preferências, CRMs, sucesso do cliente, banco de dados, automação de marketing, pagamentos e protocolos.

**Formato da API**

```http
POST /runs/
```

**Solicitação**

A solicitação a seguir cria uma execução de fluxo para a ID de fluxo `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Você só precisa fornecer o `deltaColumn` ao criar sua primeira execução de fluxo. Depois disso, `deltaColumn` será corrigido como parte da transformação de `copy` no fluxo e será tratado como a fonte da verdade. Qualquer tentativa de alterar o valor `deltaColumn` por meio dos parâmetros de execução de fluxo resultará em um erro.

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
          "startTime": "1663735590",
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
| `params.startTime` | O horário agendado para o início da execução do fluxo por demanda. Esse valor é representado no horário unix. |
| `params.windowStartTime` | A data e a hora a partir das quais os dados serão recuperados. Esse valor é representado no horário unix. |
| `params.windowEndTime` | A data e a hora em que os dados serão recuperados. Esse valor é representado no horário unix. |
| `params.deltaColumn` | A coluna delta é necessária para particionar os dados e separar os dados recém-assimilados dos dados históricos. **Observação**: `deltaColumn` é necessário somente ao criar sua primeira execução de fluxo. |
| `params.deltaColumn.name` | O nome da coluna delta. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da execução de fluxo recém-criada, incluindo sua execução exclusiva `id`.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID da execução do fluxo recém-criado. Consulte o guia em [recuperando especificações de fluxo](../api/collect/database-nosql.md#specs) para obter mais informações sobre especificações de execução baseadas em tabela. |
| `etag` | A versão do recurso da execução do fluxo. |

<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## Criar uma execução de fluxo para uma origem baseada em arquivo

Para criar um fluxo para uma origem baseada em arquivo, faça uma solicitação POST para a API [!DNL Flow Service] enquanto fornece a ID do fluxo com a qual você deseja criar a execução e os valores para a hora de início e de término.

>[!TIP]
>
>As fontes baseadas em arquivo incluem todas as fontes de armazenamento na nuvem.

**Formato da API**

```http
POST /runs/
```

**Solicitação**

A solicitação a seguir cria uma execução de fluxo para a ID de fluxo `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

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
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `flowId` | A ID do fluxo no qual a execução do fluxo será criada. |
| `params.startTime` | O horário agendado para o início da execução do fluxo por demanda. Esse valor é representado no horário unix. |
| `params.windowStartTime` | A data e a hora a partir das quais os dados serão recuperados. Esse valor é representado no horário unix. |
| `params.windowEndTime` | A data e a hora em que os dados serão recuperados. Esse valor é representado no horário unix. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da execução de fluxo recém-criada, incluindo sua execução exclusiva `id`.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | A ID da execução do fluxo recém-criado. Consulte o guia em [recuperando especificações de fluxo](../api/collect/database-nosql.md#specs) para obter mais informações sobre especificações de execução baseadas em tabela. |
| `etag` | A versão do recurso da execução do fluxo. |

## Monitore as execuções de fluxo

Após a criação da execução do fluxo, é possível monitorar os dados que estão sendo assimilados por meio dela para ver informações sobre execuções de fluxo, status de conclusão e erros. Para monitorar suas execuções de fluxo usando a API, consulte o tutorial sobre [monitoramento de fluxos de dados na API](./monitor.md). Para monitorar suas execuções de fluxo usando a interface do Experience Platform, consulte o manual sobre [fluxos de dados de fontes de monitoramento usando o painel de monitoramento](../../../dataflows/ui/monitor-sources.md).
