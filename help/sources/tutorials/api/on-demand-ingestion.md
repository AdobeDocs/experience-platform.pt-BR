---
keywords: Experience Platform; home; tópicos populares; serviço de fluxo;
title: (Beta) Criar uma Execução de Fluxo para Assimilação sob Demanda Usando a API do Serviço de Fluxo
description: Este tutorial aborda as etapas para criar uma execução de fluxo para assimilação sob demanda usando a API do Serviço de Fluxo
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 795b1af6421c713f580829588f954856e0a88277
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 2%

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
| `params.startTime` | Um número inteiro que define a hora de início da execução. O valor é representado na época unix. |
| `params.windowStartTime` | Um número inteiro que define a hora de início da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.windowEndTime` | Um número inteiro que define a hora de término da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.deltaColumn` | A coluna delta é necessária para particionar os dados e separar os dados ingeridos recentemente dos dados históricos. **Observação**: O `deltaColumn` só é necessário ao criar a primeira execução de fluxo. |
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
| `id` | A ID da execução do fluxo recém-criado. Consulte o guia sobre [recuperação de especificações de fluxo](../api/collect/database-nosql.md#specs) para obter mais informações sobre especificações de execução baseadas em tabela. |
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
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `flowId` | A ID do fluxo no qual a execução do fluxo será criada. |
| `params.startTime` | Um número inteiro que define a hora de início da execução. O valor é representado na época unix. |
| `params.windowStartTime` | Um número inteiro que define a hora de início da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |
| `params.windowEndTime` | Um número inteiro que define a hora de término da janela durante a qual os dados devem ser obtidos. O valor é representado em horário unix. |

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
| `id` | A ID da execução do fluxo recém-criado. Consulte o guia sobre [recuperação de especificações de fluxo](../api/collect/database-nosql.md#specs) para obter mais informações sobre especificações de execução baseadas em tabela. |
| `etag` | A versão do recurso da execução do fluxo. |

## Monitore suas execuções de fluxo

Depois que a execução do fluxo tiver sido criada, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções do fluxo, status de conclusão e erros. Para monitorar as execuções de fluxo usando a API, consulte o tutorial em [monitoramento de fluxos de dados na API ](./monitor.md). Para monitorar as execuções de fluxo usando a interface do usuário da plataforma, consulte o guia em [monitorar fluxos de dados de fontes usando o painel de monitoramento](../../../dataflows/ui/monitor-sources.md).
