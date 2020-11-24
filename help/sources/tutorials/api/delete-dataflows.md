---
keywords: Experience Platform;home;popular topics;flow service;API;api;delete;delete dataflows
solution: Experience Platform
title: Excluir um fluxo de dados usando a API de Serviço de Fluxo
topic: overview
type: Tutorial
description: Este tutorial aborda as etapas para excluir um fluxo de dados usando a API de Serviço de Fluxo.
translation-type: tm+mt
source-git-commit: ae3e64a5f9a82c0efe3cffeb6d4d425ae2e72bda
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# Excluir um fluxo de dados usando a API de Serviço de Fluxo

Este tutorial aborda as etapas para excluir os fluxos de dados feitos com fontes de lote e streaming usando o [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este tutorial requer que você tenha uma ID de fluxo válida. Se você não tiver uma ID de fluxo válida, selecione seu conector de opção na visão geral [das](../../home.md) fontes e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também exige que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para excluir com êxito um fluxo de dados usando a [!DNL Flow Service] API.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Excluir um fluxo de dados

Com uma ID de fluxo existente, é possível excluir um fluxo de dados executando uma solicitação de DELETE para a [!DNL Flow Service] API.

**Formato da API**

```http
DELETE /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O `id` valor exclusivo do fluxo de dados que você deseja excluir. |

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

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco. Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o fluxo de dados. A API retornará um erro HTTP 404 (Não encontrado), indicando que o fluxo de dados foi excluído.

## Próximas etapas

Ao seguir este tutorial, você usou com êxito a API [!DNL Flow Service] para excluir um fluxo de dados existente.

Para obter etapas sobre como executar essas operações usando a interface do usuário, consulte o tutorial sobre como [excluir fluxos de dados na interface do usuário](../../tutorials/ui/delete.md)
