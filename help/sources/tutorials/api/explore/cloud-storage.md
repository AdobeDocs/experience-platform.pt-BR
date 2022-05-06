---
keywords: Experience Platform, home, tópicos populares, armazenamento na nuvem, armazenamento na nuvem
title: Explorar as pastas de armazenamento da nuvem usando a API do serviço de fluxo
description: Este tutorial usa a API do Serviço de fluxo para explorar um sistema de armazenamento em nuvem de terceiros.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 2%

---

# Explore suas pastas de armazenamento em nuvem usando o [!DNL Flow Service] API

Este tutorial fornece etapas sobre como explorar e visualizar a estrutura e o conteúdo do armazenamento em nuvem usando o [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
>Para explorar o armazenamento na nuvem, você já deve ter uma ID de conexão base válida para uma fonte de armazenamento na nuvem. Se você não tiver essa ID, consulte a [visão geral das fontes](../../../home.md#cloud-storage) para obter uma lista de fontes de armazenamento em nuvem com as quais você pode criar uma conexão básica.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../landing/api-guide.md).

## Explore suas pastas de armazenamento em nuvem

Você pode recuperar informações sobre a estrutura de suas pastas de armazenamento em nuvem fazendo uma solicitação do GET para o [!DNL Flow Service] API enquanto fornece a ID de conexão básica da sua fonte.

Ao executar solicitações do GET para explorar o armazenamento na nuvem, você deve incluir os parâmetros de consulta listados na tabela abaixo:

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
| `{BASE_CONNECTION_ID}` | A ID de conexão básica da fonte de armazenamento em nuvem. |
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

Uma resposta bem-sucedida retorna uma matriz de arquivos e pastas encontrados no diretório consultado. Anote o `path` propriedade do arquivo que deseja fazer upload, pois é necessário fornecê-lo na próxima etapa para inspecionar sua estrutura.

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
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&ileType=delimited&encoding=ISO-8859-1;
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | A ID de conexão do conector de origem de armazenamento da nuvem. |
| `{FILE_PATH}` | O caminho para o arquivo que você deseja inspecionar. |
| `{FILE_TYPE}` | O tipo do arquivo. Os tipos de arquivos suportados incluem:<ul><li>DELIMITADO</code>: Valor separado por delimitadores. Os arquivos DSV devem ser separados por vírgulas.</li><li>JSON</code>: Notação de objeto JavaScript. Os arquivos JSON devem ser compatíveis com XDM</li><li>PARQUET</code>: Apache Parquet. Os arquivos de parâmetro devem ser compatíveis com XDM.</li></ul> |
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

O [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) O suporta o uso de parâmetros de consulta para visualizar e inspecionar tipos de arquivos diferentes.

| Parâmetro | Descrição |
| --------- | ----------- |
| `columnDelimiter` | O valor de caractere único especificado como delimitador de coluna para inspecionar arquivos CSV ou TSV. Se o parâmetro não for fornecido, o valor assumirá como padrão uma vírgula `(,)`. |
| `compressionType` | Um parâmetro de consulta obrigatório para a visualização de um arquivo compactado delimitado ou JSON. Os arquivos compactados compatíveis são: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Define qual tipo de codificação usar ao renderizar a visualização. Os tipos de codificação compatíveis são: `UTF-8` e `ISO-8859-1`. **Observação**: O `encoding` só está disponível ao assimilar arquivos CSV delimitados. Outros tipos de arquivos serão assimilados com a codificação padrão, `UTF-8`. |

## Próximas etapas

Ao seguir este tutorial, você explorou seu sistema de armazenamento em nuvem e encontrou o caminho do arquivo que deseja trazer para [!DNL Platform]e visualizou sua estrutura. Você pode usar essas informações no próximo tutorial para [colete dados do armazenamento em nuvem e traga-os para a Platform](../collect/cloud-storage.md).
