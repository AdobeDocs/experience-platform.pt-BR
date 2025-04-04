---
keywords: Experience Platform;home;tópicos populares;banco de dados de terceiros;serviço de fluxo de banco de dados
solution: Experience Platform
title: Explorar um banco de dados usando a API do serviço de fluxo
description: Este tutorial usa a API de serviço de fluxo para explorar o conteúdo e a estrutura de arquivos de um banco de dados de terceiros.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 10%

---

# Explorar um banco de dados usando a API [!DNL Flow Service]

Este tutorial usa a API [!DNL Flow Service] para explorar o conteúdo e a estrutura de arquivos de um banco de dados de terceiros.

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um banco de dados de terceiros usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Este tutorial requer uma conexão válida com o banco de dados de terceiros do qual você deseja assimilar dados. Uma conexão válida envolve a ID da especificação da conexão do banco de dados e a ID da conexão. Mais informações sobre como criar uma conexão de banco de dados e recuperar esses valores podem ser encontradas na [visão geral dos conectores de origem](./../../../home.md#database).

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API E[!DNL xperience Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Explore suas tabelas de dados

Usando a ID de conexão do banco de dados, você pode explorar as tabelas de dados executando solicitações do GET. Use a chamada a seguir para localizar o caminho da tabela que você deseja inspecionar ou assimilar em [!DNL Experience Platform].

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão da origem do banco de dados. |

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de tabelas do banco de dados. Encontre a tabela que você deseja trazer para [!DNL Experience Platform] e anote sua propriedade `path`, pois você deverá fornecê-la na próxima etapa para inspecionar sua estrutura.

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspecionar a estrutura de uma tabela

Para inspecionar a estrutura de uma tabela do banco de dados, execute uma solicitação GET enquanto especifica o caminho de uma tabela como um parâmetro de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de uma conexão de banco de dados. |
| `{TABLE_PATH}` | O caminho de uma tabela. |

**Solicitação**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
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
                "name": "TestID",
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
            }
        ]
    }
}
```

## Próximas etapas

Seguindo este tutorial, você explorou seu banco de dados, encontrou o caminho da tabela que deseja assimilar em [!DNL Experience Platform] e obteve informações sobre sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados do banco de dados e trazê-los para a Experience Platform](../collect/database-nosql.md).
