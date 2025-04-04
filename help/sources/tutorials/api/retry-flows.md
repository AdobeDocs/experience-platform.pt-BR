---
title: Repetir Execuções de Fluxo de Dados com Falha
description: Saiba como repetir execuções de fluxo de dados com falha usando a API do Serviço de fluxo.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# Tentar novamente execuções de fluxo de dados com falha

>[!IMPORTANT]
>
>O suporte para novas tentativas de execuções de fluxo de dados com falha está disponível para fontes em lote. Você só pode repetir execuções de fluxo de dados que falharam.

Este tutorial aborda etapas sobre como repetir execuções de fluxo de dados com falha usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../landing/api-guide.md).

## Tentar novamente uma execução de fluxo de dados com falha

Para repetir uma execução com falha de fluxo de dados, faça uma solicitação POST para o ponto de extremidade `/runs` ao fornecer a ID de execução do fluxo de dados e a operação `re-trigger` como parte dos parâmetros de consulta.

**Formato da API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parâmetro | Descrição |
| --- | --- |
| `{RUN_ID}` | A ID de execução que corresponde à execução do fluxo de dados que você deseja tentar novamente. |
| `op` | Uma operação que determina a ação a ser executada. Para repetir uma execução de fluxo de dados com falha, você deve especificar `re-trigger` como a operação. |

**Solicitação**

>[!NOTE]
>
>Você também pode usar a operação `re-trigger` para repetir execuções de fluxo de dados bem-sucedidas, considerando que a execução bem-sucedida do fluxo de dados não tem nenhum registro assimilado.

A solicitação a seguir repete a execução do fluxo de dados para a ID de execução `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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
