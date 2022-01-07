---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, excluir contas, excluir, api
solution: Experience Platform
title: Excluir uma conta usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como excluir uma conta usando a API do Serviço de fluxo.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 609f7a5de51840fe657ca72df99c90da56c8f466
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# Excluir uma conta usando a API do Serviço de Fluxo

É possível excluir contas de origem que contenham erros ou que se tornaram obsoletas usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Consulte o tutorial a seguir para obter etapas sobre como excluir uma conta usando a API.

## Introdução

Este tutorial requer uma ID de conexão válida. Se você não tiver uma ID de conexão válida, selecione o conector escolhido na [visão geral das fontes](../../home.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).

## Excluir conta

>[!TIP]
>
>Antes de excluir a conta de origem, primeiro exclua qualquer fluxo de dados existente associado à conta de origem. Para excluir fluxos de dados existentes, consulte o tutorial em [exclusão de fluxos de dados de origens](./delete-dataflows.md).

Para excluir uma conta, faça uma solicitação de DELETE para o [!DNL Flow Service] API ao fornecer a ID de conexão básica que corresponde à conta que você deseja excluir.

**Formato da API**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica da conta de origem que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
  'https://platform-int.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para a conexão.

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso a variável [!DNL Flow Service] API para excluir contas existentes.

Para obter etapas sobre como executar essas operações usando a interface do usuário, consulte o tutorial em [exclusão de contas na interface do usuário](../../tutorials/ui/delete-accounts.md).
