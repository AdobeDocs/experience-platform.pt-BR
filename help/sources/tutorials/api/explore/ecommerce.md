---
keywords: Experience Platform, home, tópicos populares, comércio eletrônico
solution: Experience Platform
title: Explorar uma conexão de comércio eletrônico usando a API do serviço de fluxo
topic-legacy: overview
description: Este tutorial usa a API do Serviço de fluxo para explorar conexões de eCommerce.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# Explore uma conexão de comércio eletrônico usando o [!DNL Flow Service] API

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa o [!DNL Flow Service] API para explorar terceiros **[!UICONTROL comércio eletrônico]** conexão.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um **[!UICONTROL comércio eletrônico]** conexão usando o [!DNL Flow Service] API.

### Obter uma ID de conexão

Para explorar as **[!UICONTROL comércio eletrônico]** conexão usando [!DNL Platform] APIs, você deve possuir uma ID de conexão válida. Se você ainda não tiver uma conexão para o **[!UICONTROL comércio eletrônico]** para trabalhar com a, crie uma por meio do seguinte tutorial:

* [Shopify](../create/ecommerce/shopify.md)

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Explorar suas tabelas de dados

Usar seu **[!UICONTROL comércio eletrônico]** ID da conexão, você pode explorar suas tabelas de dados executando solicitações GET. Use a chamada a seguir para encontrar o caminho da tabela na qual você deseja inspecionar ou assimilar [!DNL Platform].

**Formato da API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONNECTION_ID}` | Seu **[!UICONTROL comércio eletrônico]** ID da conexão. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de tabelas de seus **[!UICONTROL comércio eletrônico]** conexão. Encontre a tabela que deseja trazer [!DNL Platform] e toma nota da sua `path` , conforme você precisará fornecê-la na próxima etapa para inspecionar sua estrutura.

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect a estrutura de uma tabela

Para inspecionar a estrutura de uma tabela de sua **[!UICONTROL comércio eletrônico]** , execute uma solicitação de GET enquanto especifica o caminho de uma tabela dentro de uma `object` parâmetro de consulta.

**Formato da API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | A ID de conexão do **[!UICONTROL comércio eletrônico]** conexão. |
| `{TABLE_PATH}` | O caminho de uma tabela dentro de seu **[!UICONTROL comércio eletrônico]** conexão. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura da tabela especificada. Os detalhes relativos a cada coluna da tabela estão localizados em elementos do `columns` matriz.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## Próximas etapas

Ao seguir este tutorial, você explorou seu **[!UICONTROL comércio eletrônico]** , foi encontrado o caminho da tabela em que deseja assimilar [!DNL Platform]e obteve informações sobre a sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados do eCommerce e trazê-los para a plataforma](../collect/ecommerce.md).
