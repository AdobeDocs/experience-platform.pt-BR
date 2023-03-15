---
keywords: Experience Platform;página inicial;tópicos populares;serviço de fluxo;
title: Repetir Execuções de Fluxo de Dados com Falha
description: Este tutorial aborda etapas sobre como tentar novamente execuções de fluxo de dados com falha usando a API do serviço de fluxo
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---

# Tentar novamente execuções de fluxo de dados com falha

>[!IMPORTANT]
>
>O suporte para novas tentativas de execuções de fluxo de dados com falha está disponível para fontes em lote. Você só pode repetir execuções de fluxo de dados que falharam.

Este tutorial aborda etapas sobre como tentar novamente execuções de fluxo de dados com falha usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../landing/api-guide.md).

## Tentar novamente uma execução de fluxo de dados com falha

Para tentar executar novamente um fluxo de dados com falha, faça uma solicitação POST ao `/runs` ao fornecer a ID de execução do fluxo de dados e a variável `re-trigger` como parte dos parâmetros de consulta.

**Formato da API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parâmetro | Descrição |
| --- | --- |
| `{RUN_ID}` | A ID de execução que corresponde à execução do fluxo de dados que você deseja tentar novamente. |
| `op` | Uma operação que determina a ação a ser executada. Para repetir uma execução com falha do fluxo de dados, é necessário especificar `re-trigger` como sua operação. |

**Solicitação**

A solicitação a seguir tenta novamente a execução do fluxo de dados para a ID de execução `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

Uma resposta bem-sucedida retorna uma ID de execução de fluxo recém-criada e sua versão etag correspondente.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
