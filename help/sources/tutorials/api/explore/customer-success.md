---
keywords: Experience Platform, home, tópicos populares, cs, CS, sistema de sucesso do cliente
solution: Experience Platform
title: Explorar um sistema de sucesso do cliente usando a API do Serviço de fluxo
topic-legacy: overview
description: Este tutorial usa a API do Serviço de fluxo para explorar sistemas de CSS (Customer Success).
exl-id: 453be69d-3d72-4987-81cd-67fa3be7ee59
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# Explore um sistema bem-sucedido do cliente usando o [!DNL Flow Service] API

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa o [!DNL Flow Service] API para explorar os sistemas de CSS (Customer Success, sucesso do cliente).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um sistema CS usando o [!DNL Flow Service] API.

### Obter uma conexão base

Para explorar seu sistema de CS usando [!DNL Platform] APIs, você deve possuir uma ID de conexão base válida. Se ainda não tiver uma conexão básica para o sistema CS com o qual deseja trabalhar, crie uma por meio dos seguintes tutoriais:

* [Salesforce Service Cloud](../create/customer-success/salesforce-service-cloud.md)
* [ServiceNow](../create/customer-success/servicenow.md)

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Explorar suas tabelas de dados

Usando a conexão básica para seu sistema CS, você pode explorar suas tabelas de dados executando solicitações GET. Use a chamada a seguir para encontrar o caminho da tabela na qual você deseja inspecionar ou assimilar [!DNL Platform].

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de uma conexão básica do CS. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de tabelas do seu sistema CS. Encontre a tabela que deseja trazer [!DNL Platform] e toma nota da sua `path` , conforme você precisará fornecê-la na próxima etapa para inspecionar sua estrutura.

```json
[
    {
        "type": "table",
        "name": "Accepted Event Relation",
        "path": "AcceptedEventRelation",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account",
        "path": "Account",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Change Event",
        "path": "AccountChangeEvent",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Clean Info",
        "path": "AccountCleanInfo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect a estrutura de uma tabela

Para inspecionar a estrutura de uma tabela do seu sistema CS, execute uma solicitação de GET enquanto especifica o caminho de uma tabela como um parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de uma conexão básica do CS. |
| `{TABLE_PATH}` | O caminho de uma tabela. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=table&object=test1.Mytable' \
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
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## Próximas etapas

Ao seguir este tutorial, você explorou seu sistema CS e encontrou o caminho da tabela na qual deseja assimilar [!DNL Platform]e obteve informações sobre a sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados do sistema CS e trazê-los para a plataforma](../collect/customer-success.md).
