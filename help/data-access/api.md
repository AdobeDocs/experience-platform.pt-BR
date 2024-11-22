---
keywords: Experience Platform;página inicial;tópicos populares;acesso a dados;python sdk;spark sdk;api de acesso a dados;exportar;Exportar
solution: Experience Platform
title: Guia da API de acesso a dados
description: A API de acesso a dados é compatível com o Adobe Experience Platform, fornecendo aos desenvolvedores uma interface RESTful focada na descoberta e acessibilidade de conjuntos de dados assimilados no Experience Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 804eeb4ec976cf41fdd450bd8f307499c3ebae03
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 5%

---

# Guia da API de acesso a dados

>[!IMPORTANT]
>
>A API de acesso a dados agora está **obsoleta**. É recomendável usar Destinos para exportar dados do Adobe Experience Platform. Para obter mais informações, consulte a [documentação sobre destinos de exportação do conjunto de dados](../destinations/destination-types.md#dataset-export-destinations).

A API de Acesso a Dados dá suporte ao Adobe Experience Platform, fornecendo aos usuários uma interface RESTful com foco na descoberta e acessibilidade de conjuntos de dados assimilados no [!DNL Experience Platform].

![Um diagrama de como o Acesso a Dados facilita a descoberta e a acessibilidade dos conjuntos de dados assimilados no Experience Platform.](images/Data_Access_Experience_Platform.png)

## Referência da especificação da API

Consulte a [documentação de referência da OpenAPI do Data Access](https://developer.adobe.com/experience-platform-apis/references/data-access/) para exibir um formato padronizado e legível por máquina para facilitar a integração, o teste e a exploração.

## Terminologia {#terminology}

A tabela fornece uma descrição de alguns termos comumente usados neste documento.

| Termo | Descrição |
| ----- | ------------ |
| Conjunto de dados | Uma coleção de dados que inclui um esquema e campos. |
| Lote | Um conjunto de dados coletados por um período e processados juntos como uma única unidade. |

## Recuperar lista de arquivos em um lote {#retrieve-list-of-files-in-a-batch}

Para recuperar uma lista de arquivos pertencentes a um lote específico, use o identificador de lote (batchID) com a API de acesso a dados.

**Formato da API**

```http
GET /batches/{BATCH_ID}/files
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote especificado. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

A matriz `"data"` contém uma lista de todos os arquivos dentro do lote especificado. Cada arquivo retornado tem sua própria ID exclusiva (`{FILE_ID}`) contida no campo `"dataSetFileId"`. Você pode usar esse identificador exclusivo para acessar ou baixar o arquivo.

| Propriedade | Descrição |
| -------- | ----------- |
| `data.dataSetFileId` | A ID de cada arquivo no lote especificado. |
| `data._links.self.href` | O URL para acessar o arquivo. |

## Acessar e baixar arquivos em um lote

Para acessar detalhes específicos de um arquivo, use um identificador de arquivo (`{FILE_ID}`) com a API de Acesso a Dados, incluindo seu nome, tamanho em bytes e um link para baixar.

A resposta contém uma matriz de dados. Dependendo de o arquivo apontado pela ID ser um arquivo individual ou um diretório, a matriz de dados retornada pode conter uma única entrada ou uma lista de arquivos pertencentes a esse diretório. Cada elemento de arquivo inclui os detalhes do arquivo.

**Formato da API**

```http
GET /files/{FILE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID}` | Igual a `"dataSetFileId"`, a ID do arquivo a ser acessado. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta de arquivo único**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `data.name` | O nome do arquivo (por exemplo, `profiles.csv`). |
| `data.length` | O tamanho do arquivo (em bytes). |
| `data._links.self.href` | O URL para baixar o arquivo. |

**Resposta do diretório**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 2
  }
}
```

Quando um diretório é retornado, ele contém uma matriz de todos os arquivos dentro do diretório.

| Propriedade | Descrição |
| -------- | ----------- |
| `data.name` | O nome do arquivo (por exemplo, `profiles.csv`). |
| `data._links.self.href` | O URL para baixar o arquivo. |

## Acessar o conteúdo de um arquivo {#access-file-contents}

Você também pode usar a API [!DNL Data Access] para acessar o conteúdo de um arquivo. Você pode baixar o conteúdo para uma fonte externa.

**Formato da API**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_NAME}` | O nome do arquivo que você está tentando acessar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID}` | A ID do arquivo em um conjunto de dados. |
| `{FILE_NAME}` | O nome completo do arquivo (por exemplo, `profiles.csv`). |

**Resposta**

`Contents of the file`

## Amostras de código adicionais

Para obter amostras adicionais, consulte o [tutorial sobre acesso a dados](tutorials/dataset-data.md).

## Assinar eventos de assimilação de dados {#subscribe-to-data-ingestion-events}

Você pode assinar eventos específicos de alto valor por meio da [Adobe Developer Console](https://developer.adobe.com/console/). Por exemplo, você pode assinar eventos de assimilação de dados para ser notificado de possíveis atrasos e falhas. Consulte o tutorial em [assinatura de notificações de eventos Adobe](../observability/alerts/subscribe.md) para obter mais informações.
