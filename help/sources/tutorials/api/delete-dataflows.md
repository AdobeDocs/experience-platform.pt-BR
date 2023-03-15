---
keywords: Experience Platform;início;tópicos populares;serviço de fluxo;API;api;excluir;excluir fluxos de dados
solution: Experience Platform
title: Excluir um fluxo de dados usando a API do serviço de fluxo
type: Tutorial
description: Saiba como excluir fluxos de dados em lote e de transmissão usando a API do serviço de fluxo.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# Excluir um fluxo de dados usando a API do Serviço de fluxo

É possível excluir fluxos de dados em lote e de transmissão que contenham erros ou que se tenham tornado obsoletos usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Este tutorial aborda as etapas para excluir fluxos de dados feitas com fontes em lote e de transmissão usando [!DNL Flow Service].

## Introdução

Este tutorial requer que você tenha uma ID de fluxo válida. Se você não tiver um ID de fluxo válido, selecione o conector de sua escolha no [visão geral das origens](../../home.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../landing/api-guide.md).

## Excluir um fluxo de dados

Com uma ID de fluxo existente, é possível excluir um fluxo de dados executando uma solicitação DELETE para [!DNL Flow Service] API.

**Formato da API**

```http
DELETE /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O único `id` para o fluxo de dados que deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco. Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o fluxo de dados. A API retornará um erro HTTP 404 (Não encontrado), indicando que o fluxo de dados foi excluído.

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o [!DNL Flow Service] API para excluir um fluxo de dados existente.

Para obter etapas sobre como executar essas operações usando a interface do usuário, consulte o tutorial em [exclusão de fluxos de dados na interface](../../tutorials/ui/delete.md)
