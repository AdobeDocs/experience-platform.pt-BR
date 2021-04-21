---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, API, api, excluir, excluir fluxos de dados
solution: Experience Platform
title: Excluir um fluxo de dados usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como excluir fluxos de dados de lote e fluxo usando a API do Serviço de fluxo.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Excluir um fluxo de dados usando a API do Serviço de fluxo

Você pode excluir fluxos de dados em lote e de fluxo que contenham erros ou que se tornaram obsoletos usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

Este tutorial aborda as etapas para excluir fluxos de dados feitos com fontes em lote e de transmissão usando [!DNL Flow Service].

## Introdução

Este tutorial requer uma ID de fluxo válida. Se você não tiver uma ID de fluxo válida, selecione o conector de escolha na [visão geral das fontes](../../home.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para excluir com êxito um fluxo de dados usando a API [!DNL Flow Service].

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Excluir um fluxo de dados

Com uma ID de fluxo existente, é possível excluir um fluxo de dados executando uma solicitação de DELETE para a API [!DNL Flow Service].

**Formato da API**

```http
DELETE /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O valor exclusivo `id` para o fluxo de dados que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco. É possível confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o fluxo de dados. A API retornará um erro HTTP 404 (Not Found), indicando que o fluxo de dados foi excluído.

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso a API [!DNL Flow Service] para excluir um fluxo de dados existente.

Para obter etapas sobre como executar essas operações usando a interface do usuário, consulte o tutorial em [excluir fluxos de dados na interface do usuário](../../tutorials/ui/delete.md)
