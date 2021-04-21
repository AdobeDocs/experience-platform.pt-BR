---
keywords: Experience Platform, home, tópicos populares, armazenamento na nuvem, armazenamento na nuvem
solution: Experience Platform
title: Explore um sistema de armazenamento em alto volume usando a API do Serviço de fluxo
topic-legacy: overview
description: Este tutorial usa a API do Serviço de fluxo para explorar um sistema de armazenamento em nuvem de terceiros.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---

# Explore um sistema de armazenamento em nuvem usando a API [!DNL Flow Service]

Este tutorial usa a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para explorar um sistema de armazenamento em nuvem de terceiros.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um sistema de armazenamento em nuvem usando a API [!DNL Flow Service].

### Obter uma ID de conexão

Para explorar um armazenamento em nuvem de terceiros usando [!DNL Platform] APIs, você deve ter uma ID de conexão válida. Se ainda não tiver uma conexão com o armazenamento com o qual deseja trabalhar, crie uma por meio dos seguintes tutoriais:

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Explore o armazenamento na nuvem

Usando a ID de conexão para o armazenamento em nuvem, você pode explorar arquivos e diretórios executando solicitações do GET. Ao executar solicitações do GET para explorar o armazenamento na nuvem, você deve incluir os parâmetros de consulta listados na tabela abaixo:

| Parâmetro | Descrição |
| --------- | ----------- |
| `objectType` | O tipo de objeto que você deseja explorar. Defina esse valor como: <ul><li>`folder`: Explorar um diretório específico</li><li>`root`: Explore o diretório raiz.</li></ul> |
| `object` | Esse parâmetro é necessário somente ao visualizar um diretório específico. Seu valor representa o caminho do diretório que você deseja explorar. |

Use a chamada a seguir para localizar o caminho do arquivo que deseja trazer para [!DNL Platform]:

**Formato da API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONNECTION_ID}` | A ID de conexão do conector de origem de armazenamento na nuvem. |
| `{PATH}` | O caminho de um diretório. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de arquivos e pastas encontrados no diretório consultado. Anote a propriedade `path` do arquivo que deseja carregar, pois é necessário fornecê-lo na próxima etapa para inspecionar sua estrutura.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect a estrutura de um arquivo

Para inspecionar a estrutura do arquivo de dados do armazenamento em nuvem, execute uma solicitação de GET enquanto fornece o caminho do arquivo e digite como parâmetro de consulta.

Você pode inspecionar a estrutura de um arquivo de dados da sua fonte de armazenamento em nuvem executando uma solicitação do GET enquanto fornece o caminho e o tipo do arquivo. Também é possível inspecionar diferentes tipos de arquivos, como CSV, TSV ou JSON compactado e arquivos delimitados, especificando seus tipos de arquivo como parte dos parâmetros de consulta.

**Formato da API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | A ID de conexão do conector de origem de armazenamento da nuvem. |
| `{FILE_PATH}` | O caminho para o arquivo que você deseja inspecionar. |
| `{FILE_TYPE}` | O tipo do arquivo. Os tipos de arquivos suportados incluem:<ul><li>DELIMITADO</code>: Valor separado por delimitadores. Os arquivos DSV devem ser separados por vírgulas.</li><li>JSON</code>: Notação de objeto JavaScript. Os arquivos JSON devem ser compatíveis com XDM</li><li>PARQUET</code>: Apache Parquet. Os arquivos de parâmetro devem ser compatíveis com XDM.</li></ul> |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais que podem ser usados para filtrar resultados. Consulte a seção em [parâmetros de consulta](#query) para obter mais informações. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
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

## Uso de parâmetros de consulta {#query}

A [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) suporta o uso de parâmetros de consulta para visualizar e inspecionar tipos de arquivos diferentes.

| Parâmetro | Descrição |
| --------- | ----------- |
| `columnDelimiter` | O valor de caractere único especificado como delimitador de coluna para inspecionar arquivos CSV ou TSV. Se o parâmetro não for fornecido, o valor assumirá como padrão uma vírgula `(,)`. |
| `compressionType` | Um parâmetro de consulta obrigatório para a visualização de um arquivo compactado delimitado ou JSON. Os arquivos compactados compatíveis são: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## Próximas etapas

Ao seguir este tutorial, você explorou seu sistema de armazenamento em nuvem, encontrou o caminho do arquivo que deseja trazer para [!DNL Platform] e visualizou sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados do armazenamento na nuvem e trazê-los para a Platform](../collect/cloud-storage.md).
