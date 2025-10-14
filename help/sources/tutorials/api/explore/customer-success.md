---
keywords: Experience Platform;página inicial;tópicos populares;sistema de sucesso do cliente;;home;popular topics;cs;CS;customer success system
solution: Experience Platform
title: Explore um sistema de sucesso do cliente usando a API do serviço de fluxo
description: Este tutorial usa a API de serviço de fluxo para explorar os sistemas de Sucesso do cliente (CS).
exl-id: 453be69d-3d72-4987-81cd-67fa3be7ee59
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 13%

---

# Explore um sistema de sucesso do cliente usando a API [!DNL Flow Service]

O [!DNL Flow Service] é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e a API RESTful a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a API [!DNL Flow Service] para explorar os sistemas de Sucesso do cliente (CS).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um sistema CS usando a API [!DNL Flow Service].

### Obter uma conexão básica

Para explorar seu sistema CS usando APIs do [!DNL Experience Platform], você deve possuir uma ID de conexão base válida. Se você ainda não tiver uma conexão básica para o sistema CS com o qual deseja trabalhar, crie uma por meio dos seguintes tutoriais:

* [&#x200B; Service Cloud](../create/customer-success/salesforce-service-cloud.md)
* [ServiceNow](../create/customer-success/servicenow.md)

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Explore suas tabelas de dados

Usando a conexão básica para seu sistema CS, você pode explorar suas tabelas de dados executando solicitações do GET. Use a chamada a seguir para localizar o caminho da tabela que você deseja inspecionar ou assimilar em [!DNL Experience Platform].

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de uma conexão base CS. |

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

Uma resposta bem-sucedida retorna uma matriz de tabelas do sistema CS. Encontre a tabela que você deseja trazer para [!DNL Experience Platform] e anote sua propriedade `path`, pois você deverá fornecê-la na próxima etapa para inspecionar sua estrutura.

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

## Inspecionar a estrutura de uma tabela

Para inspecionar a estrutura de uma tabela no sistema CS, execute uma solicitação GET enquanto especifica o caminho de uma tabela como parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de uma conexão base CS. |
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

Uma resposta bem-sucedida retorna a estrutura da tabela especificada. Detalhes sobre cada coluna da tabela estão localizados em elementos da matriz `columns`.

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

Seguindo este tutorial, você explorou seu sistema CS, encontrou o caminho da tabela que deseja assimilar em [!DNL Experience Platform] e obteve informações sobre sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados do seu sistema CS e trazê-los para a Experience Platform](../collect/customer-success.md).
