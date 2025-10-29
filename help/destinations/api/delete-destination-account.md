---
keywords: Experience Platform;página inicial;tópicos populares;serviço de fluxo;excluir contas de destino;excluir;api
solution: Experience Platform
title: Excluir uma conta de destino usando a API de Serviço de Fluxo
type: Tutorial
description: Saiba como excluir uma conta de destino usando a API de serviço de fluxo.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 21%

---

# Excluir uma conta de destino usando a API de Serviço de Fluxo

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

Antes de ativar os dados, você precisa se conectar ao destino configurando primeiro uma conta de destino. Este tutorial aborda as etapas para excluir contas de destino que não são mais necessárias usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>No momento, a exclusão de contas de destino é permitida somente na API de Serviço de Fluxo. As contas de destino não podem ser excluídas usando a interface do usuário do Experience Platform.

## Introdução {#get-started}

Este tutorial requer que você tenha uma ID de conexão válida. A ID de conexão representa a conexão da conta com o destino. Se você não tiver uma ID de conexão válida, selecione seu destino escolhido no [catálogo de destinos](../catalog/overview.md) e siga as etapas descritas para [conectar-se ao destino](../ui/connect-destination.md) antes de tentar este tutorial.

Este tutorial também requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para excluir com êxito uma conta de destino usando a API [!DNL Flow Service].

### Leitura de chamadas de API de amostra {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas da [!DNL Experience Platform].

### Coletar valores para cabeçalhos obrigatórios {#gather-values-for-required-headers}

Para fazer chamadas para APIs da [!DNL Experience Platform], você deve concluir primeiro o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

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

## Localize a ID de conexão da conta de destino que você deseja excluir {#find-connection-id}

>[!NOTE]
>Este tutorial usa o [Destino da aeronave](../catalog/mobile-engagement/airship-attributes.md) como exemplo, mas as etapas descritas se aplicam a qualquer um dos [destinos disponíveis](../catalog/overview.md).

A primeira etapa ao excluir uma conta de destino é descobrir a ID de conexão que corresponde à conta de destino que você deseja excluir.

Na interface do Experience Platform, navegue até **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** e selecione a conta que deseja excluir selecionando o número na coluna **[!UICONTROL Destinations]**.

![Selecione a conta de destino a ser excluída](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Em seguida, você pode recuperar a ID de conexão da conta de destino da URL no navegador.

![Recuperar ID de conexão da URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## Excluir conexão {#delete-connection}

>[!IMPORTANT]
>
>Antes de excluir a conta de destino, você deve excluir todos os fluxos de dados existentes para a conta de destino.
>&#x200B;>Para excluir fluxos de dados existentes, consulte as páginas abaixo:
>
>* [Usar a interface do usuário do Experience Platform](../ui/delete-destinations.md) para excluir fluxos de dados existentes;
>* [Use a API de Serviço de Fluxo](delete-destination-dataflow.md) para excluir fluxos de dados existentes.

Depois de ter uma ID de conexão e verificar se não há fluxos de dados para a conta de destino, execute uma solicitação DELETE para a API [!DNL Flow Service].

**Formato da API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` exclusivo da conexão que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco. Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para a conexão. A API retornará um erro HTTP 404 (Não encontrado), indicando que a conta de destino foi excluída.

## Manipulação de erros de API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas

Ao seguir este tutorial, você usou com êxito a API [!DNL Flow Service] para excluir contas de destino existentes. Para obter mais informações sobre o uso de destinos, consulte a [visão geral sobre destinos](/help/destinations/home.md).