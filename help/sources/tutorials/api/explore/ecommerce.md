---
keywords: Experience Platform;home;popular topics;ecommerce;eCommerce
solution: Experience Platform
title: Explore uma conexão de comércio eletrônico usando a API de serviços de fluxo
topic: overview
description: Este tutorial usa a API de Serviço de Fluxo para explorar conexões de eCommerce.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# Explore uma conexão de comércio eletrônico usando a API [!DNL Flow Service]

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para explorar uma conexão **[!UICONTROL eCommerce]** de terceiros.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Sources]](../../../home.md):  [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a uma conexão **[!UICONTROL eCommerce]** usando a API [!DNL Flow Service].

### Obter uma ID de conexão

Para explorar sua conexão **[!UICONTROL eCommerce]** usando [!DNL Platform] APIs, você deve possuir uma ID de conexão válida. Se você ainda não tiver uma conexão para a conexão **[!UICONTROL eCommerce]** com a qual deseja trabalhar, poderá criar uma através do seguinte tutorial:

* [Shopify](../create/ecommerce/shopify.md)

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Explore suas tabelas de dados

Usando sua ID de conexão **[!UICONTROL eCommerce]**, você pode explorar suas tabelas de dados realizando solicitações de GET. Use a chamada a seguir para localizar o caminho da tabela que deseja inspecionar ou assimilar em [!DNL Platform].

**Formato da API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONNECTION_ID}` | Sua ID de conexão **[!UICONTROL eCommerce]**. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de tabelas da sua conexão **[!UICONTROL eCommerce]**. Encontre a tabela que deseja trazer para [!DNL Platform] e anote sua propriedade `path`, conforme necessário na próxima etapa para inspecionar sua estrutura.

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

Para inspecionar a estrutura de uma tabela da conexão **[!UICONTROL eCommerce]**, execute uma solicitação de GET enquanto especifica o caminho de uma tabela dentro de um parâmetro de query `object`.

**Formato da API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | A ID de conexão da sua conexão **[!UICONTROL eCommerce]**. |
| `{TABLE_PATH}` | O caminho de uma tabela dentro da sua conexão **[!UICONTROL eCommerce]**. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura da tabela especificada. Os detalhes referentes a cada coluna da tabela estão localizados em elementos da matriz `columns`.

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

Ao seguir este tutorial, você explorou sua conexão **[!UICONTROL eCommerce]**, encontrou o caminho da tabela que deseja assimilar em [!DNL Platform] e obteve informações sobre sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados de comércio eletrônico e trazê-los para a Plataforma](../collect/ecommerce.md).
