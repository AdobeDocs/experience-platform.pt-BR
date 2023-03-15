---
keywords: Experience Platform;página inicial;tópicos populares;acesso a dados;python sdk;spark sdk;api de acesso a dados;exportar;Exportar
solution: Experience Platform
title: Guia da API de acesso a dados
description: A API de acesso a dados é compatível com o Adobe Experience Platform, fornecendo aos desenvolvedores uma interface RESTful focada na descoberta e acessibilidade de conjuntos de dados assimilados no Experience Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 6%

---

# Guia da API de acesso a dados

A API de acesso a dados é compatível com o Adobe Experience Platform, fornecendo aos usuários uma interface RESTful com foco na descoberta e acessibilidade de conjuntos de dados assimilados no [!DNL Experience Platform].

![Acesso aos dados no Experience Platform](images/Data_Access_Experience_Platform.png)

## Referência da especificação da API

A documentação de referência da API do Swagger pode ser encontrada [aqui](https://www.adobe.io/experience-platform-apis/references/data-access/).

## Terminologia

Uma descrição de alguns termos usados com frequência neste documento.

| Termo | Descrição |
| ----- | ------------ |
| Conjunto de dados | Uma coleção de dados que inclui esquema e campos. |
| Lote | Um conjunto de dados coletados por um período e processados juntos como uma única unidade. |

## Recuperar lista de arquivos em um lote

Ao usar um identificador de lote (batchID), a API de acesso a dados pode recuperar uma lista de arquivos pertencentes a esse lote específico.

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

A variável `"data"` contém uma lista de todos os arquivos do lote especificado. Cada arquivo retornado tem seu próprio identificador exclusivo (`{FILE_ID}`) contido na `"dataSetFileId"` campo. Esse identificador exclusivo pode ser usado para acessar ou baixar o arquivo.

| Propriedade | Descrição |
| -------- | ----------- |
| `data.dataSetFileId` | A ID de cada arquivo no lote especificado. |
| `data._links.self.href` | O URL para acessar o arquivo. |

## Acessar e baixar arquivos em um lote

Ao usar um identificador de arquivo (`{FILE_ID}`), a API de acesso a dados pode ser usada para acessar detalhes específicos de um arquivo, incluindo nome, tamanho em bytes e um link para baixar.

A resposta conterá uma matriz de dados. Dependendo de o arquivo apontado pela ID ser um arquivo individual ou um diretório, a matriz de dados retornada pode conter uma única entrada ou uma lista de arquivos pertencentes a esse diretório. Cada elemento de arquivo incluirá os detalhes do arquivo.

**Formato da API**

```http
GET /files/{FILE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID}` | Equal to the `"dataSetFileId"`, a ID do arquivo a ser acessado. |

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
| `data.name` | Nome do arquivo (por exemplo, profiles.csv). |
| `data.length` | Tamanho do arquivo (em bytes). |
| `data._links.self.href` | O URL para baixar o arquivo. |

**Resposta de diretório**

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
| `data.name` | Nome do arquivo (por exemplo, profiles.csv). |
| `data._links.self.href` | O URL para baixar o arquivo. |

## Acessar o conteúdo de um arquivo

A variável [!DNL Data Access] A API também pode ser usada para acessar o conteúdo de um arquivo. Isso pode ser usado para baixar o conteúdo para uma fonte externa.

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
| `{FILE_NAME}` | O nome completo do arquivo (por exemplo, profiles.csv). |

**Resposta**

`Contents of the file`

## Amostras de código adicionais

Para obter amostras adicionais, consulte o [tutorial sobre acesso a dados](tutorials/dataset-data.md).

## Assinar eventos de assimilação de dados

[!DNL Platform] disponibiliza eventos específicos de alto valor para assinatura por meio do [Console do Adobe Developer](https://www.adobe.com/go/devs_console_ui). Por exemplo, você pode assinar eventos de assimilação de dados para ser notificado de possíveis atrasos e falhas. Veja o tutorial sobre [assinatura de notificações de assimilação de dados](../ingestion/quality/subscribe-events.md) para obter mais informações.
