---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, API, api, excluir, excluir fluxos de dados de destino
solution: Experience Platform
title: Excluir um fluxo de dados de destino usando a API de Serviço de Fluxo
type: Tutorial
description: Saiba como excluir fluxos de dados para destinos de lote e fluxo por meio da API de Serviço de Fluxo.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# Excluir um fluxo de dados de destino usando a API de Serviço de Fluxo

Você pode excluir fluxos de dados que contenham erros ou que se tornaram obsoletos usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Este tutorial aborda as etapas para excluir fluxos de dados para destinos de lote e streaming usando [!DNL Flow Service].

## Introdução {#get-started}

Este tutorial requer uma ID de fluxo válida. Se você não tiver uma ID de fluxo válida, selecione o destino escolhido na [catálogo de destinos](../catalog/overview.md) e siga as etapas descritas em [conectar-se ao destino](../ui/connect-destination.md) e [ativar dados](../ui/activation-overview.md) antes de tentar este tutorial.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para excluir com êxito um fluxo de dados usando o [!DNL Flow Service] API.

### Lendo exemplos de chamadas de API {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários {#gather-values-for-required-headers}

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se a variável `x-sandbox-name` não for especificado, as solicitações serão resolvidas na variável `prod` sandbox.

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Excluir um fluxo de dados de destino {#delete-destination-dataflow}

Com uma ID de fluxo existente, é possível excluir um fluxo de dados de destino executando uma solicitação de DELETE para a [!DNL Flow Service] API.

**Formato da API**

```http
DELETE /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O único `id` para o fluxo de dados de destino que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 (Sem conteúdo) e um corpo em branco. É possível confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o fluxo de dados. A API retornará um erro HTTP 404 (Not Found), indicando que o fluxo de dados foi excluído.

## Tratamento de erros da API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais da mensagem de erro da API de Experience Platform. Consulte [Códigos de status da API](/help/landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](/help/landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma para obter mais informações sobre a interpretação das respostas dos erros.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você usou com sucesso a variável [!DNL Flow Service] API para excluir um fluxo de dados existente para um destino.

Para obter etapas sobre como executar essas operações usando a interface do usuário, consulte o tutorial em [exclusão de fluxos de dados na interface do usuário](../ui/delete-destinations.md).

Pode agora prosseguir e [excluir contas de destino](/help/destinations/api/delete-destination-account.md) usando o [!DNL Flow Service] API.
