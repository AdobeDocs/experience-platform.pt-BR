---
keywords: Experience Platform;página inicial;tópicos populares;serviço de fluxo;API;api;excluir;excluir fluxos de dados de destino
solution: Experience Platform
title: Excluir um fluxo de dados de destino usando a API do Serviço de fluxo
type: Tutorial
description: Saiba como excluir fluxos de dados para destinos em lote e de transmissão usando a API de serviço de fluxo.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 14%

---

# Excluir um fluxo de dados de destino usando a API do Serviço de fluxo

Você pode excluir fluxos de dados que contêm erros ou que se tornaram obsoletos usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Este tutorial aborda as etapas para excluir fluxos de dados para destinos em lote e de fluxo usando [!DNL Flow Service].

## Introdução {#get-started}

Este tutorial requer que você tenha uma ID de fluxo válida. Se você não tiver uma ID de fluxo válida, selecione seu destino escolhido no [catálogo de destinos](../catalog/overview.md) e siga as etapas descritas para [conectar-se ao destino](../ui/connect-destination.md) e [ativar dados](../ui/activation-overview.md) antes de tentar este tutorial.

Este tutorial também requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para excluir com êxito um fluxo de dados usando a API [!DNL Flow Service].

### Leitura de chamadas de API de amostra {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários {#gather-values-for-required-headers}

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se o cabeçalho `x-sandbox-name` não for especificado, as solicitações serão resolvidas na sandbox `prod`.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Excluir um fluxo de dados de destino {#delete-destination-dataflow}

Com uma ID de fluxo existente, é possível excluir um fluxo de dados de destino executando uma solicitação DELETE para a API [!DNL Flow Service].

**Formato da API**

```http
DELETE /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O valor `id` exclusivo do fluxo de dados de destino que você deseja excluir. |

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

Uma resposta bem-sucedida retorna o status HTTP 202 (Sem conteúdo) e um corpo em branco. Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o fluxo de dados. A API retornará um erro HTTP 404 (Não encontrado), indicando que o fluxo de dados foi excluído.

## Manipulação de erros de API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](/help/landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](/help/landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform para obter mais informações sobre como interpretar respostas de erro.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você usou com êxito a API [!DNL Flow Service] para excluir um fluxo de dados existente para um destino.

Para obter etapas sobre como executar essas operações usando a interface do usuário, consulte o tutorial em [exclusão de fluxos de dados na interface](../ui/delete-destinations.md).

Agora você pode continuar e [excluir contas de destino](/help/destinations/api/delete-destination-account.md) usando a API [!DNL Flow Service].
