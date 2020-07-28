---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---


# Explore um sistema de armazenamento em nuvem usando a [!DNL Flow Service] API

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Este tutorial usa a [!DNL Flow Service] API para explorar um sistema de armazenamento em nuvem de terceiros.

## Introdução

Este guia exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Caixas de proteção](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um sistema de armazenamento em nuvem usando a [!DNL Flow Service] API.

### Obter uma conexão básica

Para explorar um armazenamento em nuvem de terceiros usando [!DNL Platform] APIs, é necessário ter uma ID de conexão básica válida. Se você ainda não tiver uma conexão básica para o armazenamento com o qual deseja trabalhar, poderá criar uma através dos seguintes tutoriais:

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Armazenamento Gen2 do Azure Data Lake](../create/cloud-storage/adls-gen2.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Explore seu armazenamento em nuvem

Usando a conexão básica para seu armazenamento em nuvem, você pode explorar arquivos e diretórios executando solicitações de GET. Ao executar solicitações de GET para explorar seu armazenamento em nuvem, você deve incluir os parâmetros de query listados na tabela abaixo:

| Parâmetro | Descrição |
| --------- | ----------- |
| `objectType` | O tipo de objeto que você deseja explorar. Defina esse valor como: <ul><li>`folder`: Explorar um diretório específico</li><li>`root`: Explore o diretório raiz.</li></ul> |
| `object` | Esse parâmetro é necessário somente ao exibir um diretório específico. Seu valor representa o caminho do diretório que você deseja explorar. |

Use a chamada a seguir para localizar o caminho do arquivo que deseja trazer para [!DNL Platform]:

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de uma conexão básica de armazenamentos na nuvem. |
| `{PATH}` | O caminho de um diretório. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de arquivos e pastas encontrados no diretório consultado. Anote a `path` propriedade do arquivo que deseja carregar, pois é necessário fornecê-lo na próxima etapa para inspecionar sua estrutura.

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## Inspect a estrutura de um arquivo

Para inspecionar a estrutura do arquivo de dados do seu armazenamento em nuvem, execute uma solicitação de GET enquanto fornece o caminho do arquivo como um parâmetro de query.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de uma conexão básica de armazenamentos na nuvem. |
| `{FILE_PATH}` | Caminho para um arquivo. |
| `{FILE_TYPE}` | O tipo do arquivo. Os tipos de arquivos suportados incluem:<ul><li>DELIMITADO</code>: Valor separado por delimitadores. Os arquivos DSV devem ser separados por vírgulas.</li><li>JSON</code>: Notação do objeto JavaScript. Os arquivos JSON devem ser compatíveis com XDM</li><li>PARQUET</code>: Apache Parquet. Os arquivos de parâmetro devem ser compatíveis com XDM.</li></ul> |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a estrutura do arquivo consultado, incluindo nomes de tabela e tipos de dados.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## Próximas etapas

Ao seguir este tutorial, você explorou seu sistema de armazenamento em nuvem, encontrou o caminho do arquivo que deseja inserir [!DNL Platform]e visualizou sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados do seu armazenamento em nuvem e trazê-los para o Platform](../collect/cloud-storage.md).