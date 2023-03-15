---
keywords: Experience Platform;página inicial;tópicos populares;serviço de fluxo;excluir contas;excluir;api
solution: Experience Platform
title: Excluir uma conta usando a API do serviço de fluxo
type: Tutorial
description: Saiba como excluir uma conta usando a API do Serviço de fluxo.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# Excluir uma conta usando a API do Serviço de fluxo

Você pode deletar as contas de origem que contêm erros ou que se tornaram obsoletas usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Consulte o tutorial a seguir para obter etapas sobre como excluir uma conta usando a API.

## Introdução

Este tutorial requer que você tenha uma ID de conexão válida. Se você não tiver um ID de conexão válido, selecione o conector de sua escolha no [visão geral das origens](../../home.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../landing/api-guide.md).

## Excluir conta

>[!TIP]
>
>Antes de excluir a conta de origem, primeiro você deve excluir todos os fluxos de dados existentes associados à conta de origem. Para excluir fluxos de dados existentes, consulte o tutorial sobre [exclusão de fluxos de dados de origens](./delete-dataflows.md).

Para excluir uma conta, faça uma solicitação DELETE à [!DNL Flow Service] ao fornecer a ID de conexão básica que corresponde à conta que você deseja excluir.

**Formato da API**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID da conexão básica da conta de origem que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para a conexão.

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o [!DNL Flow Service] API para excluir contas existentes.

Para obter etapas sobre como executar essas operações usando a interface do usuário, consulte o tutorial em [exclusão de contas na interface](../../tutorials/ui/delete-accounts.md).
