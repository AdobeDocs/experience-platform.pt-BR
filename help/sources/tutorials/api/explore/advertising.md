---
keywords: Experience Platform, home, tópicos populares, sistema de publicidade, sistema de publicidade
solution: Experience Platform
title: Explorar um sistema de publicidade usando a API do serviço de fluxo
topic-legacy: overview
description: O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis. Este tutorial usa a API do Serviço de fluxo para explorar sistemas de publicidade.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 9938b0bb939dc7bab9d8e02bd58735360fc883fa
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---

# Explore um sistema de publicidade usando o [!DNL Flow Service] API

Com uma conexão básica criada, agora é possível usar a ID de conexão base exclusiva para navegar e explorar a estrutura de dados e o conteúdo de sua fonte. Isso permite identificar os itens específicos e seus respectivos tipos de dados e formatos, antes de criar um fluxo de dados e trazê-los para o Adobe Experience Platform.

Este tutorial usa o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) explorar sistemas de publicidade.

## Introdução

>[!IMPORTANT]
>
>Este tutorial requer que você tenha a ID de conexão básica exclusiva para sua fonte de publicidade. Caso não tenha essa ID, consulte o tutorial em [conectar uma fonte de publicidade à Platform](../../api/create/advertising/ads.md) tutorial.

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um sistema de publicidade usando o [!DNL Flow Service] API.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../landing/api-guide.md).

## Explorar suas tabelas de dados

Usando a conexão básica para seu sistema de publicidade, você pode explorar suas tabelas de dados executando solicitações GET. Use a chamada a seguir para encontrar o caminho da tabela na qual você deseja inspecionar ou assimilar [!DNL Platform].

**Formato da API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID da conexão básica para seu sistema de publicidade. |

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida é uma matriz de tabelas da para seu sistema de publicidade. Encontre a tabela que deseja trazer [!DNL Platform] e toma nota da sua `path` , conforme você precisará fornecê-la na próxima etapa para inspecionar sua estrutura.

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect a estrutura de uma tabela

Para inspecionar a estrutura de uma tabela em seu sistema de anúncios, execute uma solicitação de GET enquanto especifica o caminho de uma tabela como um parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão do seu sistema de publicidade. |
| `{TABLE_PATH}` | O caminho de uma tabela em seu sistema de publicidade. |

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura de uma tabela. Os detalhes relativos a cada coluna da tabela estão localizados em elementos do `columns` matriz.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## Próximas etapas

Ao seguir este tutorial, você explorou seu sistema de publicidade e encontrou o caminho da tabela que deseja trazer para [!DNL Platform]e obteve informações sobre a sua estrutura. Você pode usar essas informações no próximo tutorial para [colete dados de seu sistema de publicidade e traga-os para a Platform](../collect/advertising.md).
