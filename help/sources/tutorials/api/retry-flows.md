---
title: Repetir Execuções de Fluxo de Dados com Falha
description: Saiba como repetir execuções de fluxo de dados com falha usando a API do Serviço de fluxo.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---

# Tentar novamente execuções de fluxo de dados com falha

>[!IMPORTANT]
>
>O suporte para novas tentativas de execuções de fluxo de dados com falha está disponível para fontes em lote. Você só pode repetir execuções de fluxo de dados que falharam.

Este tutorial aborda etapas sobre como tentar novamente execuções de fluxo de dados com falha usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam um único [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

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

>[!NOTE]
>
>Você pode usar o `re-trigger` a operação para repetir execuções de fluxo de dados bem-sucedidas também, considerando que a execução bem-sucedida do fluxo de dados tem zero registros assimilados.

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
