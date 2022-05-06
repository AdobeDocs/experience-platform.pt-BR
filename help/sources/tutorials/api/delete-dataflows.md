---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, API, api, excluir, excluir fluxos de dados
solution: Experience Platform
title: Excluir um fluxo de dados usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como excluir fluxos de dados de lote e fluxo usando a API do Serviço de fluxo.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# Excluir um fluxo de dados usando a API do Serviço de fluxo

Você pode excluir fluxos de dados de lote e fluxo que contenham erros ou que se tornaram obsoletos usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Este tutorial aborda as etapas para excluir fluxos de dados feitos com fontes de lote e fluxo contínuo usando [!DNL Flow Service].

## Introdução

Este tutorial requer uma ID de fluxo válida. Se você não tiver uma ID de fluxo válida, selecione o conector escolhido na [visão geral das fontes](../../home.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).

## Excluir um fluxo de dados

Com uma ID de fluxo existente, é possível excluir um fluxo de dados executando uma solicitação de DELETE para a [!DNL Flow Service] API.

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

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco. É possível confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o fluxo de dados. A API retornará um erro HTTP 404 (Not Found), indicando que o fluxo de dados foi excluído.

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso a variável [!DNL Flow Service] API para excluir um fluxo de dados existente.

Para obter etapas sobre como executar essas operações usando a interface do usuário, consulte o tutorial em [exclusão de fluxos de dados na interface do usuário](../../tutorials/ui/delete.md)
