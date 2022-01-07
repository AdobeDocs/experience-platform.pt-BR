---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, excluir contas de destino, excluir, api
solution: Experience Platform
title: Excluir uma conta de destino usando a API de Serviço de Fluxo
type: Tutorial
description: Saiba como excluir uma conta de destino usando a API de Serviço de Fluxo.
source-git-commit: df89f8ce8050b26068e0ab7aa01f1c964f5d2422
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---

# Excluir uma conta de destino usando a API de Serviço de Fluxo

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

Antes de ativar os dados, é necessário se conectar ao destino primeiro configurando uma conta de destino. Este tutorial aborda as etapas para excluir contas de destino que não são mais necessárias usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Atualmente, a exclusão de contas de destino é compatível somente na API de Serviço de Fluxo. As contas de destino não podem ser excluídas usando a interface de usuário do Experience Platform.

## Introdução {#get-started}

Este tutorial requer uma ID de conexão válida. A ID de conexão representa a conexão da conta com o destino. Se você não tiver uma ID de conexão válida, selecione o destino escolhido na [catálogo de destinos](../catalog/overview.md) e siga as etapas descritas em [conectar-se ao destino](../ui/connect-destination.md) antes de tentar este tutorial.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para excluir com êxito uma conta de destino usando o [!DNL Flow Service] API.

### Lendo exemplos de chamadas de API {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários {#gather-values-for-required-headers}

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se a variável `x-sandbox-name` não for especificado, as solicitações serão resolvidas na variável `prod` sandbox.

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Encontre a ID de conexão da conta de destino que deseja excluir {#find-connection-id}

>[!NOTE]
>Este tutorial usa o [Destino da aeronave](../catalog/mobile-engagement/airship-attributes.md) como exemplo, mas as etapas descritas se aplicam a qualquer uma das [destinos disponíveis](../catalog/overview.md).

A primeira etapa na exclusão de uma conta de destino é descobrir a ID da conexão que corresponde à conta de destino que você deseja excluir.

Na interface do usuário do Experience Platform, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Contas]** e selecione a conta que deseja excluir selecionando o número na **[!UICONTROL Destinos]** coluna.

![Selecione a conta de destino a ser excluída](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Em seguida, é possível recuperar a ID da conexão da conta de destino do URL no navegador.

![Recuperar ID de conexão do URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "imsOrgId": "{IMS_ORG}",
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

## Eliminar ligação {#delete-connection}

>[!IMPORTANT]
>
>Antes de excluir a conta de destino, você deve excluir todos os fluxos de dados existentes para a conta de destino.
>Para excluir fluxos de dados existentes, consulte as páginas abaixo:
>* [Usar a interface do usuário do Experience Platform](../ui/delete-destinations.md) eliminar fluxos de dados existentes;
>* [Usar a API do Serviço de Fluxo](delete-destination-dataflow.md) para excluir fluxos de dados existentes.


Depois de ter uma ID de conexão e garantir que nenhum fluxo de dados exista para a conta de destino, execute uma solicitação de DELETE para a [!DNL Flow Service] API.

**Formato da API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O único `id` para a conexão que deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco. Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para a conexão. A API retornará um erro HTTP 404 (Not Found), indicando que a conta de destino foi excluída.

## Tratamento de erros da API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais da mensagem de erro da API de Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso a variável [!DNL Flow Service] API para excluir contas de destino existentes.
