---
keywords: Experience Platform;página inicial;tópicos populares;armazenamento na nuvem;armazenamento na nuvem
title: Explorar pastas de armazenamento na nuvem usando a API do serviço de fluxo
description: Este tutorial usa a API de serviço de fluxo para explorar um sistema de armazenamento em nuvem de terceiros.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 4%

---

# Explore suas pastas de armazenamento na nuvem usando a API do [!DNL Flow Service]

Este tutorial fornece etapas sobre como explorar e visualizar a estrutura e o conteúdo do seu armazenamento na nuvem usando a API do [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Para explorar seu armazenamento na nuvem, você já deve ter uma ID de conexão básica válida para uma fonte de armazenamento na nuvem. Se você não tiver essa ID, consulte a [visão geral das fontes](../../../home.md#cloud-storage) para obter uma lista de fontes de armazenamento na nuvem com as quais você pode criar uma conexão base.

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../landing/api-guide.md).

## Explore suas pastas de armazenamento na nuvem

Você pode recuperar informações sobre a estrutura de suas pastas de armazenamento na nuvem fazendo uma solicitação GET para a API [!DNL Flow Service] enquanto fornece a ID de conexão básica de sua origem.

Ao executar solicitações do GET para explorar seu armazenamento na nuvem, você deve incluir os parâmetros de consulta listados na tabela abaixo:

| Parâmetro | Descrição |
| --------- | ----------- |
| `objectType` | O tipo de objeto que você deseja explorar. Defina esse valor como: <ul><li>`folder`: Explorar um diretório específico</li><li>`root`: Explore o diretório raiz.</li></ul> |
| `object` | Esse parâmetro é necessário somente ao visualizar um diretório específico. Seu valor representa o caminho do diretório que você deseja explorar. |


**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parâmetro | Descrição |
| --- | --- |
| `{BASE_CONNECTION_ID}` | A ID de conexão básica da sua fonte de armazenamento na nuvem. |
| `{PATH}` | O caminho de um diretório. |

**Solicitação**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de arquivos e pastas encontrados no diretório consultado. Anote a propriedade `path` do arquivo que deseja carregar, pois você deverá fornecê-la na próxima etapa para inspecionar sua estrutura.

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

## Inspecionar a estrutura de um arquivo

Para inspecionar a estrutura do arquivo de dados do armazenamento na nuvem, execute uma solicitação GET enquanto fornece o caminho e o tipo do arquivo como um parâmetro de consulta.

É possível inspecionar a estrutura de um arquivo de dados da fonte de armazenamento na nuvem executando uma solicitação GET e fornecendo o caminho e o tipo do arquivo. Você também pode inspecionar diferentes tipos de arquivos, como CSV, TSV ou JSON compactado e arquivos delimitados, especificando seus tipos de arquivos como parte dos parâmetros de consulta.

**Formato da API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&fileType=delimited&encoding=ISO-8859-1;
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | A ID de conexão do conector de origem de armazenamento na nuvem. |
| `{FILE_PATH}` | O caminho para o arquivo que você deseja inspecionar. |
| `{FILE_TYPE}` | O tipo do arquivo. Os tipos de arquivos compatíveis incluem:<ul><li><code>DELIMITADO</code>: valor separado por delimitadores. Os arquivos DSV devem ser separados por vírgulas.</li><li><code>JSON</code>: Notação de objeto do JavaScript. Os arquivos JSON devem ser compatíveis com XDM</li><li><code>PARQUET</code>: Apache Parquet. Os arquivos Parquet devem ser compatíveis com XDM.</li></ul> |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais que podem ser usados para filtrar resultados. Consulte a seção sobre [parâmetros de consulta](#query) para obter mais informações. |

**Solicitação**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

A [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) oferece suporte ao uso de parâmetros de consulta para visualizar e inspecionar diferentes tipos de arquivos.

| Parâmetro | Descrição |
| --------- | ----------- |
| `columnDelimiter` | O valor de caractere único especificado como delimitador de coluna para inspecionar arquivos CSV ou TSV. Se o parâmetro não for fornecido, o valor padrão será uma vírgula `(,)`. |
| `compressionType` | Um parâmetro de consulta necessário para visualizar um arquivo JSON ou delimitado compactado. Os arquivos compactados compatíveis são: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Define qual tipo de codificação usar ao renderizar a visualização. Os tipos de codificação com suporte são: `UTF-8` e `ISO-8859-1`. **Observação**: o parâmetro `encoding` só está disponível ao assimilar arquivos CSV delimitados. Outros tipos de arquivos serão assimilados com a codificação padrão, `UTF-8`. |

## Próximas etapas

Seguindo este tutorial, você explorou seu sistema de armazenamento em nuvem, encontrou o caminho do arquivo que deseja trazer para [!DNL Experience Platform] e visualizou sua estrutura. Você pode usar essas informações no próximo tutorial para [coletar dados do armazenamento na nuvem e trazê-los para a Experience Platform](../collect/cloud-storage.md).
