---
keywords: Experience Platform; home; tópicos populares; serviço de fluxo;
title: Tentativa de Execução de Fluxo de Dados com Falha
description: Este tutorial aborda as etapas sobre como tentar novamente executar o fluxo de dados com falha usando a API do Serviço de Fluxo
source-git-commit: dfb95f457d7ddb730950159165ed85b2f532f9ab
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---

# Repetir as execuções de fluxo de dados com falha

>[!IMPORTANT]
>
>O suporte para repetição de execuções de fluxo de dados com falha está disponível para origens em lote. Você só pode tentar executar novamente o fluxo de dados que falharam.

Este tutorial aborda as etapas sobre como tentar novamente executar o fluxo de dados com falha usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).

## Repetir a execução do fluxo de dados com falha

Para repetir uma execução de fluxo de dados com falha, faça uma solicitação de POST para a `/runs` endpoint ao fornecer a ID de execução do seu fluxo de dados e da variável `re-trigger` como parte dos parâmetros de consulta.

**Formato da API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parâmetro | Descrição |
| --- | --- |
| `{RUN_ID}` | A ID de execução que corresponde à execução do fluxo de dados que você deseja repetir. |
| `op` | Uma operação que determina a ação a ser executada. Para repetir uma execução de fluxo de dados com falha, você deve especificar `re-trigger` como sua operação. |

**Solicitação**

A solicitação a seguir tenta executar o fluxo de dados para a ID de execução `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**Resposta**

Uma resposta bem-sucedida retorna uma ID de execução de fluxo recém-criada e a versão de tag correspondente.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
