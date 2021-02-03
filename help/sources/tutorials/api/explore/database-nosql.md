---
keywords: Experience Platform;home;popular topics;banco de dados de terceiros;serviço de fluxo de banco de dados
solution: Experience Platform
title: Explore um banco de dados usando a API de Serviço de Fluxo
topic: overview
description: Este tutorial usa a API de Serviço de Fluxo para explorar o conteúdo e a estrutura de arquivos de um banco de dados de terceiros.
translation-type: tm+mt
source-git-commit: ddf5be2f30bc347a881bdcbc6b880f087c03e263
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---


# Explore um banco de dados usando a API [!DNL Flow Service]

Este tutorial usa a API [!DNL Flow Service] para explorar o conteúdo e a estrutura de arquivos de um banco de dados de terceiros.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../home.md):  [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Caixas de proteção](../../../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um banco de dados de terceiros usando a API [!DNL Flow Service].

### Reunir credenciais obrigatórias

Este tutorial requer uma conexão válida com o banco de dados de terceiros do qual você deseja assimilar dados. Uma conexão válida envolve a ID de especificação de conexão e a ID de conexão do banco de dados. Mais informações sobre como criar uma conexão de banco de dados e recuperar esses valores podem ser encontradas na [visão geral dos conectores de origem](./../../../home.md#database).

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API E[!DNL xperience Platform], como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Explore suas tabelas de dados

Usando a ID de conexão para seu banco de dados, você pode explorar suas tabelas de dados realizando solicitações de GET. Use a chamada a seguir para localizar o caminho da tabela que deseja inspecionar ou assimilar em [!DNL Platform].

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de tabelas do banco de dados. Encontre a tabela que deseja trazer para [!DNL Platform] e anote sua propriedade `path`, conforme necessário na próxima etapa para inspecionar sua estrutura.

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

## Inspect a estrutura de uma tabela

Para inspecionar a estrutura de uma tabela do banco de dados, execute uma solicitação de GET enquanto especifica o caminho de uma tabela como um parâmetro de query.

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

Ao seguir este tutorial, você explorou seu banco de dados, encontrou o caminho da tabela que deseja assimilar em [!DNL Platform] e obteve informações sobre sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados de seu banco de dados e trazê-los para o Platform](../collect/database-nosql.md).