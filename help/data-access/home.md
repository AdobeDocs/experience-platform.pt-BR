---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral do acesso aos dados
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Visão geral do acesso aos dados

A API de acesso a dados oferece suporte à Adobe Experience Platform, fornecendo aos usuários uma interface RESTful focada na descoberta e acessibilidade de conjuntos de dados assimilados na Experience Platform.

![Acesso a dados na plataforma Experience](images/Data_Access_Experience_Platform.png)

## Referência de especificação da API

A documentação de referência da API do Swagger pode ser encontrada [aqui](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## Terminologia

Uma descrição de alguns termos comumente usados neste documento.

| Termo | Descrição |
| ----- | ------------ |
| Conjunto de dados | Uma coleção de dados que inclui schemas e campos. |
| Lote | Um conjunto de dados coletados durante um período de tempo e processados juntos como uma única unidade. |

## Recuperar lista de arquivos em um lote

Usando um identificador de lote (batchID), a API de acesso a dados pode recuperar uma lista de arquivos pertencentes a esse lote específico.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

A `"data"` matriz contém uma lista de todos os arquivos dentro do lote especificado. Cada arquivo retornado tem sua própria ID exclusiva (`{FILE_ID}`) contida no `"dataSetFileId"` campo. Essa ID exclusiva pode ser usada para acessar ou baixar o arquivo.

| Propriedade | Descrição |
| -------- | ----------- |
| `data.dataSetFileId` | A ID de arquivo para cada arquivo no lote especificado. |
| `data._links.self.href` | O url para acessar o arquivo. |

## Acessar e baixar arquivos em um lote

Usando um identificador de arquivo (`{FILE_ID}`), a API de acesso a dados pode ser usada para acessar detalhes específicos de um arquivo, incluindo seu nome, tamanho em bytes e um link para download.

A resposta conterá uma matriz de dados. Dependendo de o arquivo apontado pela ID ser um arquivo individual ou um diretório, a matriz de dados retornada pode conter uma única entrada ou uma lista de arquivos pertencentes a esse diretório. Cada elemento de arquivo incluirá os detalhes do arquivo.

**Formato da API**

```http
GET /files/{FILE_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID}` | Igual à ID `"dataSetFileId"`do arquivo a ser acessado. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data.name` | Nome do arquivo (por exemplo, perfis.csv). |
| `data.length` | Tamanho do arquivo (em bytes). |
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
| `data.name` | Nome do arquivo (por exemplo, perfis.csv). |
| `data._links.self.href` | O URL para baixar o arquivo. |

## Acessar o conteúdo de um arquivo

A API de acesso a dados também pode ser usada para acessar o conteúdo de um arquivo. Isso pode ser usado para baixar o conteúdo em uma fonte externa.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{FILE_ID}` | A ID do arquivo em um conjunto de dados. |
| `{FILE_NAME}` | O nome completo do arquivo (por exemplo, perfis.csv). |

**Resposta**

```
Contents of the file
```

## Amostras de código adicionais

Para obter exemplos adicionais, consulte o tutorial [de acesso a](tutorials/dataset-data.md)dados.


## Assinar eventos de ingestão de dados

A plataforma disponibiliza eventos específicos de alto valor para subscrição por meio do console [de E/S da](https://console.adobe.io/)Adobe. Por exemplo, você pode assinar eventos de ingestão de dados para receber notificações de possíveis atrasos e falhas. Para obter mais informações sobre o uso de Eventos de E/S da Adobe, consulte o guia [de](https://www.adobe.io/apis/experienceplatform/events/docs.html)introdução.